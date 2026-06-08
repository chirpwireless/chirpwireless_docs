---
description: One small LoRaWAN gateway covers a whole home — learn how it works and how coverage spreads.
---

# LoRaWAN gateways

A LoRaWAN gateway is the small box that listens for radio signals from your battery-powered sensors and forwards them to Chirp. If you have door sensors, leak detectors, temperature probes, or any other LoRaWAN-based devices in your home, a gateway is what makes them visible to Chirp.

This sub-section covers everything specific to LoRaWAN gateways:

- **[Setting up a LoRaWAN gateway](setting-up-a-lorawan-gateway.md)** — Register your gateway with Chirp, download the certificate, and get it connected.
- **[Checking LoRaWAN gateway health](checking-lorawan-gateway-health.md)** — Confirm it's online, see how long it's been running, and check how much data it's handling.
- **[Compatible LoRaWAN gateways](compatible-lorawan-gateways.md)** — What to look for when choosing one.

## How LoRaWAN coverage works

One LoRaWAN gateway is usually enough for a typical home, apartment, or small property. The radios used by LoRaWAN sensors are tuned for range over throughput — they pass through walls, floors, and ceilings well, and a centrally-placed gateway can often cover every room in your house plus the garden, garage, or shed.

If you have an unusually large property, multiple separate buildings, or thick walls (stone, concrete, or basements), you may benefit from a second gateway. Chirp doesn't require you to do anything special — multiple gateways forwarding the same sensor's data simply give Chirp a stronger picture of where the sensor is reporting from.

## Secure by design

Chirp requires LoRaWAN gateways that use the Basics Station protocol, which connects over encrypted TLS/WSS. The certificate download step during gateway registration provides the TLS credentials for that secure connection. Older gateway protocols that send data unencrypted (the legacy UDP Packet Forwarder) are not supported.

In practice this means most modern indoor home gateways work fine — Compatible LoRaWAN gateways covers what to look for if you're shopping.

## How this differs from a Zigbee2MQTT hub

Zigbee2MQTT hubs are a separate kind of gateway covered in [Zigbee2MQTT hubs](../zigbee2mqtt-hubs/README.md). They're for Zigbee devices specifically — smart bulbs, smart plugs, Aqara/IKEA/Sonoff sensors. A LoRaWAN gateway and a Zigbee2MQTT hub can coexist in the same home and complement each other.
