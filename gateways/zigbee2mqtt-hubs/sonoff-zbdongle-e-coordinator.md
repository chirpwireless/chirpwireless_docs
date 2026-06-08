---
description: Plug in the Sonoff ZBDongle-E, confirm Linux sees it, and get ready to run your Zigbee2MQTT hub.
---

# Sonoff ZBDongle-E coordinator

This is a hardware-specific walkthrough for setting up a **Sonoff ZBDongle-E** — the Zigbee coordinator dongle we tested our Zigbee2MQTT-on-Chirp setup with. If you have this exact dongle, follow these steps to confirm it's plugged in correctly and Linux sees it. Then continue to [Setting up Zigbee2MQTT](../../connectors/mqtt/zigbee2mqtt.md) for the software install — Z2M is generic across coordinators, so once your dongle is detected, the rest of the setup follows the same flow as any other supported coordinator.

If you have a **different coordinator** — Sonoff ZBDongle-P, SLZB-06, ConBee II, SkyConnect, etc. — you don't need this page. Z2M supports many coordinators, and the [Z2M adapter guide](https://www.zigbee2mqtt.io/guide/adapters/) covers them all. The Sonoff ZBDongle-E happens to be the one we tested with — others work just as well.

## What's in the box

The Sonoff ZBDongle-E ("Dongle Plus MG24") ships with:

- The USB dongle (antenna built in)
- A short USB-A extension cable

That's it. No driver disc, no software, no batteries.

## Step 1 — plug it in (use the extension cable)

**Always use the included extension cable.** Plugging the dongle directly into a motherboard USB port causes the metal of your computer chassis to attenuate the 2.4 GHz Zigbee signal. The cable physically moves the antenna away from interference, and the difference in pairing reliability and range is significant.

1. Connect the short extension cable to the dongle.
2. Plug the cable into any available USB-A port on your machine.
3. Watch the LED on the dongle:
   - **Solid blue** — powered up and running coordinator firmware.
   - **No light** — check the cable and try a different USB port.
4. Wait about 3 seconds for Linux to enumerate the device.

That's the entire physical install. No driver to download, no installer to run, no reboot needed.

## Step 2 — confirm Linux sees the dongle

The CP210x USB-UART chip used in the ZBDongle-E is supported natively by the Linux kernel since version 3.x. The driver loads automatically.

```bash
ls /dev/tty* | grep -E "USB|ACM"
```

You should see `/dev/ttyUSB0`. (If you have other USB-serial devices already plugged in, your dongle will be the highest-numbered `/dev/ttyUSBN`.)

```bash
lsusb | grep -i silicon
```

Expected output:
```
Bus 003 Device 004: ID 10c4:ea60 Silicon Labs CP210x UART Bridge
```

The `10c4:ea60` USB ID is the CP210x chip — used by both the ZBDongle-E **and** the ZBDongle-P. You **cannot** tell the two dongles apart from `lsusb` alone. The packaging or the label on the dongle body is the only reliable way:

| Dongle | Radio chip | Z2M `serial.adapter:` value |
|--------|-----------|----------------------------|
| **ZBDongle-E** (look for "MG24" or "EFR32" on the packaging) | EFR32MG24 | `ezsp` |
| ZBDongle-P (look for "CC2652P") | CC2652P | `zstack` |

Picking the wrong adapter value in `configuration.yaml` causes Z2M to log `Error: Failed to find adapter` and exit. **For the ZBDongle-E it's `ezsp`** — write that down for the next step.

## Step 3 — verify the driver

Optional but useful for confirming everything is healthy:

```bash
cat /sys/class/tty/ttyUSB0/device/uevent
```

Expected line:
```
DRIVER=cp210x
```

```bash
ls -la /dev/ttyUSB0
```

Expected output (the exact group may be `dialout` or `uucp` depending on distribution):
```
crw-rw---- 1 root dialout 188, 0 ... /dev/ttyUSB0
```

## Step 4 — Linux permissions (if running Z2M outside Docker)

If you'll run Z2M in **Docker** (the recommended path), you can skip this step — the Docker container runs as root inside its namespace and reaches the device through the `devices:` mapping in `docker-compose.yml`. Host-side `dialout` membership doesn't matter.

If you're running Z2M directly on the host (not in a container), your user needs to be in the `dialout` group:

```bash
id $USER | grep dialout
```

If you don't see `dialout` in the output, add yourself:

```bash
sudo usermod -aG dialout $USER
```

Log out and back in to apply the change.

## Step 5 — does any of this run MQTT? (No — and why this matters)

A common confusion at this point is "I plugged in the dongle, where is the MQTT?"

The answer: **the dongle doesn't speak MQTT.** It has no IP stack, no Wi-Fi, no Ethernet, no operating system. It's a Zigbee radio with firmware, communicating with your machine over USB serial using a binary protocol called EZSP. That's all.

MQTT runs in the Zigbee2MQTT software you'll install next. The full data flow looks like this:

```
Zigbee bulb / sensor  →  [Zigbee 2.4 GHz radio]
                              ↓
                          Sonoff ZBDongle-E (radio + EZSP firmware, USB)
                              ↓
                          /dev/ttyUSB0 (serial)
                              ↓
                          Zigbee2MQTT (Docker container on your host)
                              ↓
                          MQTT (TCP/TLS)
                              ↓
                          Chirp
```

The dongle's only job is translating between the Zigbee radio signal and the EZSP serial commands Z2M understands. All the intelligence — device identification, pairing, friendly names, MQTT publishing — lives in Z2M.

Practical implication: if you stop the Z2M container, MQTT stops. The dongle's LED stays on (it's still running) but nothing reaches Chirp. The dongle is passive hardware; Z2M is the active link.

## Step 6 — what about firmware?

The ZBDongle-E ships from the factory with Zigbee coordinator firmware pre-installed. **You do not need to flash it** before use. Firmware updates are only needed for specific known bugs in old versions, which you're unlikely to hit with a freshly-purchased dongle.

If you're curious what firmware version your dongle is running, you'll see it in the Z2M startup logs once Z2M is installed:

```
z2m: Coordinator firmware version: ... type EZSP v13
```

`EZSP v13` confirms the chip is an EFR32MG family (matches `adapter: ezsp` in `configuration.yaml`). The build number (e.g. `7.4.5.0 build 0`) is the actual firmware version.

## What's next

The dongle is plugged in, detected, and ready. Time to install the software.

Continue to [Setting up Zigbee2MQTT](../../connectors/mqtt/zigbee2mqtt.md) for the Docker Compose setup, `configuration.yaml` template, and first-publish verification. The page is generic across coordinators — when it asks for `serial.adapter:` and `serial.port:`, use:

```yaml
serial:
  port: /dev/ttyUSB0
  adapter: ezsp
```

After Z2M is running and your first device is paired, the [Paulmann 50064 walkthrough](../../devices/tested-device-guides/zigbee/paulmann-50064-light-bulb.md) covers a tested end-device pairing flow if you have that specific bulb. For other devices, follow the manufacturer's pairing instructions — once Z2M sees the device, registering it in Chirp is the same regardless of make or model.
