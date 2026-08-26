---
description: Tell Chirp what your sensors measure so readings appear with the right name and unit, all from one Metrics list you can search and filter.
---

# Data Templates

This is the part of Chirp that turns a raw number into something you can read.

Your sensors do not send tidy labels. One temperature sensor might send `temp_c`, another `t`, a third `temperature` — three names for the same thing. Data templates are how Chirp knows all three mean *temperature*, that it is measured in °C, and that it should be shown with a decimal point.

Most common sensors arrive already set up, so plenty of people never open this page at all. You come here when you have something unusual, or when you want a reading labelled your way.

## Where it lives

Open **Devices** and choose the **Metrics** tab.

It is all on one screen now — the list of what your sensors measure, and, inside the form, the units and names those measurements are built from.

<figure><img src="../.gitbook/assets/device-metrics.jpg" alt="The Devices Metrics list with search, unit, type and data type filters and a sort control"><figcaption></figcaption></figure>

## Finding your way around the list

The list shows everything your home measures. Once you have a few dozen sensors that is a long list, so there are a few ways to cut it down:

- **Search** — start typing and the list narrows. It looks at the measurement's proper name only, not its unit or the raw name your sensor uses.
- **All units** — show only the ones measured in a particular unit. You can search inside this one, and there is a bucket for things that have no unit at all.
- **All types** — show only one way of storing a value: String, Integer, Float or Boolean.
- **All data type** — show only one kind of measurement: Telemetry, Device metadata or Custom attributes.
- **Sort by** — **Newest** or **Oldest**, meaning when it was added. **Newest** is the quick way back to something you have just created.

You can tick several options in any of them. They behave slightly differently, though: **All types** and **All data type** take effect the moment you tick a box, while **All units** waits for you to press **Apply**.

Anything you created has **Edit** and **Delete** on its row. **The ones that came with Chirp do not** — they are shared, so they are not yours to change.

## Adding something new

Press **Add metric** at the top of the page. The same form is used for adding and editing, so there is only one set of boxes to learn.

There are four boxes, in this order.

<figure><img src="../.gitbook/assets/device-metrics-add.jpg" alt="The Add Metric dialog with Data type, Type, Normalized key and Unit of measurement"><figcaption></figcaption></figure>

### Data type

What sort of thing this is:

| Data type | Meaning |
|---|---|
| **Telemetry** | A normal reading that changes as the day goes on — temperature, humidity, battery. Nearly everything is this. |
| **Device metadata** | Facts the sensor reports about itself and hardly ever changes, like its firmware version. |
| **Custom attributes** | Notes you add yourself that no sensor sends — when you installed it, which room you bought it for, when it next needs a battery. |

That last pair are kept out of the lists you see when mapping what a sensor sends, which is exactly right: a sensor cannot report a note you wrote.

### Type

How the value itself is stored:

| Type | For |
|---|---|
| **Float** | Anything with a decimal point — 22.5 °C, 67.3 % |
| **Integer** | Whole numbers — battery 85, signal −120 |
| **String** | Words — `"open"`, `"standby"` |
| **Boolean** | Yes or no — motion detected, or not |

> **This decides whether you can put it on a dashboard.** The dial and gauge widgets need an actual number to fill against. If a reading is stored as words or as yes/no, it will not turn up when you go looking for it in a widget. If something you expected is missing from a widget's list, come back here and check the **Type** — assuming, of course, that the sensor really does send a number.

### Normalized key

The proper name for what is being measured, regardless of what your sensor calls it internally.

Open the box and either pick one that already exists or choose **Create a new normalized key** and type it. **This box is also where you rename or remove keys** — there is no separate screen for them any more, and the unit box below works the same way.

One thing to know about both: **the names and units that came with Chirp cannot be renamed or removed.** They are shared, so those buttons do nothing on them. The ones you made yourself are fine to change.

Name the thing being measured, not the gadget measuring it: `soil_moisture` reads much better than `sensor_3_value` when you meet it again in six months. Lowercase with underscores is the house style.

Each name gets used once. Pick one that is already taken and the form will tell you.

### Unit of measurement

What gets shown next to the number — °C, %, lux, mV.

Same as above: pick an existing one, or choose **Create a new unit** and type the symbol. **Whatever symbol you type becomes the unit**, so write it exactly as you want to see it on your dashboard.

**Whether you have to fill it in depends on the Data type above.** A **Telemetry** reading needs a unit — a number on your dashboard with nothing beside it is anyone's guess. **Device metadata** and **Custom attributes** can be left blank, and usually should be: a firmware version or a note about which room a sensor is in has no unit, and inventing one just adds clutter.

Press **Add** to save it, or **Cancel** to back out.

## Editing — worth reading the warning

Here is the thing to understand: **these are shared across your whole home, not set per sensor.** Every sensor using a measurement uses the same definition of it.

So changing one is not a small local edit. Chirp asks you to confirm, and the confirmation spells out what happens: every sensor using it updates to match.

That is perfect when you are fixing a unit everywhere at once. It is not what you want if you meant to change one sensor. **If it is just the one, make a new metric and point that sensor at it instead** — leave the shared one alone.

## Deleting

Deleting asks first too.

If anything is still using it, Chirp will not delete it, and says so — it is *used in other devices*. Unhook it from the sensors using it, then delete. Nothing gets pulled out from under a sensor that still depends on it.

## See also

- [Adding Sensors](adding-sensors.md) — pointing a new sensor at these measurements
- [What Your Device Is Sending](what-your-device-is-sending.md) — matching raw readings to the right name
- [Sensor Details](sensor-details.md) — the per-sensor Metrics tab
