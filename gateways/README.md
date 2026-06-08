---
description: Gateways bring your sensors into Chirp — choose between a LoRaWAN gateway and a Zigbee2MQTT hub.
---

# Gateways

Gateways are the connectivity hardware that brings sensors and end devices into Chirp. Different protocols use different kinds of gateways, but they share the same role: they sit in your home, listen for the radios your sensors use, and forward what they hear to Chirp.

Chirp supports two categories of gateway today, organized in this section by the protocol they handle:

## In this section

### [LoRaWAN gateways](lorawan-gateways/README.md)

The original Chirp gateway category. A small box — usually about the size of a paperback book — that listens for LoRaWAN radio signals from sensors anywhere in your home. One gateway is typically enough for a house or apartment; LoRaWAN signals reach far on tiny amounts of power, and a battery-powered sensor can last years on one charge.

- [Setting up a LoRaWAN gateway](lorawan-gateways/setting-up-a-lorawan-gateway.md)
- [Checking LoRaWAN gateway health](lorawan-gateways/checking-lorawan-gateway-health.md)
- [Compatible LoRaWAN gateways](lorawan-gateways/compatible-lorawan-gateways.md)

### [Zigbee2MQTT hubs](zigbee2mqtt-hubs/README.md)

A different kind of "gateway" for Zigbee devices: a small computer (a Raspberry Pi, a home server, an old laptop) running Zigbee2MQTT software, with a USB or network-attached Zigbee coordinator. Together, the host machine plus the coordinator plus Z2M form what we call a "Zigbee2MQTT hub" — it joins your Zigbee devices into a mesh and publishes their data to MQTT, which Chirp then ingests through the [MQTT connector](../connectors/mqtt-connector.md).

- [Sonoff ZBDongle-E coordinator](zigbee2mqtt-hubs/sonoff-zbdongle-e-coordinator.md) — the specific coordinator we tested with. Other Zigbee2MQTT-supported coordinators follow the same pattern.

## Which kind do I need?

It depends on the sensors and devices you want to connect:

- **LoRaWAN sensors** — long-battery-life devices designed for whole-home or whole-property coverage. A LoRaWAN gateway is the right kind.
- **Zigbee devices** — typically smart bulbs, smart plugs, and battery sensors from brands like Aqara, IKEA, Sonoff, Philips Hue, Paulmann. A Zigbee2MQTT hub is the right kind.
- **Both** — many homes run both. A LoRaWAN gateway and a Zigbee2MQTT hub coexist without conflict; they listen on different radios.

If you're not sure what your sensor uses, check the manufacturer's listing or the product packaging — it's almost always stated clearly.

## Secure by design

Both kinds of gateway connect to Chirp over encrypted channels:

- LoRaWAN gateways download a certificate file during setup that keeps the connection encrypted and authenticated. Only your registered gateway can send data to your account.
- Zigbee2MQTT hubs use TLS-protected MQTT (`mqtts://` on port 1884) to publish to Chirp's managed broker, with credentials unique to your connector.

In both cases, nobody on the public internet can eavesdrop on your sensor readings or inject fake data — the channel is encrypted and the credentials are yours alone.
