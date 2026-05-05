# Tested device guides

These walkthroughs cover end devices we have tested end-to-end on Chirp. They are not the supported device list — Chirp's MQTT and LoRaWAN connectors work with thousands of devices across many brands, and you don't need to find your specific hardware in this section before adding it. The point of these pages is simply that **if you happen to have one of these exact devices**, the pairing procedure, configuration values, and quirks are documented here so you don't have to figure them out yourself.

For the standard registration flow that applies to any device, see [Adding Sensors](../adding-sensors.md). For Zigbee devices specifically, [Setting up Zigbee2MQTT](../../connectors/mqtt/zigbee2mqtt.md) explains the generic pairing pattern and links you to your device's manufacturer instructions.

## What's in this section

### [Zigbee devices](zigbee/README.md)

Walkthroughs for Zigbee end devices we tested through a Zigbee2MQTT hub. Currently:

- [Paulmann 50064 light bulb](zigbee/paulmann-50064-light-bulb.md) — a CCT (tunable-white) Zigbee bulb.

If you have a different Zigbee device, follow your manufacturer's pairing instructions and the [generic Z2M setup page](../../connectors/mqtt/zigbee2mqtt.md). The registration steps in Chirp are the same for every Zigbee device — the only piece that's device-specific is how the device enters pairing mode and what payload keys it publishes.

## How a tested-device walkthrough is structured

Each page covers four things:

1. **What the device is** — quick orientation, what to expect, what works and what doesn't (e.g., bulbs that don't publish on physical wall-switch toggles).
2. **The pairing procedure** — exactly what we did to get the device joined and named in Z2M. Includes specific gotchas, like reset patterns and timing.
3. **The capability profile** — every payload key the device publishes, with type, range, and what it means.
4. **Registering it in Chirp** — values to use in the device form (Device ID, Device ID Topic, mappings) and a confirmation that the readings flow into the Mapping tab.

If you want to add a device that isn't covered here, the same four-part shape applies — the manufacturer's documentation will tell you (1), (2), and (3), and the [MQTT connector documentation](../../connectors/mqtt-connector.md) covers (4) for any MQTT-bridged device.
