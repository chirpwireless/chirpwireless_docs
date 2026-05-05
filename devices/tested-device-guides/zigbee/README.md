# Tested Zigbee devices

Zigbee end devices we have paired and registered end-to-end on Chirp through a Zigbee2MQTT hub. These pages cover the device-specific parts — pairing procedures, payload formats, behavioral quirks. The protocol-level setup (Z2M install, MQTT connector configuration, Chirp device registration flow) is the same for every Zigbee device and lives in [Setting up Zigbee2MQTT](../../../connectors/mqtt/zigbee2mqtt.md) and [Topics and device routing](../../../connectors/mqtt/topics-and-device-routing.md).

## In this section

- [Paulmann 50064 light bulb](paulmann-50064-light-bulb.md) — Tunable-white CCT bulb. Covers the 5-cycle factory-reset pattern, the full payload field set, the Mirek-scale color-temperature mapping, and the behavioral quirk where physical wall-switch toggles don't generate MQTT publishes.

## Don't have one of these?

That's the normal case. The [Zigbee2MQTT supported devices list](https://www.zigbee2mqtt.io/supported-devices/) covers thousands of devices — anything in there works with Chirp. The procedure for registering a new Zigbee device is:

1. Pair the device through Z2M, following the manufacturer's instructions for entering pairing mode.
2. Rename it in the Z2M web UI to a whitespace-free friendly name.
3. Register it in Chirp using the friendly name as the Device ID and `zigbee2mqtt/{{deviceId}}` as the Device ID Topic — the same values as for any other Z2M-bridged device.
4. Map the payload keys the device publishes to your chosen normalized metrics.

The only thing that changes between devices is step 1 (pairing varies by manufacturer) and the specific payload keys at step 4 (they differ by device class). Steps 2 and 3 are universal.

If you'd find a walkthrough for your specific hardware useful, the [Paulmann 50064 page](paulmann-50064-light-bulb.md) is a good template for what one of these looks like — the structure transfers cleanly to other devices.
