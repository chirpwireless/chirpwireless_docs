---
description: A Zigbee2MQTT hub — a small computer plus a coordinator — brings your Zigbee devices into Chirp.
---

# Zigbee2MQTT hubs

A Zigbee2MQTT hub is a small always-on computer in your home — a Raspberry Pi, a home server, an old laptop, an Intel NUC — running Zigbee2MQTT software and connected to a Zigbee coordinator radio (usually a USB stick). Together, the host machine, the coordinator, and Z2M form what we call a "Zigbee2MQTT hub": the gateway that brings your Zigbee devices into Chirp.

If you have Zigbee bulbs, Zigbee smart plugs, Zigbee sensors from brands like Aqara, IKEA, Sonoff, Philips Hue, or Paulmann, this is the kind of gateway you need. Once your hub is running and joined to your devices, every Zigbee message reaches Chirp through the [MQTT connector](../../connectors/mqtt-connector.md).

## What's in this sub-section

- **[Sonoff ZBDongle-E coordinator](sonoff-zbdongle-e-coordinator.md)** — Step-by-step physical setup for the specific Zigbee coordinator we tested with. If you have this exact dongle, this page covers everything from plugging it in to confirming Linux sees it.

The pages here are tested-hardware walkthroughs. If you have one of the specific coordinators below, follow the page for the detail. If you have a different supported coordinator, the [generic Zigbee2MQTT setup page](../../connectors/mqtt/zigbee2mqtt.md) covers the broader install — pair the device through Z2M, register it in Chirp, the rest is identical.

## What a Zigbee2MQTT hub actually is

Three things, working together:

1. **A host machine.** The computer Z2M runs on. Linux is the most common (Raspberry Pi, NUC, mini-PC), but macOS and Windows also work. The machine needs a USB port (for USB coordinators) or network access (for network-attached coordinators), Docker installed, and a stable always-on connection. It does not need to be powerful — a 5-year-old Raspberry Pi handles a typical home Zigbee mesh fine.
2. **A Zigbee coordinator.** A small USB or network-attached radio that speaks Zigbee. The Sonoff ZBDongle-E and ZBDongle-P are the most common starter coordinators; SMLIGHT SLZB-06 is a popular network-attached option. Any [Zigbee2MQTT-supported coordinator](https://www.zigbee2mqtt.io/guide/adapters/) works.
3. **Zigbee2MQTT itself** — the software, running in Docker on the host machine. Z2M opens the coordinator's serial port (or network connection), joins Zigbee devices, and translates their messages into MQTT publishes that Chirp consumes.

```
Zigbee bulbs, sensors  →  [Zigbee mesh]
                                ↓
                          Coordinator radio (USB or network)
                                ↓
                          Host machine running Z2M
                                ↓
                          MQTT  →  Chirp
```

The coordinator alone doesn't reach Chirp. USB coordinators (ZBDongle-E, ZBDongle-P, ConBee II, SkyConnect) have no IP stack, no Wi-Fi, no Ethernet — they're pure Zigbee radios speaking serial over USB. Network-attached coordinators (SMLIGHT SLZB-06 and similar) do have an IP interface, but only as transport between the radio and Z2M; they don't run MQTT either. In both cases, the coordinator is the Zigbee radio bridge and Z2M is what turns the Zigbee mesh into MQTT publishes. They are always two separate things working together.

## Why "hub" and not "gateway"?

Both words describe what this hardware does, but we use "hub" specifically for the Zigbee2MQTT setup to distinguish it from LoRaWAN gateways:

- A **LoRaWAN gateway** is a single integrated box that listens for sensors and forwards their data over your home internet. The hardware does the whole job.
- A **Zigbee2MQTT hub** is a host machine plus a coordinator plus software. The pieces are visible and configurable — you choose the host, you choose the coordinator, you configure Z2M.

Both connect into Chirp; they're just different shapes.

## How this differs from LoRaWAN gateways

Different radios, different range characteristics:

| | LoRaWAN gateway | Zigbee2MQTT hub |
|---|----|----|
| Protocol | LoRaWAN (LoRa physical layer) | Zigbee 3.0 |
| Range from one gateway/hub | Whole home, garden, often more | Per device hop — most rooms, ceilings/walls reduce range |
| Mesh | No (star topology — every sensor talks to the gateway directly) | Yes (devices forward for each other) |
| Hardware | Single integrated box | Host machine + coordinator + Z2M software |
| Typical battery life | Years on a single charge | Months to a year for sensors; mains-powered for bulbs and plugs |
| Best for | Whole-property coverage with battery sensors | Indoor smart home — bulbs, plugs, room sensors |

A home can run both side by side. The two networks don't interfere — they use different parts of the radio spectrum and don't share airtime.

## What's next

If you're starting from scratch and you have a Sonoff ZBDongle-E (the dongle we tested with), open the [Sonoff ZBDongle-E coordinator](sonoff-zbdongle-e-coordinator.md) page for physical setup, then the generic [Setting up Zigbee2MQTT](../../connectors/mqtt/zigbee2mqtt.md) page for the software install.

For other coordinators, head straight to the generic Z2M setup page; the procedure is identical except for the `serial.adapter` value, which depends on your coordinator's chip family.
