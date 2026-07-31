---
description: Have the Chirp AI Helper add a sensor, build an automation, or create an alert from a plain-language chat.
---

# Let the Helper Set It Up

The most useful thing about the helper isn't answering questions — it's doing the jobs you'd normally have to figure out yourself. Tell it what you want your home to do, and it sets it up.

## How it works

When you ask the helper to set something up, it doesn't just give you instructions — it makes the change for you, then double-checks that it worked. Two simple promises keep you in charge:

* **It asks before anything important.** Removing a device or an automation, or marking an alert as handled, brings up a clear **Confirm Action** / **Cancel** prompt. It only goes ahead once you tap Confirm. Small, safe steps just happen; the big ones always wait for you.
* **It checks its own work.** After making a change, it looks again to make sure it really took, so it can tell you what's actually set up now.

## Build an automation, just by describing it

This is where the helper really shines. Describe what you'd like to be warned about, and it creates the whole automation — working out the logic, testing it, and turning it on.

> *"Send me an alert if the basement humidity stays above 70% for an hour."*
> *"Let me know if the front door opens after midnight."*

The helper builds the automation, tries it against an example that *should* trigger it and one that *shouldn't* — so you can see it behaves — and then switches it on. Want to tweak it? Just say so ("make it 30 minutes", "alert my partner too") and it updates and re-saves. (Automations like these keep watch and let you know; they don't switch devices on and off — that's [Device Commands](../devices/commands/).) If you'd like to learn the automation builder yourself, see the [Rules engine](../rules-engine/).

## Add a sensor

Tell the helper about a new device and it walks the setup with you, step by step, asking for whatever it needs along the way. For many devices that's all it takes to get readings flowing — and it'll check that data is actually arriving so you're not left wondering.

## Make a pretend sensor

Nothing arrived yet? Ask the helper for a pretend sensor and it makes one — picking a real sensor model so the readings match what you have on order, sending a test value so you can watch your alert fire, and taking the same sensor live onto your LoRaWAN connection when it finally turns up. It can move things the other way too — put one of your real sensors onto the emulator for a moment to test something.

> *"Make a pretend temperature sensor for the garage and send a reading of 2 degrees."*

See [Pretend Sensors](../devices/pretend-sensors.md).

## Set up an alert

Ask for an alert and the helper creates it — who to notify, how, and what triggers it — so you find out the moment something needs attention. It can also mark an alert as resolved once you tell it the situation's handled (with a quick confirmation first).

## Ask it to turn things on

Say *"turn on the lamp"* and it will. The helper can now operate the things in your home, not just watch them.

Ask what a device can do and it lists what that device is set up for; ask it to do one of those things and it does it, then tells you whether the device actually got the message. Switch a lamp or a relay, change how often a sensor reports, adjust a setting — if it is set up on the device, the helper can run it.

Three things to know:

* **It only does things your device is already set up to do.** Those actions live on the device itself (see [Device Commands](../devices/commands/)). The helper runs them; it doesn't make up new ones.
* **It works with sensors connected to Chirp**, over LoRaWAN, MQTT or HTTP. It is not a universal smart-home remote: a Hue bulb or a Tuya plug that lives in its own app isn't controllable from here. Bridge that gear into Chirp over MQTT — with zigbee2mqtt, for example — and it becomes an ordinary Chirp device that the helper can switch like any other.
* **It always asks first.** Something is about to physically happen in your house, so it shows you what it's about to do and waits for you to say yes.
* **It tells you if it didn't work.** Messages to a device take a moment and a sleeping sensor might miss one, so it checks and reports back instead of just saying "done".

<figure><img src="../.gitbook/assets/ai-chat-commands.jpg" alt="The Chirp helper explaining which devices it can switch on and which it cannot"><figcaption></figcaption></figure>

You can still do all of this by hand, of course — the device's own page, or a [Control widget](../dashboards/adding-widgets/control-widget.md) on your dashboard for one-tap switching.

## Getting good results

* **Say what you want to happen, not which buttons to press** — "remind me if the garage is left open at night" is perfect.
* **Give it the details** — rooms, times, who to notify — and it'll have fewer follow-up questions.
* **Read the confirmation** — it spells out the change before you approve it.
* **Tweak as you go** — treat the first version as a starting point you can adjust in the same chat.

## See also

* [Talking to Your Home](talking-to-your-home.md) — the asking-questions side
* [Device Commands](../devices/commands/) — control your devices directly
* [Rules engine](../rules-engine/) — build automations yourself
