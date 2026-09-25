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

A **LoRaWAN** sensor uses **Code functions** on its **Connection** tab. Choosing a device profile fills in its codec; manual setup needs a compatible codec from the manufacturer. If you change it, save and check a new message.

**MQTT** devices use their message-format and field-extraction settings instead. A tracker gets its fields from the tracking integration, while a pretend sensor uses the keys you configured. Those sources do not use the LoRaWAN Code functions box.

See [Adding Sensors](adding-sensors.md) for the setup that fits your connection.

## Giving the fields proper names

Mapping is where you connect a field to a data template, so a cryptic `t` turns into *Temperature* with a unit and a type. After that, it shows up under its friendly name everywhere.

You do that from the same Mapping section — see [Adding Sensors](adding-sensors.md) for the steps, and [Data Templates](data-templates.md) if you need a template that doesn't exist yet.

A field you never map keeps arriving but has nowhere to go: it won't turn up in automations, on dashboards, or in a command check.

## Match the reading to its type {#readings-keep-the-shape-they-arrived-in}

The incoming field and the stored measurement can have different types. Chirp uses the **Type** chosen in your data template when saving readings:

- **Float** accepts numbers and numeric text: `"19.5"` becomes the number `19.5`.
- **Integer** accepts numeric values but removes their fractional part toward zero. A reading of `19.5` becomes `19`, with a warning in diagnostics.
- **Boolean** accepts true/false, text `true`/`false`, and `0` or `1` as numbers or text. It does not translate words such as `ON`, `OFF`, or `yes` into Boolean values.
- **String** keeps text and turns other values into text.

If a value cannot be converted to its chosen type, it is not saved for that measurement. For a lamp reporting `ON` and `OFF`, choose String. For temperatures or car coordinates with decimals, use Float.

Look at **Logs** to check what was stored and **Connection** diagnostics to investigate rejected values. Write automation conditions and [command checks](commands/verification.md#what-to-type-as-the-expected-value) using that stored type. Adding a unit label does not convert the number into another unit.

## When the fields aren't what you expected

**Readings are arriving but nothing shows up in automations or on dashboards.** They haven't been mapped yet. Open the Mapping section and map the ones you want.

**The names aren't the ones you were expecting.** The decoder is producing different field names than your measurements are looking for — which usually means the code was written for a different version of the device. Compare the names in the table against what you've mapped, and either fix the mapping or swap the code.

**Nothing's being decoded at all.** Check the device is actually sending, then check the code. [Connection Diagnostics](connection-diagnostics.md) shows what arrived most recently and whether anything came out of it.

## When a replacement sends different fields

A new tracker or sensor may use different field names from the old one. The connector keys table shows what the current hardware reports. Map those fields to the digital device's existing measurements to keep their history together.

For Family Car, reconnect the tracker fields `position.latitude` and `position.longitude` to the existing coordinate measurements. Check units for other values such as speed. The **Logs** tab shows stored measurement readings; the current payload table shows what is arriving now. See [Sensor Details](sensor-details.md#replace-your-cars-tracker).

## See also

* [Adding Sensors](adding-sensors.md) — Setting a device up, decoders and mapping
* [Data Templates](data-templates.md) — Friendly names, units and types
* [Connection Diagnostics](connection-diagnostics.md) — What turned up last, and whether it decoded
* [Making sure it worked](commands/verification.md) — Using a measurement to check a command
