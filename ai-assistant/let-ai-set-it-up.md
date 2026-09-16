---
description: Have the Chirp AI Helper add a sensor, build an automation, or create an alert from a plain-language chat.
---

# Let the Helper Set It Up

Tell the Chirp AI Helper what you want your home to do, and let it work through the setup with you. It can add a sensor, create an alert with the right recipients, and build and switch on the automation that connects them. You can ask for changes as you go instead of starting again in another screen.

Open **AI Chat** and begin with a specific job: *“Add this sensor to the basement and alert me when its humidity reading exceeds 70%.”* Have the device's connection details ready. The helper asks for missing information, makes the configuration, and can check the resulting sensor, alert, and automation.

## How it works

When you ask the helper to set something up, it doesn't just give you instructions — it makes the change for you, then double-checks that it worked. Two simple promises keep you in charge:

* **It asks before anything important.** Removing a device or an automation, or marking an alert as handled, brings up a clear **Confirm Action** / **Cancel** prompt. It only goes ahead once you tap Confirm. Small, safe steps just happen; the big ones always wait for you.
* **It checks its own work.** After making a change, it looks again to make sure it really took, so it can tell you what's actually set up now.

## Build an automation, just by describing it

Describe which sensor should start the automation, what to check, and what should happen. The helper writes the logic and builds and deploys the rule. You can ask it to simulate readings that should and should not match, then inspect the results together.

> *“When the basement sensor reports humidity above 70%, raise an alert for me.”*
> *“Change that humidity threshold to 75% and notify my partner too.”*

The resulting automation is visible in the [Rules Engine](../rules-engine/README.md), so you can open the diagram and understand what it does. For an automation that operates equipment, add an Execute Command step in the visual editor and choose its saved device command. For a condition that must remain true over time or watch multiple devices, follow [Ask about triggers](#ask-about-triggers) below.

## Add a sensor

Tell the helper about a new device and it walks the setup with you, step by step, asking for whatever it needs along the way. For many devices that's all it takes to get readings flowing — and it'll check that data is actually arriving so you're not left wondering.

## Make a pretend sensor

Nothing arrived yet? Ask the helper for a pretend sensor and it makes one — picking a real sensor model so the readings match what you have on order, sending a test value so you can watch your alert fire, and taking the same sensor live onto your LoRaWAN connection when it finally turns up. It can move things the other way too — put one of your real sensors onto the emulator for a moment to test something.

> *"Make a pretend temperature sensor for the garage and send a reading of 2 degrees."*

See [Pretend Sensors](../devices/pretend-sensors.md).

## Prepare a dashboard

Ask the helper to create a dashboard for your garden or a folder for your upstairs rooms. It can change dashboard settings and arrange the layout of widgets already on a dashboard. Use [Adding Widgets](../dashboards/adding-widgets/README.md) to add the displays and controls and configure their sensor readings and appearance.

> *“Create a Garden dashboard where I can put soil moisture and temperature readings.”*

This gives you the place to build the view; the helper can guide you through choosing the widgets and explain the readings afterward.

## Set up an alert

Ask the helper to create an alarm definition with the message, recipients, and delivery settings you need. A responding automation raises events from that definition; configure any saved trigger separately. It can also mark an alert as resolved once you tell it the situation's handled (with a quick confirmation first).

## Ask it to turn things on

Ask it to run a saved command, such as *"turn on the lamp"*. The lamp must be connected to Chirp with an appropriate command already configured.

Ask what a device can do and it lists what that device is set up for; ask it to do one of those things and it does it, then reports the available execution status and verification result. Switch a lamp or a relay, change how often a sensor reports, adjust a setting — if it is set up on the device, the helper can run it.

When you run a command:

* **It only does things your device is already set up to do.** Those actions live on the device itself (see [Device Commands](../devices/commands/)). The helper runs them; it doesn't make up new ones.
* **It works with sensors connected to Chirp**, through a connection that supports commands, such as MQTT or Class C LoRaWAN. It is not a universal smart-home remote: a Hue bulb or a Tuya plug that lives in its own app isn't controllable from here. Bridge that gear into Chirp over MQTT — with zigbee2mqtt, for example — and it becomes an ordinary Chirp device that the helper can switch like any other.
* **It always asks first.** Something is about to physically happen in your house, so it shows you what it's about to do and waits for you to say yes.
* **Check the result.** A sleeping device might miss a message. The helper can retrieve command status; proof of a reported state depends on the command's optional [verification](../devices/commands/verification.md).

<figure><img src="../.gitbook/assets/ai-chat-commands.jpg" alt="The Chirp helper explaining which devices it can switch on and which it cannot"><figcaption></figcaption></figure>

You can still do all of this by hand, of course — the device's own page, or a [Control widget](../dashboards/adding-widgets/control-widget.md) on your dashboard for one-tap switching.

## Ask about triggers

A **trigger** is the condition Chirp watches; a **rule** is the automation that responds. You can create the trigger first, before any rule exists. The helper can walk you through it, but it cannot currently save or edit a trigger for you in chat.

Open **Rules Engine → Triggers → Add trigger** to set it up. When you want an automation to respond, select the saved trigger in its **Start Event** using **Start source → Trigger condition**, then save, build, and deploy the automation. Follow [Create a trigger](../rules-engine/going-deeper/triggers.md#create-a-trigger) for the full instructions.

## Getting good results

* **Say what you want to happen, not which buttons to press** — "remind me if the garage is left open at night" is perfect.
* **Give it the details** — rooms, times, who to notify — and it'll have fewer follow-up questions.
* **Read the confirmation** — it spells out the change before you approve it.
* **Tweak as you go** — treat the first version as a starting point you can adjust in the same chat.

## See also

* [Talking to Your Home](talking-to-your-home.md) — the asking-questions side
* [Device Commands](../devices/commands/) — control your devices directly
* [Rules engine](../rules-engine/) — build automations yourself
