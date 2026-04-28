# Changelog

<details>

<summary>Flight Log. Release 3.1.0</summary>

<figure><img src="../.gitbook/assets/Flight_Release_3.1.0.png" alt=""><figcaption></figcaption></figure>

Chirp 3.1.0 is the platform's largest connectivity expansion to date. MQTT support means a much wider range of MQTT-capable sensors, bridges, and home hardware can now connect to Chirp directly — opening access to thousands of device models across hundreds of manufacturers. This release also introduces live tracker maps with route history, scoped API keys for home automation integrations, a refreshed subscription structure, and sharper alert controls. [app.chirpwireless.io](https://app.chirpwireless.io)

***

#### What's in This Release

* **MQTT Connector** — Cloud MQTT and External MQTT open Chirp to a much wider range of MQTT-capable devices: thousands of supported models across hundreds of manufacturers
* **Map Widget** — Live tracker position on a dashboard map, plus one selected transmitted metric and historical route playback
* **API Keys** — Scoped access keys for home automation scripts, local tools, and trusted integrations — with create, rotate, and revoke lifecycle
* **Subscription Plans** — Refreshed tiers — Free, Light, Pro, Max — with a Business path for larger deployments
* **Alert Improvements** — Required Notify recipients in escalation steps, clearer one-time notification behavior by severity, and last-trigger timestamps in the alert inbox

***

**MQTT Connector**

<figure><img src="../.gitbook/assets/mqtt-connector-type-selector.jpg" alt="Add connector dialog showing External MQTT and Cloud MQTT options"><figcaption></figcaption></figure>

MQTT is one of the most widely used protocols in the world of home sensors, hubs, and connected hardware. With Cloud MQTT and External MQTT now available in Chirp, the platform can connect to a much wider range of devices than before — from ESP32 DIY projects to Tasmota devices to popular automation bridges. For Zigbee devices, Zigbee2MQTT can act as the bridge that publishes their readings into Chirp — opening access to thousands of supported Zigbee device models from hundreds of manufacturers.

The Chirp-compatible device ecosystem grew significantly with 3.1.0.

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

<figure><img src="../.gitbook/assets/map-widget-configuration.jpg" alt="Map widget configuration showing device and metric selection"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/map-widget-route-history.jpg" alt="Map widget showing historical route playback on the dashboard"><figcaption></figcaption></figure>

Did you know that Chirp goes beyond your house walls? Connect a car tracker, motorcycle tracker, or any GPS device and the Map widget shows you exactly where it is — live on your dashboard. Choose one metric the tracker is transmitting, like vehicle speed, and that reading appears right alongside the map marker. Want to see where the car went today? Historical route playback lets you replay the full route.

Any tracker device registered in Chirp can appear on the map. The widget fits into the same dashboard layout as everything else — resize it, organize it in folders, share it with your household.

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
