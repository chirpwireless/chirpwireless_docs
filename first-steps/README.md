# First Steps

Welcome to Chirp. This section helps you get comfortable with the platform and walks you through connecting your first sensor. The hands-on guide here uses the LoRaWAN path from unboxing to live data, while the rest of the docs explain where other connection types start differently. Every feature has its own dedicated section later in the documentation — here we're just covering the essentials to get you up and running.

## What's ahead

| Page | What you'll learn |
|---|---|
| [Finding Your Way Around](finding-your-way-around.md) | A tour of the interface — where everything is, what each section does, and how to customize your view |
| [Connect Your First Sensor](connect-your-first-sensor.md) | A hands-on LoRaWAN guide: set up your gateway, create an LNS connection, register a sensor, build a room dashboard, and create your first alarm |

## What you'll need

- A Chirp account
- A web browser on your computer, tablet, or phone
- For the hands-on guide: a LoRaWAN gateway and a sensor (like a temperature/humidity sensor) with its Device EUI and AppKey — these usually come printed on the device or its packaging

No hardware yet? The first two pages are still worth reading — they'll help you understand what Chirp can do and how it works before your sensors arrive.

## The LoRaWAN setup flow

Here's what that path looks like:

```
Sign up → Plug in your gateway → Create a connector → Register your sensor → Build a dashboard → Set up an alarm
```

Not every Chirp setup starts with a gateway. This flow is specifically for LoRaWAN sensors. Other connection types begin with the connection itself instead.

Most people have their first LoRaWAN sensor reporting data within 15 minutes. The [Connect Your First Sensor](connect-your-first-sensor.md) guide walks you through every step.

## After your first sensor

Want to connect scripts or trusted tools to Chirp? Create an API key and use the [API](../api/README.md) — REST over plain HTTPS is all most home setups need.
