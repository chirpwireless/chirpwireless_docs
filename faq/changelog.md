# Changelog

<details>

<summary>Flight Log. Release 3.1.0</summary>

<figure><img src="../.gitbook/assets/Flight_Release_3.1.0.png" alt=""><figcaption></figcaption></figure>

Chirp 3.1.0 is the platform's largest connectivity expansion to date. MQTT support means any MQTT-capable sensor, hub, or home hardware can now send data directly into Chirp — without LoRaWAN, without special gateways, without hardware constraints. Combined with Zigbee2MQTT compatibility, that unlocks thousands of devices across hundreds of manufacturers and opens the platform to a much wider range of homes and users than was possible before. This release also introduces live tracker maps with route history, scoped API keys for home automation integrations, a refreshed subscription structure, and sharper alert controls. [chirpwireless.io](https://chirpwireless.io)

***

#### What's in This Release

* **MQTT Connector** — Cloud MQTT and External MQTT open Chirp to a much wider range of MQTT-capable devices: thousands of supported models across hundreds of manufacturers, reachable without a LoRaWAN gateway
* **Map Widget** — Live tracker position on a dashboard map, plus one selected transmitted metric and historical route playback
* **API Keys** — Scoped access keys for home automation scripts, local tools, and trusted integrations — with create, rotate, and revoke lifecycle
* **Subscription Plans** — Refreshed tiers — Free, Light, Pro, Max — with a Business path for larger deployments
* **Alert Improvements** — Required Notify recipients in escalation steps, clearer one-time notification behavior by severity, and last-trigger timestamps in the alert inbox

***

**MQTT Connector**

MQTT is the language most home sensors, hubs, and DIY hardware already speak. Until now, connecting a device to Chirp meant LoRaWAN — a specific radio technology with specific hardware requirements. With MQTT support, that changes. Any MQTT-capable device on a standard home network can now publish data directly into Chirp, without gateways or radio hardware. Combined with bridges like Zigbee2MQTT — which supports thousands of Zigbee devices from hundreds of manufacturers — this release brings a much wider range of homes and hardware into reach.

The Chirp-compatible device ecosystem grew significantly with 3.1.0. If it speaks MQTT, it can connect.

**Two ways to connect**

**Cloud MQTT** is the simpler path for most home setups. Chirp provides a ready-to-use broker endpoint with a username, password, and topic prefix. Paste the credentials into your device or bridge settings, then register the device in Chirp and map its payload keys so readings become platform metrics. No broker to install or maintain. For Zigbee2MQTT running on a Raspberry Pi or home server, Cloud MQTT is the recommended approach — configure Zigbee2MQTT to publish outward to the Chirp-hosted endpoint.

**External MQTT** connects Chirp to an MQTT broker you already operate that is reachable from the internet. Useful when you run your own cloud-hosted broker or want Chirp to join an existing MQTT setup.

**What you can connect**

* **Zigbee2MQTT bridges** — temperature and humidity sensors, motion detectors, smart plugs, door and window sensors, leak detectors, energy monitors, and many more from Aqara, IKEA, Sonoff, Philips Hue, Tuya, and other brands. Compatibility depends on Zigbee2MQTT's device support, your coordinator adapter, and the specific device model — check the [Zigbee2MQTT supported devices list](https://www.zigbee2mqtt.io/supported-devices/) before purchasing.
* **ESP32 and ESP8266 projects** — any DIY sensor or microcontroller build that publishes over MQTT
* **Tasmota-flashed smart plugs, switches, and energy monitors**
* **Environmental sensors** — soil moisture, CO2, air quality, and other hardware with MQTT firmware
* **Any device a developer or integrator builds with MQTT support**

Per-device topic routing and payload mapping work the same way for every device type — the same metric pipeline that handles LoRaWAN devices applies to MQTT devices without modification.

[→ MQTT Connector](../connectors/mqtt-connector.md)

***

**Map Widget**

The Map widget brings your tracker data onto the dashboard. Select a tracker device, choose one metric it transmits alongside location, and get a live map showing the current position with that reading displayed — plus full historical route playback so you can see everywhere the tracker has been.

Home uses that make sense with this: a GPS pet tracker showing your pet's current location and activity level. A family tracker for a teenager's bike or scooter. A car tracker with location and battery. Any tracker device registered in Chirp can appear on a map widget.

The widget fits into the same dashboard layout as everything else — resize it, organize it in folders, share it with household members.

[→ Choosing Widgets](../dashboards/choosing-widgets.md)

***

**API Keys**

Scripts, local home automation tools, and trusted integrations can now access your Chirp data with scoped API keys instead of sharing your account credentials. Each key carries exactly the permissions you choose — read-only access to sensor data, or write access to specific resources, or any combination. One key per tool means revoking one integration doesn't touch anything else.

The full key is shown exactly once at creation — copy it to a password manager immediately. After the dialog closes, only the key prefix remains visible in the table. If a key is lost or compromised, rotate it in one click and the old key stops working instantly.

Every key ever issued stays visible in the API Keys table with its status — Active, Rotated, or Revoked — so you have a complete record of what has access, what has been cycled, and what has been permanently cut off.

[→ API Keys](../settings/api-keys.md)

***

**Subscription Plans**

Chirp 3.1.0 aligns the subscription tier structure. Current plans:

| Plan | Monthly Price |
|------|--------------|
| Free | — |
| Light | €7.99 |
| Pro | €12.99 |
| Max | €19.99 |
| Business | → Switch to Kilo IoT Server |

The **Business** card in Chirp includes a **Switch to Kilo** option for setups that have grown beyond a single home — multiple locations, managing sensors for others, or commercial installations. Kilo IoT Server is a separate platform built for that scale.

[→ Subscription](../account/subscription.md)

***

**Alert Improvements**

Three targeted changes to how home alerts work:

**Required recipients** — Escalation steps now require at least one Notify recipient before an alert rule can be saved. This prevents silent chains that trigger with no one to receive them.

**One-time notification clarity** — One-time notification behavior is now described clearly per severity level, so you know exactly what to expect when an alert fires once versus repeating.

**Last trigger in the inbox** — The alert inbox now shows when each alert last triggered, making it easy to see which alerts have been active recently and which have been quiet.

[→ Set Up a Home Alert](../alarm/set-up-a-home-alert.md)

***

**What to read next**

* [MQTT Connector](../connectors/mqtt-connector.md) — Connect your devices and bridges
* [Choosing Widgets](../dashboards/choosing-widgets.md) — Add a Map widget to your dashboard
* [API Keys](../settings/api-keys.md) — Set up scoped access for scripts and integrations
* [Subscription](../account/subscription.md) — Review your current plan
* [Set Up a Home Alert](../alarm/set-up-a-home-alert.md) — Configure alerts with the latest improvements

</details>
