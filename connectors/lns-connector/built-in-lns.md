# Built-in Network Server

Behind every LoRaWAN setup, there's a network server — the system that receives data from your gateway, authenticates your sensors, and routes readings to the right place. In traditional LoRaWAN deployments, this is a separate piece of software that you'd need to install, configure, and maintain on your own. That's a lot of work just to get a temperature reading into a dashboard.

Chirp takes care of all of this for you. The network server is built right into the platform — there's nothing extra to install, no server to manage, and no technical setup required on your end.

## What It Does

When your sensor sends a reading, here's what happens automatically:

- **Authentication** — Chirp verifies the sensor is legitimate using the encryption keys you entered during setup (the AppKey)
- **Data reception** — Your gateway picks up the sensor's radio signal and forwards it to Chirp's network server
- **Deduplication** — If multiple gateways hear the same sensor transmission (which is normal), Chirp keeps one copy and discards the duplicates
- **Delivery** — The sensor reading arrives in your dashboards, automations, and alerts — ready to use

All of this happens in the background, every time any of your sensors sends data.

## What This Means for You

- **No extra software to install** — the network server is part of Chirp, not a separate system
- **No configuration** — adding the LNS connector activates the network server for your home automatically
- **No maintenance** — updates, scaling, and reliability are all handled for you
- **Instant data flow** — once a sensor connects to your gateway, its readings appear in Chirp within moments

You can focus on choosing sensors, placing them around your home, and building the dashboards and automations you care about — without worrying about network infrastructure.

For an overview of LoRaWAN, see [What is LoRaWAN?](what-is-lorawan.md). For setting up your gateway, see [Gateways](../../gateways/).
