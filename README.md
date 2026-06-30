---
description: Chirp is an AI-first home automation platform — connect any maker's sensors and let a built-in AI helper run the setup.
---

# Chirp — Home Automation Platform

Chirp is an **AI-first** home automation platform that connects sensors from different manufacturers into one system — with shared dashboards, unified automations, and a single alerting workflow across every device in your home. No vendor lock-in, no juggling multiple apps. And instead of hunting through settings to get any of it working, you can just *ask*: a built-in AI helper sets up sensors, builds automations, and creates alerts for you, in plain language.

Whether you're monitoring temperature in a baby's room, watching for water leaks in the basement, tracking soil moisture in the garden, or making sure the garage door closed after you left — Chirp brings it all together. Sensors from different brands, using different protocols, reporting data in different formats, all working as one.

And Chirp doesn't stop at your front door. Connect a GPS or OBD-II tracker to your car or motorcycle and get engine diagnostics, error codes, real-time location, and theft recovery — all in the same platform, the same dashboards, the same alerts. Pick up a compatible tracker (for example, from [Kilo Electronics — Teltonika trackers](https://kiloelectronics.com/en/product-brand/teltonika/)), plug it in, and your vehicle shows up alongside your home sensors within minutes.

## Why Chirp

### Just ask — your home has an expert built in

The best part of Chirp is that you don't have to be technical to use it. A built-in AI helper knows your whole home — every sensor and its history — so you can ask it anything in plain English: *"What was the bedroom temperature overnight?"* or *"Were there any motion events in the hallway after 11 PM?"* It checks your real data and answers, then draws you a chart if you'd like one.

And it doesn't stop at answers. Ask it to *do* something — "add my new leak sensor", "alert me if the basement gets damp", "let me know if a door opens after midnight" — and it sets it up for you, writing the automation, testing it, and switching it on. Before anything important or permanent, it asks you to confirm, so you're always in charge. It's like having a smart-home installer on call, who happens to live inside the app. See [Your Home AI Helper](ai-assistant/).

This is what people mean by **AIoT** — artificial intelligence built right into your connected home, not a chatbot stuck on the side. The helper keeps getting better the more it's used, and the engine behind it is something we built ourselves and were proud enough of to share openly as [Synthetic Brew](https://github.com/syntheticinc/syntheticbrew).

### Connect any manufacturer, one platform

Chirp doesn't lock you into a single brand. You can connect LoRaWAN sensors, vehicle trackers, and MQTT-capable devices from any manufacturer — including thousands of Zigbee devices through the MQTT connector. The vehicle tracker library alone covers over 2,000 preconfigured models — OBD-II dongles that read engine codes, fuel level, and battery voltage, as well as standalone GPS trackers for location and route history.

Different manufacturers report data in completely different formats — one says `temp`, another says `temperature_celsius`, a third just sends a number with no label. Chirp normalizes all of it. Every sensor in your home speaks the same language, so your dashboards, automation rules, and alerts work the same way regardless of which brand made the hardware.

If a better sensor comes along next year, just add it. Your existing rules, dashboards, and alert configurations keep working.

### Every sensor, fully modeled

When you connect a sensor, it doesn't just show you a number. Every device becomes a living digital model — its current state, full history, and patterns over time. Even when a sensor temporarily loses connection, its data and configuration are preserved. You always know what's happening at home.

### Automate with confidence

Set rules that make your home — and your vehicles — respond to what's happening. If the basement humidity goes above 70% for more than an hour, get a notification. If the front door opens after midnight, send a text to everyone in the household. If the garden soil gets too dry, know about it before your plants do. If your car's engine throws a warning code, get an alert on your phone immediately. If your motorcycle moves outside a geofence at 3 AM, trigger a critical alarm.

Rules are built visually — you pick a sensor, set a condition, choose what should happen. Behind the scenes, Chirp uses [CEL (Common Expression Language)](https://cel.dev) for conditions, giving you precise control when you want it. You can combine readings from multiple sensors — regardless of manufacturer — in a single rule, schedule rules to run only on certain days, and set conditions that need to persist for a minimum time before triggering.

That last point matters more than you'd think: a temperature sensor might briefly spike to 35 degrees if sunlight hits it for a moment, then settle back to 22. With Chirp's "remain true for" conditions, you can say *"only alert me if the temperature stays above 30 for at least 15 minutes."* Transient spikes are ignored. You only hear about real problems.

And here's something you won't find in most smart home systems: every change you make to a rule is versioned. If you adjust an automation and it starts behaving unexpectedly, you can see exactly what changed, compare with the previous version, and undo it with one click. Nothing is lost.

### Know when it matters

Chirp delivers alerts through the channels that work for you — email, text messages, or push notifications through the **Chirp Alerts** mobile app ([iPhone](https://apps.apple.com/us/app/chirp-alerts/id6756504956) / [Android](https://play.google.com/store/apps/details?id=io.chirpwireless.alarm)).

The mobile app takes alerting further: critical alerts trigger a full-screen alarm with looping sound and vibration, designed to get your attention even when your phone is locked or in silent mode. The alarm keeps going until you silence or acknowledge it. Informational alerts, on the other hand, arrive quietly — you see them when you check your notifications. For full details, see the [Chirp Alerts App](alarm/chirp-alerts-app/) section.

Set up quiet hours so non-critical notifications don't disturb you at night. Configure escalation chains so that if one person doesn't respond, the alert goes to the next. And if a notification fails to deliver for any reason, the system automatically retries.

### See your home at a glance

Build dashboards for any room, any purpose — or any vehicle. A "Kitchen" dashboard showing temperature and air quality. A "Security" dashboard with every door and window sensor. A "Garden" view tracking soil moisture and rainfall. A "My Car" dashboard with live location, engine status, and trip history. Sensors and trackers from different manufacturers show up side by side — because Chirp normalizes their data into a shared model.

Each dashboard is made of widgets you customize. Pick the display type — charts for trends, numbers for current readings, on/off indicators for states. Then fine-tune: set value boundaries so you can see at a glance when a reading is in or out of range, choose your preferred units, and toggle graph visibility. Each widget adapts to the way you want to see your data.

Your data appears on screen the moment your sensor reports it — no polling, no refresh button, no "data updated 5 minutes ago." The platform streams data through specialized channels built for real-time delivery. And when you pull up a chart of last month's humidity readings, it loads quickly even with thousands of data points.

### See your home in 3D

Build a 3D model of your home and watch your sensors come to life inside it. The Digital Building Twin lets you draw your rooms — walls, doors, windows, every floor — or import a floor plan, then furnish it from a library of more than 60 ready-made 3D objects: sofas, beds, the fridge, a parking spot in the driveway. Connect each one to a sensor and choose what its colors mean.

Then the model lights up. The nursery glows warm when the temperature climbs. The garage shows at a glance whether the door was left open. The basement turns blue the moment the leak sensor gets wet. The driveway shows whether the car is home. Your house stops being a list of readings and becomes a picture you can read in a second — and what it shows is up to you, room by room, however your home is laid out.

You can even place your home on the real-world map, anchored to its actual location. See [Digital Building Twin](dashboards/adding-widgets/digital-building-twin/README.md) for the full guide.

### Share with the people who live there

Invite family members, roommates, or property managers to your organization. Give everyone full access, or limit some members to view-only — kids can check the temperature but can't modify rules. If you're a landlord, give tenants view access to shared utility sensors without exposing your own devices or settings.

Every organization has an activity log, so you can see who changed what and when. From the user menu, go to **Users** to manage members and **Organization settings** to configure your setup.

### Connect your own tools

Prefer to wire Chirp into your own scripts or another home-automation platform? A scoped API key lets trusted tools read your sensors and history — pull readings into a spreadsheet, bridge data into another system, or build a small automation of your own. REST over plain HTTPS is all most setups need. See the [API](api/README.md) section to get started, and [API Keys](settings/api-keys.md) to create a key.

### No gateway lock-in

Chirp includes a built-in LoRaWAN Network Server, which means your gateway connects directly to the platform — no separate network server to manage, no middleware in between. You can use a variety of compatible gateways, and adding one takes just a few minutes.

## Available in your language

The interface is available in English, German, French, Spanish, and Portuguese. Switch between light and dark modes with one click, and your preferences are remembered automatically.

## Plans

Chirp offers several plan tiers to fit every home — from a free tier to get started, up to plans with more devices, unlimited automation rules, and advanced features. You can view and manage your plan from the **Subscription** section in the user menu.

## Access the Platform

Open Chirp at [app.chirpwireless.io](https://app.chirpwireless.io).

## Let's get started

Ready to connect your first sensor? Head to [First Steps](first-steps/) — we'll walk you through the interface and the standard LoRaWAN path to your first alert, while pointing out where other connection types follow a different setup order.
