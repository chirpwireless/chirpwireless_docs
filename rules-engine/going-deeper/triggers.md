---
description: Only get alerted when something has been going on for a while, and cover every door or window in your home with one automation instead of one each.
---

# Triggers — "only if it's still happening"

Most automations react to a single reading. The sensor says something, the automation runs. That is exactly right for a leak — water on the basement floor is worth knowing about the same second it appears.

But a lot of what happens in a house is only worth telling you about if it **keeps** happening.

A trigger is how you say that. It watches for a situation and waits to see whether it lasts, and only then starts your automation. It also lets one automation look after a whole set of sensors at once, instead of you building the same thing over and over.

## The alerts you turn off

Think about a motion sensor by the side gate.

If it alerts on every movement, it alerts on the neighbour's cat, on a delivery driver turning around, on you taking the bins out, and on a branch moving in the wind. Within about a week you stop reading the notifications. And then, on the evening it matters, you stop reading that one too.

Now say it differently: **tell me if there's someone by the side gate and they're still there ten minutes later.** Cats leave. Delivery drivers leave. You leave. Somebody who is still standing there after ten minutes is worth a look.

Same sensor, same readings — the waiting is what turns a noisy sensor into a useful one.

It works the same way all over the house:

- The freezer door open for **thirty seconds** is you getting the peas out. Open for **ten minutes** means it has not shut properly, and dinner is defrosting.
- The bathroom humid for **half an hour** is somebody's shower. Humid **all day** means it is not clearing, and that is how you get mould.
- The garage door open **for a few minutes** is normal. Open **all night** is not.

None of those need a cleverer sensor. They need you to be able to say *"and it stayed that way."*

## One automation instead of nine

The other thing triggers fix is repetition.

Say you want to know about any window left open when the heating is on. If you have nine window sensors, you used to need nine automations — nine copies of the same idea, and nine places to go if you change your mind about the timing.

A trigger holds the list of sensors itself. You describe the situation once, tick the sensors it applies to, and that is the whole job. Adding a tenth window later is one more tick, not another automation.

They are still watched **separately**, which is the part that matters. The kitchen window being open has nothing to do with the landing window, each one is timed on its own, and when your automation runs it can tell you **which** window it was.

There is one handy exception. If your situation depends on a second reading as well, that reading does not have to come from each window — it can come from **one sensor speaking for all of them**. Windows open *and* the heating on: the heating is one thing, measured once, and applied to every window you are watching. What you cannot do is have it come from *some* of them; Chirp will not save that.

<figure><img src="../../.gitbook/assets/trigger-time-window.jpg" alt="The Create trigger dialog with a humidity condition and Only if it lasts set to 10 minutes"><figcaption></figcaption></figure>

## Making a trigger

Triggers have their own tab next to your automations. Open **Triggers** and click **Add trigger**.

Give it a **Name** you will recognise later — "Side gate, someone lingering", "Window left open" — because you will be picking it from a list when you build the automation.

Then there are four things to fill in.

### What should start the rule?

The situation you are watching for. You pick what the sensors report — motion, contact, humidity, temperature — then how to compare it:

- **Is** — for numbers you get **equals**, **is greater than** and **is less than**. For text or a simple yes/no, just **equals**.
- **Value** — what you are comparing against.

Two buttons let you say more. **Add check on ‹reading›** adds a second comparison against the *same* reading, for when one value needs to satisfy two things at once. **Add normalized key** brings in a different reading altogether — one of your chosen sensors has to be able to report it.

### When should it start?

This is the waiting, and it is the whole point of the page.

- **Immediately** — don't wait, start as soon as it's true. Pick this when you only wanted the grouping.
- **Only if it lasts** — it has to still be true after the time you set. Choose a number and pick **seconds**, **minutes**, **hours** or **days**.

A new trigger starts out on **Only if it lasts, 10 minutes**, since that is what most people want it for.

The shortest you can set is **10 seconds** and the longest is **30 days**. The box will let you type something shorter than ten seconds, but it will refuse to save — so if a save is not going through, check that first.

> **Make the wait longer than the gap between your sensor's reports.** Battery sensors do not report constantly — some only speak every fifteen minutes to make the battery last. If nothing new arrives during the wait, the situation just carries on counting, so you will not get a false all-clear. But a ten-minute wait on a sensor that reports every fifteen minutes is really being decided by one reading, which rather misses the point.

### Clear behavior

Normally the trigger stops the moment a reading says the situation is over — the window shuts, done.

Occasionally that is too jumpy. A motion sensor going quiet for one report does not prove everyone has gone. Turn on **Clear by a separate condition** and you can describe the all-clear separately, with **its own** wait — so it has to be properly quiet for a while before the trigger lets go.

### Devices

This is where you tick the sensors. The list only offers sensors that can actually answer the question you asked, so choose what you are measuring first — until then it will tell you to pick that first.

Once you have, you will see how many **compatible devices** you have — meaning sensors that report the thing your trigger needs — a **Search devices** box, and the sensors as little chips you click to select. **Select all** takes the lot, and **Clear selection** starts again.

You need at least one, and you can have up to 500 — counting the sensors you are watching plus any that supply a shared reading. Far more than any house needs, so you will never bump into it.

If a sensor you expected is not offered, it is because nothing on it reports the thing you asked about. Add that reading on the sensor's **Mapping** tab and it will turn up.

### Have a look before you save

At the bottom, **How this trigger will run** shows you exactly what you just built — one row per sensor, so you can see it really is watching the nine windows you meant and not every contact sensor in the house.

<figure><img src="../../.gitbook/assets/trigger-device-group.jpg" alt="The sensor picker and the How this trigger will run table, one row per selected sensor"><figcaption></figcaption></figure>

It is worth a glance every time. It is much easier to spot a mistake here than to work out later why your phone is buzzing.

## Using it in an automation

The trigger just watches. To make something happen, point an automation at it.

Open the automation, select the **Start Event** and click the little **pencil** that appears under it, then set **Start source**:

- **Sensor reading** — what you have always done: pick a sensor, run on its readings.
- **Trigger condition** — hand the job to a trigger. The sensor boxes disappear and one **Trigger condition** box takes their place.

It is one or the other, never both.

### Naming the sensor in your alert

When one automation covers nine windows, the alert needs to say which window — otherwise you are told "a window is open" and you go and check all nine.

The name of the sensor that set it off is available as `vars.device_name`, and you put it into your alarm's message yourself:

```
"Window left open: " + vars.device_name
```

There is no automatic way to do this. If you leave it out, the alert simply will not say which one.

> **One thing to watch:** `vars.value` isn't there when an automation starts from a trigger. A trigger tells you a situation *held*, not what the reading was, so there is no single number to give you. If you are converting an automation you already had, that is the line that will need changing.

## Triggers and time of day work together

The **Enable Schedule** switch on the Start Event still does its job, and putting the two together is where this gets genuinely useful:

> **Schedule** — only between 22:00 and 06:00
> **Trigger** — motion at the side gate, only if it lasts 10 minutes
> **Automation** — alert me, and say where

Someone wandering past at two in the morning: nothing. Someone who is still out there ten minutes later: one alert, and it tells you which sensor.

There is one detail worth knowing, because it is not quite what you would guess. **The trigger is not watching the clock.** It counts its ten minutes whatever the hour; the schedule is checked at the end, when the trigger has made up its mind and hands the job to your automation.

So somebody who turns up at 21:55 and is still there at 22:05 *will* wake you, even though they arrived before your night hours started — the ten minutes ran out inside the window, and that is the moment that counts. Somebody whose ten minutes run out at 06:05 will not, even though they arrived while it was still night.

That is usually what you want: something that carries on into the small hours is exactly the thing worth being told about. If you would rather the whole episode had to happen inside your hours, just set the window a little wider than the wait.
## Changing or removing one

**Editing a trigger can restart what it is watching.** If you change the situation itself, anything mid-count goes back to zero — a window that has been open eight minutes starts again. Chirp warns you first.

**Deleting one cannot be undone.** It stops watching, clears the alerts it raised, and any automation using it stops starting. Check what is pointing at it before you delete.

## Tips

- **Name it after the situation, not the sensor.** "Freezer door left open" tells you what you are picking. "Sensor 4 trigger" does not.
- **Start with a longer wait than feels right.** If a week goes by with nothing, shorten it. That is much nicer than being pestered while you tune it down.
- **Always put `vars.device_name` in a grouped alert.** An alert that says a window is open somewhere is only slightly better than no alert.
- **Group sensors that you'd react to the same way.** All the ground-floor windows belong together. The freezer does not belong with them, because you would do something completely different about it.

## See also

- [Trigger Alarms and Actions](../your-first-automation/trigger-alarms-and-actions.md) — setting up what actually happens
- [CEL for Home Automations](../reference/cel-for-home-automations.md) — writing the message that names the sensor
- [Safety and Alerting](../examples/safety-and-alerting.md) — worked examples you can adapt
