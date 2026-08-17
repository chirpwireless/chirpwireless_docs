---
description: See exactly what your sensor is reporting and in what form, and why the name Chirp shows you isn't the name inside the device's own messages.
---

# What Your Device Is Sending

Your sensor sends a very short message — a few bytes, or a small bundle of text. Something has to unpack that into readings you can actually use, and that something is the device's decoder. Everything you see afterwards, on a dashboard or in an automation, started life as one of the fields it produced.

There are two names for the same reading, and they're usually different:

* The **field name** is what comes out of the decoder — things like `t`, `socket_status`, or `humidity_pct`. That comes from whoever made the device.
* The **measurement name** is what you called it when you set the device up — *Temperature*, *Plug status*. This is the one you see everywhere else in Chirp.

Knowing which is which — and what the readings actually look like — is what saves you a puzzled ten minutes when a condition never seems to match.

## Have a look at what's arriving

Open the device and go to its **Mapping** section. There's a table there listing every field the device has sent, with:

* the **field name**, exactly as the device sends it
* what it's **saying right now**
* when it **last updated**

It's live, so it refreshes as new messages come in. This is the quickest way to answer "what does this thing report, and what does it look like?" — and it's worth a glance whenever you're about to compare a reading to something, whether that's an automation condition or a check on a command.

If a device has never sent anything, there's nothing to show yet. Wait for its next update.

## Where the decoder lives

The decoder sits in the **Code functions** box on the device's connection settings. Picking a ready-made device profile fills it in for you. Setting a device up by hand leaves it empty, and you paste in the code from the manufacturer's instructions or a community collection.

You can change it whenever you like. If readings are missing, look wrong, or the names don't match what the manufacturer describes, edit it and save — the device's next message comes through your version.

See [Adding Sensors](adding-sensors.md) for the whole setup walkthrough.

## Giving the fields proper names

Mapping is where you connect a field to a data template, so a cryptic `t` turns into *Temperature* with a unit and a type. After that, it shows up under its friendly name everywhere.

You do that from the same Mapping section — see [Adding Sensors](adding-sensors.md) for the steps, and [Data Templates](data-templates.md) if you need a template that doesn't exist yet.

A field you never map keeps arriving but has nowhere to go: it won't turn up in automations, on dashboards, or in a command check.

## Readings keep the shape they arrived in

Chirp keeps what the decoder produced, exactly as it was. If your plug reports the word `on`, the measurement holds the word `on` — not `true`, and not `1`. If it reports the number `1`, you get a number.

That matters any time you compare something:

* **In an automation**, compare a word to a word: `vars.socket_status == "on"`.
* **On a command**, what you type as the expected value has to match how the device says it — see [Making sure it worked](commands/verification.md#what-to-type-as-the-expected-value).
* **On a dashboard**, the same goes for conditions.

When a comparison never seems to match, go and read the current value in the Mapping table and write yours to match.

## When the fields aren't what you expected

**Readings are arriving but nothing shows up in automations or on dashboards.** They haven't been mapped yet. Open the Mapping section and map the ones you want.

**The names aren't the ones you were expecting.** The decoder is producing different field names than your measurements are looking for — which usually means the code was written for a different version of the device. Compare the names in the table against what you've mapped, and either fix the mapping or swap the code.

**Nothing's being decoded at all.** Check the device is actually sending, then check the code. [Connection Diagnostics](connection-diagnostics.md) shows what arrived most recently and whether anything came out of it.

## See also

* [Adding Sensors](adding-sensors.md) — Setting a device up, decoders and mapping
* [Data Templates](data-templates.md) — Friendly names, units and types
* [Connection Diagnostics](connection-diagnostics.md) — What turned up last, and whether it decoded
* [Making sure it worked](commands/verification.md) — Using a measurement to check a command
