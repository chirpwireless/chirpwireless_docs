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

## Set up an alert

Ask for an alert and the helper creates it — who to notify, how, and what triggers it — so you find out the moment something needs attention. It can also mark an alert as resolved once you tell it the situation's handled (with a quick confirmation first).

## The one thing it hands off

The helper sets up the *automations* that watch your home and alert you, but it doesn't operate your devices — and those automations send alerts, not commands. If you want to turn a light on right now, dim it, or change its color this instant, that's [Device Commands](../devices/commands/) — and the easiest way is a [Control widget](../dashboards/adding-widgets/control-widget.md) on your dashboard. Ask the helper to "turn on the lamp" and it'll point you to that, and happily set up any alerting around it.

## Getting good results

* **Say what you want to happen, not which buttons to press** — "remind me if the garage is left open at night" is perfect.
* **Give it the details** — rooms, times, who to notify — and it'll have fewer follow-up questions.
* **Read the confirmation** — it spells out the change before you approve it.
* **Tweak as you go** — treat the first version as a starting point you can adjust in the same chat.

## See also

* [Talking to Your Home](talking-to-your-home.md) — the asking-questions side
* [Device Commands](../devices/commands/) — control your devices directly
* [Rules engine](../rules-engine/) — build automations yourself
