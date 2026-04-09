# Chirp — Smart Home, Simplified

Chirp is a home automation platform that turns wireless sensors into a connected, intelligent home. It brings together everything you need to monitor conditions, automate responses, and stay informed — all in one place, without juggling multiple apps or services.

Whether you're tracking the temperature in your baby's room, watching for a water leak in the basement, or making sure the garage door closed after you left, Chirp gives your home a voice.

## What Chirp does for your home

### Every sensor tells a story

When you connect a sensor to Chirp, it doesn't just show you a number. Every device becomes a living digital model of the real thing — its current state, its full history, and its patterns over time. Even when a sensor temporarily loses connection, its data and configuration are preserved. You always know what's happening at home.

You're not locked into one brand or one type of connection. Chirp works with LoRaWAN wireless sensors and vehicle trackers today, with MQTT device connectivity coming soon — which will open the door to Zigbee devices bridged through MQTT and a virtually unlimited range of smart home hardware.

Different manufacturers report data in completely different formats — one says `temp`, another says `temperature_celsius`, a third just sends a number with no label. Chirp normalizes all of that. When you add a device, you tell Chirp what each piece of data means — or it figures it out from known device profiles. After that, every sensor in your home reports data the same way. Your rules and dashboards don't care who manufactured the hardware.

This also means you're never locked into one brand. If a better sensor comes along next year, just add it.

### Automate with confidence

Set rules that make your home respond to what's happening. If the basement humidity goes above 70% for more than an hour, get a notification. If the front door opens after midnight, send a text to everyone in the household. If the garden soil gets too dry, know about it before your plants do.

Rules are built visually — you pick a sensor, set a condition, choose what should happen. Behind the scenes, Chirp uses [CEL (Common Expression Language)](https://cel.dev) for conditions, giving you precise control when you want it. You can combine readings from multiple sensors in a single rule, schedule rules to run only on certain days, and set conditions that need to persist for a minimum time before triggering.

That last point matters more than you'd think: a temperature sensor might briefly spike to 35 degrees if sunlight hits it for a moment, then settle back to 22. With Chirp's "remain true for" conditions, you can say *"only alert me if the temperature stays above 30 for at least 15 minutes."* Transient spikes are ignored. You only hear about real problems.

And here's something you won't find in most smart home systems: every change you make to a rule is versioned. If you adjust an automation and it starts behaving unexpectedly, you can see exactly what changed, compare with the previous version, and undo it with one click. Nothing is lost.

### Know when it matters

Chirp delivers alerts through the channels that work for you — email, text messages, or push notifications on your phone. You decide which alerts are critical (wake you up at 3 AM) and which are just informational (check when you have a moment).

Set up quiet hours so non-critical notifications don't disturb you at night. If something truly urgent happens — a water leak, a smoke detector trigger, a freezer going above temperature — the critical alert still gets through. And if a notification fails to deliver for any reason, the system automatically retries. Nothing falls through the cracks.

### See your home at a glance

Build dashboards for any room, any purpose. A "Kitchen" dashboard showing temperature and air quality. A "Security" dashboard with every door and window sensor. A "Garden" view tracking soil moisture and rainfall.

Each dashboard is made of widgets you customize. Pick the display type — charts for trends, numbers for current readings, on/off indicators for states. Then fine-tune: set value boundaries so you can see at a glance when a reading is in or out of range, choose your preferred units, and toggle graph visibility. Each widget adapts to the way you want to see your data.

Your data appears on screen the moment your sensor reports it — no polling, no refresh button, no "data updated 5 minutes ago." The platform streams data through specialized channels built for real-time delivery, so readings reach your dashboard as fast as the infrastructure allows. And when you pull up a chart of last month's humidity readings, it's designed to load quickly even with thousands of data points — the architecture uses specialized tools optimized for exactly this kind of workload.

### Share with the people who live there

Invite family members, roommates, or property managers to your organization. Give everyone full access, or limit some members to view-only — kids can check the temperature but can't modify rules. If you're a landlord, give tenants view access to shared utility sensors without exposing your own devices or settings.

Every organization has an activity log, so you can see who changed what and when. From the user menu, go to **Users** to manage members and **Organization settings** to configure your setup.

### Ask your home a question

The built-in AI helper understands your home's data. Ask in plain English: *"What was the bedroom temperature overnight?"* or *"Were there any motion events in the hallway after 11 PM?"* It checks your actual sensor history and gives you a real answer — not a canned FAQ response.

### No gateway lock-in

Chirp includes a built-in LoRaWAN Network Server, which means your gateway connects directly to the platform — no separate network server to manage, no middleware in between. You can use a variety of compatible gateways, and adding one takes just a few minutes.

## Available in your language

The interface is available in English, German, French, and Spanish. Switch between light and dark modes with one click, and your preferences are remembered automatically.

## Plans

Chirp offers several plan tiers to fit every home — from a free tier to get started, up to plans with more devices, unlimited automation rules, and advanced features. You can view and manage your plan from the **Subscription** section in the user menu.

## Let's get started

Ready to connect your first sensor? Head to [First Steps](first-steps/) — we'll walk you through the interface and the standard LoRaWAN path to your first alert, while pointing out where other connection types follow a different setup order.
