---
description: Install Zigbee2MQTT to bridge your Zigbee bulbs and sensors into Chirp through the MQTT connector.
---

# Setting up Zigbee2MQTT

Zigbee2MQTT (Z2M) is the bridge between your Zigbee devices and your MQTT broker. Devices speak Zigbee — a low-power radio protocol — to a USB or network-attached coordinator. Z2M is the software, running on the same machine as the coordinator, that turns each Zigbee message into an MQTT publish. Once Z2M is running, every Zigbee sensor and bulb in your home becomes an MQTT publisher, and Chirp's MQTT connector picks it up like any other MQTT device.

This page is the generic Zigbee2MQTT setup. We worked through it with a Sonoff ZBDongle-E coordinator and a Paulmann 50064 bulb, but Z2M supports thousands of coordinators and devices — anything in the [supported devices list](https://www.zigbee2mqtt.io/supported-devices/) follows the same flow. If you have the exact hardware we tested, the [Sonoff ZBDongle-E walkthrough](../../gateways/zigbee2mqtt-hubs/sonoff-zbdongle-e-coordinator.md) and the [Paulmann 50064 walkthrough](../../devices/tested-device-guides/zigbee/paulmann-50064-light-bulb.md) drop you into the specifics. Otherwise, follow this generic setup and consult your hardware's manufacturer for pairing details — the rest is identical.

## What runs where

A small mental-model warning, because this confuses a lot of people first time around: **the coordinator is the radio bridge, not the brain.**

- **USB coordinators** (Sonoff ZBDongle-E, ZBDongle-P, SkyConnect, ConBee II, etc.) — radio chip plus firmware, communicating with your machine over USB serial using a binary protocol like EZSP or Z-Stack. They have no IP stack, no Wi-Fi, no Ethernet, no operating system.
- **Network-attached coordinators** (SMLIGHT SLZB-06 and similar) — the same radio role, but with a small embedded Linux that exposes the coordinator over Ethernet or Wi-Fi. They have an IP interface for transport, but they don't run MQTT — Z2M still does that.

In both cases, the coordinator handles the Zigbee radio plus protocol-to-transport bridge; **Zigbee2MQTT is the software** that opens the coordinator's transport (serial port for USB, TCP for network-attached), sends Zigbee commands, receives Zigbee messages, translates them to JSON, and publishes them to MQTT. All the device-management intelligence lives in Z2M.

```
Zigbee device → [Zigbee radio]
                    ↓
                Coordinator (radio + firmware, plugged into your machine)
                    ↓
                /dev/ttyUSB0 (or network port for SLZB-06 etc.)
                    ↓
                Zigbee2MQTT (running on your machine)
                    ↓
                MQTT (TCP/TLS to your broker — Chirp Cloud or your own Mosquitto)
                    ↓
                Chirp
```

Practical implication: stop the Z2M container or unplug the host machine and your Zigbee devices stop reaching MQTT, even though their LEDs may still be on and the radios are still healthy. Z2M is the active link.

## What you need

- A **machine that's always on** with a USB port (or a network-attached coordinator on your LAN). A Raspberry Pi, a small home server, an old laptop, an Intel NUC — anything Linux-based works fine. Z2M can also run on macOS or Windows but Docker on Linux is the most common deployment.
- **A Zigbee coordinator.** Any [supported coordinator](https://www.zigbee2mqtt.io/guide/adapters/) — Sonoff ZBDongle-P or ZBDongle-E, SMLIGHT SLZB-06, ConBee II, SkyConnect, etc.
- **Docker and Docker Compose** installed on the host machine. (Z2M has other deployment options, but Docker is the simplest and what we'll use here.)
- **An MQTT broker** to publish to — either a [Cloud MQTT connector](cloud-mqtt.md) from Chirp, or your own broker via [External MQTT](external-mqtt.md).

## Step 1 — set up the working directory

On the host machine:

```bash
mkdir -p ~/zigbee2mqtt/data
cd ~/zigbee2mqtt
```

You'll create two files in here: a `docker-compose.yml` and the Z2M `configuration.yaml`.

## Step 2 — confirm the coordinator is detected (USB coordinators)

For USB-attached coordinators, plug the dongle in (use the included extension cable if there is one — the metal of your computer chassis attenuates 2.4 GHz signal, and the cable physically moves the antenna away from interference) and check that Linux sees it:

```bash
ls /dev/tty* | grep -E "USB|ACM"
```

You should see `/dev/ttyUSB0` (for CP210x-based dongles like the Sonoff series) or `/dev/ttyACM0` (for some other adapters). If multiple USB serial devices are plugged in, your coordinator will be the highest-numbered one — note which path is yours, you'll need it in `configuration.yaml`.

```bash
lsusb | grep -i "silicon\|zigbee\|conbee"
```

This shows the chip — useful when you're not sure which dongle variant you have. For Sonoff dongles specifically, both ZBDongle-P and ZBDongle-E show as `Silicon Labs CP210x UART Bridge` on `lsusb`, so you must check the packaging or the label on the dongle body to tell them apart.

For network-attached coordinators (SLZB-06, etc.), there's no `/dev/tty*` device — instead you'll use a `tcp://` URL in `configuration.yaml`.

## Step 3 — `docker-compose.yml`

`~/zigbee2mqtt/docker-compose.yml`:

```yaml
services:
  zigbee2mqtt:
    image: koenkk/zigbee2mqtt:latest
    container_name: zigbee2mqtt
    restart: unless-stopped
    volumes:
      - ./data:/app/data
      - /run/udev:/run/udev:ro
    ports:
      - "8080:8080"
    environment:
      - TZ=Etc/UTC
    devices:
      - /dev/ttyUSB0:/dev/ttyUSB0
```

A few details that aren't obvious:

- `./data:/app/data` is where Z2M reads `configuration.yaml` and writes its device database. Persisting this directory means paired devices and settings survive container restarts.
- `/run/udev:/run/udev:ro` — without this, Z2M can fail to auto-detect the adapter on some systems. Read-only because Z2M only needs to query udev, not modify it.
- `devices: /dev/ttyUSB0:/dev/ttyUSB0` passes the USB coordinator into the container. Docker handles the permissions, so you don't need to add your user to the `dialout` group on the host.
- For network-attached coordinators, omit the `devices:` mapping — Z2M will use the `tcp://` URL from `configuration.yaml`.

If your coordinator is at a different path (e.g. `/dev/ttyACM0`), update both sides of the `devices:` mapping.

## Step 4 — `configuration.yaml`

`~/zigbee2mqtt/data/configuration.yaml`:

```yaml
homeassistant: false
permit_join: false

mqtt:
  base_topic: iot/{your-org-segment}/{your-connection-segment}/zigbee2mqtt
  server: mqtts://mqtt-iot.chirpwireless.io:1884
  user: {username from Chirp}
  password: {password from Chirp}

serial:
  port: /dev/ttyUSB0
  adapter: ezsp

advanced:
  log_level: debug
  channel: 11

frontend:
  enabled: true
  port: 8080
```

Three settings deserve attention:

- **`adapter: ezsp` vs `adapter: zstack`** — this tells Z2M what kind of radio chip your coordinator has. **Sonoff ZBDongle-E (EFR32MG21/MG24)** uses `ezsp`. **Sonoff ZBDongle-P (CC2652P)** uses `zstack`. They look almost identical externally and have the same USB ID, but the protocol is different. Picking the wrong one logs `Error: Failed to find adapter` and Z2M exits. For other adapters, see the [Z2M adapter guide](https://www.zigbee2mqtt.io/guide/adapters/).
- **`log_level: debug`** — leave this on while you're setting things up. At `info` level, Z2M doesn't log MQTT publish lines, which makes it impossible to tell whether the broker connection is working. Switch back to `info` once everything is verified.
- **`channel: 11`** — Zigbee shares the 2.4 GHz band with Wi-Fi. Channels 11, 15, 20, and 25 are commonly chosen because they reduce overlap with the most-used Wi-Fi channels (1, 6, 11). They are not perfectly non-overlapping, but they're the safer starting points if your Wi-Fi uses default channels. **You can't change the Zigbee channel later without re-pairing every device**, so pick once and don't change it.

For External MQTT, the `mqtt:` section is simpler — see [External MQTT](external-mqtt.md) for the configuration. The rest of `configuration.yaml` is identical.

## Step 5 — start Z2M

```bash
cd ~/zigbee2mqtt
docker compose up -d
docker compose logs -f zigbee2mqtt
```

You're looking for these lines, in roughly this order:

```
z2m: zigbee-herdsman started (reset)
z2m: Coordinator firmware version: ... type EZSP v13
z2m: Currently 0 devices are joined.
z2m: Connecting to MQTT server at mqtts://mqtt-iot.chirpwireless.io:1884
z2m: Connected to MQTT server
z2m:mqtt: MQTT publish: topic '.../bridge/state', payload '{"state":"online"}'
z2m: Started frontend on port 8080
z2m: Zigbee2MQTT started!
```

The first MQTT publish line is your end-to-end signal: Z2M's bridge announced itself online, the broker accepted it, and Chirp will see the message arrive. You can verify on the Chirp side too — open the connector's detail page and check **Last data received**. Within a few seconds of Z2M starting, this field updates with a timestamp.

If you don't see those log lines, the most common causes are:

- `Error: Failed to find adapter` → wrong `adapter:` value or wrong serial port. Re-check `serial.port` and `serial.adapter`.
- `Error: Failed to connect to MQTT broker` → wrong server URL, credentials, or port. Re-copy the four credentials from Chirp; check for trailing whitespace.
- `SSL handshake failed` → TLS issue. Add `ssl: true` under `mqtt:` and restart.
- `Authentication failed` → wrong username or password. Rotate the connector's credentials in Chirp and update `configuration.yaml`.

### What to expect on first start

Z2M does two things the first time it boots that can look like errors but aren't:

- **It rewrites your `configuration.yaml`.** Z2M reformats the YAML and adds a `version: 5` line at the bottom. Your values are preserved exactly — only formatting changes. Long single-line strings may be wrapped using YAML block-scalar notation (`>-`), which is functionally identical to the original.
- **It creates migration log files** in `~/zigbee2mqtt/data/` named `migration-1-to-2.log` through `migration-4-to-5.log`. These are Z2M's internal config-schema migrations between its own versions. Normal — no action needed.

If you see your `configuration.yaml` looking different after first boot, that's why. The migration logs can be safely ignored.

## Step 6 — open the Z2M web UI

Z2M ships with a small web interface. Open `http://localhost:8080` (or the IP of your host machine + port 8080 if you're remote). No login by default.

Key things you'll use it for:

- **Permit join** — the green shield icon at the top opens the Zigbee network for new devices to pair (180 seconds at a time).
- **Devices** — list of paired devices, with their IEEE addresses, friendly names, models, and link quality.
- **Logs** — the same output as `docker compose logs -f` but in the browser.
- **Per-device controls** — clicking a device opens a panel where you can rename it, see its current state, and (for actuators like bulbs and plugs) toggle / dim / change settings. These controls publish MQTT `/set` commands, which is also how you can generate a fresh publish during setup-time verification — drag a slider, the bulb confirms the new state, and Z2M re-publishes the payload that Chirp consumes.

## Step 7 — pair your first device

Pairing is device-specific. Generic pattern:

1. In the Z2M web UI, click **Permit join (All)** — the green shield. The Zigbee network is open for 180 seconds.
2. Put your Zigbee device into pairing mode. **The procedure varies by device** — consult the manufacturer's manual or the device's [Z2M page](https://www.zigbee2mqtt.io/supported-devices/). Common patterns:
   - Bulbs: power-cycle 5 times in a row (on/off/on/off/on/off/on/off/on, ~2 seconds each). Many bulbs flash on the 5th on-cycle to signal pairing mode — when they do, **stop cycling and leave them on**.
   - Battery sensors: hold a small reset button (often inside a battery compartment) for 5–10 seconds.
   - Wall-plugs: hold the physical button for 5+ seconds.
3. Within 10–30 seconds, Z2M's web UI shows the device in the Devices list, identified by its IEEE address (`0x...`).
4. Z2M auto-identifies the model from its built-in device database — for most devices, you'll see the brand and model name in the Devices list immediately.

If pairing fails: the 180-second window may have closed (click Permit join again), or the device may already be paired to a previous network and need a factory reset first. Some bulbs need a full reset before they'll accept a new network — see the manufacturer's instructions, or the [Paulmann 50064 walkthrough](../../devices/tested-device-guides/zigbee/paulmann-50064-light-bulb.md) if that's what you're pairing.

## Step 8 — give the device a friendly name

When a device pairs, its initial friendly name is its IEEE address (something like `0x00158d0001abc123`). Rename it to something readable — that name becomes both the device-level MQTT topic Z2M publishes to AND the Device ID you'll enter in Chirp.

In the Z2M web UI:
1. Click the device in the Devices list.
2. Click the pencil icon next to the name.
3. Type a new name. **Avoid spaces** — they cause silent mismatch with Chirp's Device ID input. Use CamelCase (`LivingRoomSensor`) or snake_case (`living_room_sensor`). Don't use `/`, `#`, or `+` (those are MQTT-reserved characters).
4. Press Enter.

After renaming, Z2M publishes to `{base_topic}/{newName}` immediately. The IEEE-address topic stops receiving data.

## Step 9 — register the device in Chirp

The device is now publishing JSON payloads on a topic like `iot/{org}/{conn}/zigbee2mqtt/LivingRoomSensor` (Cloud MQTT) or `zigbee2mqtt/LivingRoomSensor` (External MQTT). Now register it in Chirp.

The full registration flow — the Mapping/Topic sub-tabs, byte-for-byte Device ID, the Connector key two-pass save, the Reported State vs Telemetry choice — is on [Topics and device routing](topics-and-device-routing.md). That's the next page to read.

## Where to go next

- [Topics and device routing](topics-and-device-routing.md) — register the device.
- [Sonoff ZBDongle-E coordinator walkthrough](../../gateways/zigbee2mqtt-hubs/sonoff-zbdongle-e-coordinator.md) — if you have this exact dongle and want the physical-install detail.
- [Paulmann 50064 light bulb walkthrough](../../devices/tested-device-guides/zigbee/paulmann-50064-light-bulb.md) — if you have this exact bulb and want the pairing-procedure detail.
- [Troubleshooting](troubleshooting.md) — when something isn't working.
