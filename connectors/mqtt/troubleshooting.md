---
description: Fix MQTT data that isn't reaching Chirp — empty Logs, topic mismatches, and devices that won't publish.
---

# MQTT Troubleshooting

When MQTT data isn't reaching Chirp, the failure is almost always at one of three places: Z2M-to-broker, broker-to-Chirp, or Chirp's device routing. This page walks through each in order — the same order to use when diagnosing — plus the two patterns that catch out almost every first-time MQTT user (empty Logs tab, no publish from a wall-switch toggle).

**Start by letting Chirp narrow it down for you.** Open the device's **Connection** tab and read its diagnostics — they say whether messages are arriving, whether Chirp understood them, and whether they're being saved, which usually points straight at the right phase below. See [Connection Diagnostics](../../devices/connection-diagnostics.md). For the connector itself, its **Connector diagnostics** area has **Source health**, **Incoming**, and **Activity** tabs — the fastest way to tell a broker problem from a single misbehaving device.

## Phase 1 — Z2M is not connecting to the broker

**Symptoms:** Z2M container is running, but the connector's **Last data received** in Chirp never updates. No `MQTT publish` log lines from Z2M.

Check `docker compose logs zigbee2mqtt` for one of these:

| Log line | Cause | Fix |
|----------|-------|-----|
| `Error: Failed to find adapter` | Wrong `adapter:` value in `configuration.yaml`, or wrong `serial.port` | For Sonoff ZBDongle-E (EFR32MG24): `adapter: ezsp`. For ZBDongle-P (CC2652P): `adapter: zstack`. Check the dongle packaging or label — the USB ID is the same for both. Verify `serial.port` matches the actual `/dev/ttyUSB*` device (`ls /dev/tty* | grep USB`). |
| `Error: Failed to connect to MQTT broker` | Wrong server URL, port, or credentials | Re-copy all four credentials from Chirp's connector page. Check for trailing whitespace — `\n` at the end of a copied password is a common cause. Verify the port is **1884** for Cloud MQTT (not the default 1883). |
| `SSL handshake failed` | TLS negotiation issue | Add `ssl: true` under the `mqtt:` section of `configuration.yaml` and restart Z2M. |
| `Authentication failed` | Wrong username or password | If the password was lost, rotate the credentials from Chirp's connector settings, then update `configuration.yaml` with the new password. |
| (no MQTT lines, but connection looks fine) | `log_level: info` is hiding publish events | Change to `log_level: debug` in `configuration.yaml` and restart Z2M. The `MQTT publish` lines are only logged at debug. |

The first MQTT message Z2M sends is its bridge state announcement (`{base_topic}/bridge/state`, payload `{"state":"online"}`). If you see that line in the logs, Z2M is connected and the broker accepted the connection. From there, problems are downstream.

## Phase 2 — Z2M is publishing but the connector's Last data received doesn't update

**Symptoms:** Z2M log shows `MQTT publish: topic '...' payload '...'` lines, but Chirp's connector page shows **Last data received** is still empty.

This is rare — if the Z2M side is publishing successfully on a topic that starts with the right Topic prefix, the broker accepts it. Things to verify:

- **Topic prefix matches.** Z2M's `base_topic` must start with the exact Topic prefix Chirp gave you. For Cloud MQTT, that's `iot/{org}/{conn}/zigbee2mqtt` — the first three segments must match exactly what Chirp's connector page shows.
- **The connector is the right one.** If you have multiple Cloud MQTT connectors, double-check which one Z2M is configured against. The Topic prefix is unique per connector.
- **External MQTT only — Chirp can reach your broker.** External MQTT is the case where this can genuinely fail for network reasons. Even after publishing locally to your Mosquitto broker, the message reaches Chirp only if Chirp can dial out to your broker's public address. Run a one-shot test publish from `mosquitto_pub` against the public address (your ngrok TCP endpoint or DDNS hostname) — see [External MQTT](external-mqtt.md) for the test command. If the local broker accepts it but Chirp's **Last data received** stays empty, the public reachability is the problem (firewall, expired ngrok session, wrong port forward).

## Phase 3 — Last data received updates but the device's Mapping tab is empty

**Symptoms:** The connector shows recent Last data received timestamps, but when you open a registered device, the Mapping tab's Value column is empty and nothing's coming in.

This is a device-routing problem inside Chirp. The connector is receiving messages but they're not matching the device record.

- **Device ID Topic pattern doesn't match the published topic.** Z2M publishes to `zigbee2mqtt/{friendlyName}` (after Chirp strips the prefix). The Device ID Topic field must be `zigbee2mqtt/{{deviceId}}` — exactly. Common mistakes: leading slash, missing the `zigbee2mqtt/` prefix, an extra path segment that the published topic doesn't have.
- **Device ID is byte-for-byte different from the friendly name.** This is the single most common cause. Chirp's Device ID input strips whitespace, so a Z2M friendly name with spaces (`Living Room Sensor`) won't match a Device ID typed with the same spaces — Chirp stored a different string. The fix: rename the device in Z2M to a whitespace-free name (`LivingRoomSensor`), and use the same exact string in Chirp's Device ID field. Capitalisation is preserved and significant — `LivingRoomSensor` and `livingroomsensor` are different.

Verify what Z2M is publishing right now:
```bash
docker compose logs zigbee2mqtt | grep "MQTT publish" | grep -v bridge | tail -5
```

The topic in those lines is what your Device ID Topic and Device ID need to match against.

## Phase 4 — Mapping tab Value column updates but Logs tab is empty

**Symptoms:** Open a registered device, the Mapping tab shows live values and Last update timestamps, but the Logs tab stays empty even after toggling the device. The most common cause of "is this thing broken?"

It's not broken. The two tabs read different things:

- **Mapping tab Value column** = a live snapshot of the most recent payload. Updates on every accepted publish, regardless of whether you've finished setting up Connector keys.
- **Logs tab** = per-sensor history. Populated only by publishes that arrive *after* you've saved Connector keys for that sensor.

If the most recent publish happened before you saved Connector keys, that publish never reaches Logs — only future publishes will. The fix is to **generate a fresh publish**.

For a Zigbee device the cleanest way is to use the Z2M web UI:

1. Open `http://localhost:8080`.
2. Click your device.
3. Drag a control — the brightness slider on a bulb, the on/off toggle on a plug, etc.

Z2M sends a `/set` command, the device confirms the new state, and Z2M publishes the confirmed payload back. That publish flows through Chirp into the Logs tab.

Alternatively, you can poll the device with a `/get` request via `mosquitto_pub` — useful when the device doesn't have a controllable state (a temperature sensor, for example).

## Phase 5 — physical wall-switch toggles don't generate publishes

**Symptoms:** You toggle the wall switch for a Zigbee bulb. The light comes on. The Logs tab still shows nothing.

Many Zigbee CCT bulbs (the Paulmann 50064 confirmed; many other brands behave the same) **don't send an MQTT publish on a physical power-cycle**. The bulb's firmware only reports state changes that came in over Zigbee — not changes caused by the wall switch.

Actions that **do** generate a publish:

| Action | Notes |
|--------|-------|
| Drag a control or click the toggle in the Z2M web UI | Z2M sends `/set` over Zigbee, bulb confirms, Z2M publishes the new state. The cleanest setup-time check. |
| `mosquitto_pub` to `{base_topic}/{friendlyName}/get` with `{"state":""}` payload | Forces Z2M to poll the bulb for current state and publish what it reads back. Useful for non-controllable devices and for forcing a publish on demand. Local Z2M-side verification, not a Chirp control path. |
| Wait for the device's next scheduled report | Battery sensors typically wake on a schedule (every 5 minutes, every hour, etc.). Mains-powered bulbs without state-change reporting won't publish unless commanded. |

## Forcing Z2M to publish: the `/get` command

The `/get` request is the tool of last resort when you need a current-state publish from a device that won't generate one on its own. Send a JSON payload with empty strings as values for the keys you want the bulb to report:

```bash
docker run --rm eclipse-mosquitto:2 mosquitto_pub \
  -h mqtt-iot.chirpwireless.io \
  -p 1884 \
  --cafile /etc/ssl/certs/ca-certificates.crt \
  -u {your-cloud-mqtt-username} \
  -P '{your-cloud-mqtt-password}' \
  -t "iot/{org}/{conn}/zigbee2mqtt/{friendlyName}/get" \
  -m '{"state":"","brightness":"","color_temp":""}'
```

(Use your actual Cloud MQTT credentials and connection prefix. For External MQTT, replace the broker host/port/auth with your local broker's settings, and use `zigbee2mqtt/{friendlyName}/get` as the topic with no prefix.)

Z2M sends ZCL read requests to the bulb and publishes one or more responses with the current state. One `/get` can produce 2–4 publishes back as Z2M polls different attribute clusters in sequence — that's normal.

This is local Z2M-side verification — it generates a publish that Chirp consumes. It's not a Chirp API control surface.

## When a Zigbee device won't pair at all

Pairing failures are entirely a Z2M / coordinator / device problem — Chirp isn't involved. The usual culprits:

- **Permit join is closed.** The 180-second window has expired. Click Permit join again in the Z2M web UI.
- **Device is already paired to another network.** Many Zigbee devices remember the last network they joined. Factory-reset the device first (procedure varies — check the manufacturer's instructions or the device's [Z2M page](https://www.zigbee2mqtt.io/supported-devices/)).
- **Coordinator range too short.** Move the device within 1–2 meters of the coordinator for initial pairing. After joining, Zigbee mesh routing handles distance — but the first join needs proximity.
- **Wrong reset procedure.** Different devices need different reset sequences. Bulbs often require a 5×-power-cycle pattern. Sensors usually have a small button. Always follow the manufacturer's guide.

For the Paulmann 50064 specifically, see the [tested device guide](../../devices/tested-device-guides/zigbee/paulmann-50064-light-bulb.md) — the 5×-cycle-then-stop procedure is documented there with the timing details.

## Resetting Cloud MQTT credentials

If the Cloud MQTT password is lost or compromised:

1. Open the connector in Chirp.
2. In edit mode, regenerate the password.
3. Copy the new password.
4. Update Z2M's `configuration.yaml` (`mqtt: password:`).
5. Restart the Z2M container: `docker compose restart zigbee2mqtt`.

The username and Topic prefix don't change on rotation.

## Where to go next

- Back to [Topics and device routing](topics-and-device-routing.md) — to confirm the Device ID Topic pattern and friendly-name rules.
- [External MQTT](external-mqtt.md) — for broker-side issues with self-hosted brokers.
- [Setting up Zigbee2MQTT](zigbee2mqtt.md) — to recheck the Z2M install.
