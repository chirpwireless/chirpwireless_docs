# External MQTT

External MQTT is the second way to connect MQTT data into Chirp: instead of using a broker Chirp provides, you point Chirp at one you already run. Chirp connects out to your broker, subscribes to its messages, and brings them into the same device-routing pipeline as everything else.

## How the connection works

The most important thing to understand up front: **Chirp connects out to your broker**, not the other way around. This single fact decides everything that follows.

Practically that means your broker must be reachable from the public internet — Chirp's cloud needs to dial it. A broker running on `192.168.1.50:1883` on your home network is invisible to Chirp. Tunnels and port-forwarding fix that, with the trade-off that running an exposure tool such as ngrok does not by itself confirm Chirp can reach the broker — you must publish a test message after saving and verify the connector's **Last data received** field updates.

If your broker is already on a VPS or a cloud account, you're set — point Chirp at the public hostname and you're done.

## When to choose External MQTT

- You already run Mosquitto, HiveMQ Cloud, or another broker, and you want Chirp to consume from it without rerouting devices.
- Your home automation setup (Home Assistant, Node-RED) is already publishing to a broker, and Chirp is one more subscriber.
- You want Chirp to share data with other consumers — your dashboards, your scripts, your local NAS — through one common bus.

If none of those apply, [Cloud MQTT](cloud-mqtt.md) is simpler.

## Setting up Mosquitto on a home server

Mosquitto is the most common open-source broker for home use. The minimal Docker setup looks like this:

`~/mqtt/docker-compose.yml`:
```yaml
services:
  mosquitto:
    image: eclipse-mosquitto:2
    container_name: mosquitto
    restart: unless-stopped
    ports:
      - "1883:1883"
    volumes:
      - ./mosquitto/config:/mosquitto/config
      - ./mosquitto/data:/mosquitto/data
```

`~/mqtt/mosquitto/config/mosquitto.conf`:
```
listener 1883
allow_anonymous true
persistence true
persistence_location /mosquitto/data/
log_dest stdout
```

Bring it up:
```bash
cd ~/mqtt
docker compose up -d mosquitto
docker compose logs mosquitto
```

You should see `Opening ipv4 listen socket on port 1883` and `mosquitto version X.Y.Z running` in the logs. If you do, the broker is up locally — internet exposure comes next.

> **`log_dest stdout` matters.** A common mistake is to log to a host-mounted file (`log_dest file /mosquitto/log/mosquitto.log`). On many systems the bind-mount permissions or security labels prevent Mosquitto from writing there, and the container fails to start. Logging to stdout works in every Docker setup, and `docker compose logs` shows the same content.

> **Port 1883 is sometimes already taken.** On a developer machine, another tool may have already bound port 1883 — for example, a kubectl port-forward or a different broker process. The container will fail with `failed to bind host port 0.0.0.0:1883/tcp: address already in use`. Diagnose with `ss -tlnp | grep 1883` to see what's holding the port. The simplest fix is to remap Mosquitto's host-side port to anything free: `"1885:1883"` keeps the container internal port at 1883 but binds it to host port 1885, and any device or tunnel pointing at the host needs to use 1885.

## Exposing the broker to the internet

You have two practical options.

### Option A — ngrok TCP tunnel (good for testing)

ngrok creates a public TCP endpoint that forwards back to your local Mosquitto. It's the fastest way to get something Chirp can reach.

1. Install ngrok using the current instructions from `https://ngrok.com/download` for your operating system.
2. Sign up at `https://dashboard.ngrok.com/signup` (free tier is fine for this).
3. Get your auth token from `https://dashboard.ngrok.com/get-started/your-authtoken`.
4. Configure ngrok with the token:
   ```bash
   ngrok config add-authtoken YOUR_TOKEN_HERE
   ```
5. Start a TCP tunnel pointing at the host port your broker is bound to:
   ```bash
   ngrok tcp 1883
   ```
   ngrok prints something like `Forwarding tcp://0.tcp.ngrok.io:14217 -> localhost:1883`. The `0.tcp.ngrok.io:14217` part is your broker's public address — you'll use it in Chirp's Broker URL field.

ngrok TCP tunnels require an authenticated account; without the auth token, the tunnel won't start. The free tier is sufficient for testing, but the address changes each time you restart ngrok — for a permanent setup, ngrok offers paid plans with reserved TCP addresses, or use Option B.

### Option B — router port forwarding (permanent)

For a permanent home setup:

1. Pick a stable external port (anything not already in use — 8883 is conventional for MQTT-over-TLS).
2. In your router's settings, add a port forward: external port 8883 → your machine's local IP : Mosquitto's host port (1883 or whatever you remapped to).
3. Configure a dynamic DNS hostname (Duck DNS, No-IP, your router may have a built-in option) so you have a stable address even when your home IP changes.

Use `mqtt://yourhome.duckdns.org:8883` (or `mqtts://...` if you've configured TLS) as Chirp's Broker URL.

This approach doesn't depend on a third party and gives you a fixed address forever.

## Securing Mosquitto before exposing it publicly

`allow_anonymous true` is fine while you're verifying the local setup, but **don't expose an anonymous broker to the internet**. Anyone on the internet who finds it can publish or subscribe. Switch to password authentication before going public.

Edit `mosquitto.conf`:

```
listener 1883
allow_anonymous false
password_file /mosquitto/config/passwd
persistence true
persistence_location /mosquitto/data/
log_dest stdout
```

Create the password file:

```bash
docker exec mosquitto mosquitto_passwd -c /mosquitto/config/passwd myuser
# enter password when prompted
docker compose restart mosquitto
```

Now your broker requires `myuser` + the password you set. Update Zigbee2MQTT (`configuration.yaml` `user:` and `password:` fields) and Chirp's connector with the same credentials.

For TLS — encrypted broker traffic — Mosquitto supports it via certificates. The Mosquitto documentation has the full setup; not strictly required for testing but recommended for any permanent public deployment.

## Creating the External MQTT connector in Chirp

1. **Connectors → Add connector**.
2. Pick **External MQTT**.
3. Fill in:
   - **Name**: any label, e.g. `Home Mosquitto`.
   - **Broker URL**: the public address. For ngrok, `mqtt://0.tcp.ngrok.io:14217`. For router forwarding, `mqtt://yourhome.duckdns.org:8883`. Use `mqtts://` if your broker is configured for TLS.
4. Pick the **authentication method**:
   - **Anonymous** if your broker still allows anonymous (for testing only).
   - **Basic** with the username and password you set.
   - **Certification** for TLS with client certs (uploads three files — CA Certificate, Client Certificate, Private Key).
   - **JWT Token** for token-based auth.
5. Tap **Save**.

Chirp creates an outbound bridge from its managed broker to your broker, subscribes to all topics on your broker, and forwards them into the same internal pipeline as Cloud MQTT data.

## Verifying the connection works end to end

After saving the connector, **publish a test message and confirm Chirp's Last data received updates** — this is the only way to confirm the platform can actually reach your broker. Just having ngrok or a port-forward "running" doesn't prove the path is open.

The simplest test is a one-shot publish from the same machine running Mosquitto:

```bash
docker run --rm eclipse-mosquitto:2 mosquitto_pub \
  -h 0.tcp.ngrok.io -p 14217 \
  -u myuser -P 'your-password' \
  -t test/hello -m '{"hello":"world"}'
```

(Substitute your actual ngrok address or DDNS hostname, and your credentials.)

Within a few seconds, the connector's **Last data received** field in Chirp should update. If it doesn't, the message never reached Chirp — see [Troubleshooting](troubleshooting.md) for a checklist (the most common causes are firewall blocking the host port, ngrok session expired, or wrong credentials).

## Configuring Zigbee2MQTT for an External MQTT connector

In Z2M's `configuration.yaml`:

```yaml
mqtt:
  base_topic: zigbee2mqtt
  server: mqtt://mosquitto:1883
  # if you set up password auth:
  user: myuser
  password: your-password
```

Note the differences from Cloud MQTT:

- **`base_topic` is just `zigbee2mqtt`**, with no Chirp prefix in front. Chirp's bridge handles the prefix internally.
- **`server` points at your local broker.** If both Z2M and Mosquitto are running in the same Docker Compose project, use the service name (`mqtt://mosquitto:1883`) — Docker's internal DNS resolves it. If Z2M is running on the host and Mosquitto in Docker, use `mqtt://localhost:{host port}` (1883 by default, or your remapped port).
- **No TLS unless you configured it** — local Mosquitto on Docker speaks plain MQTT by default.

After Z2M restarts and the bulb publishes, you'll see the device-level topic in Chirp as `zigbee2mqtt/{friendlyName}` — same as Cloud MQTT. The Device ID Topic in the device registration form is `zigbee2mqtt/{{deviceId}}` for both paths.

## Limits

External MQTT connectors are limited to 10 per home. If you have several brokers — a Mosquitto on the home server, a HiveMQ for outdoor sensors, a third for a hobby project — each gets its own connector and the 10 covers all of them combined.
