# Your Home Gateway

Your gateway is the heart of your Chirp smart home. It's a small box — usually about the size of a paperback book — that sits in your home and listens for radio signals from your LoRaWAN and LR-FHSS sensors. When a sensor sends a reading (like a temperature update or a door-open event), the gateway picks it up and passes it along to Chirp through your home internet connection.

Think of it like a Wi-Fi router, but for sensors. Your phone connects to your router to reach the internet; your sensors connect to your gateway to reach Chirp.

## Why you need one

Without a gateway, Chirp has no way to hear from your sensors. LoRaWAN sensors don't connect directly to Wi-Fi — they use their own low-power radio protocol that can reach across your entire home (and beyond) on a single battery charge that lasts for years.

One gateway is usually enough for a typical home, apartment, or small property. LoRaWAN signals pass through walls, floors, and ceilings well, so a gateway placed centrally can often cover every room in your house plus the garden.

## Secure by design

Chirp requires gateways that use a modern, secure connection protocol. When you set up your gateway, you'll download a certificate file that keeps the connection between your gateway and Chirp encrypted and authenticated. This means only your gateway can send data to your account — nobody can eavesdrop on your sensor readings or inject fake data.

This section covers the current way to set up a gateway with Chirp. If you see options in the app that aren't related to smart home setup, those can be safely skipped.

## In this section

- [Setting Up Your Gateway](setting-up-your-gateway.md) — Register your gateway with Chirp and get it connected in minutes.
- [Checking Gateway Health](checking-gateway-health.md) — See if your gateway is online, how long it's been running, and how much data it's handling.
- [Compatible Gateways](compatible-gateways.md) — What to look for when choosing a gateway for your home.
