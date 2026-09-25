---
description: Replace a car tracker or home sensor while keeping its digital device, reconnect measurements, and review retained readings.
---

# Sensor Details

The detail view belongs to your device's digital twin: the lasting record of your car, home sensor, or controllable device. It brings together its name, connection, measurements, and retained readings. You can change the hardware supplying those readings without creating another digital device. See [Sensors](README.md) for an introduction to the digital twin concept.

## Opening sensor details

There are several ways to open a sensor's details:

- **From Devices** — Click **Devices** in the sidebar, then click any sensor row to open its detail page.
- **From a connection** — Open your LNS connection's **Connected Devices** tab, or open your Tracker connection's sensor list, and click a sensor row.
- **Edit button** — Click the pencil icon on any sensor row to jump straight into editing.

## Replace your car's tracker

Keep **Family Car** when a faulty GPS tracker is replaced. The car's record stays in Chirp; only the hardware sending its readings changes.

Before starting, have the new tracker's identifier and model ready, and make sure you can edit devices. Note which measurements are already attached, especially latitude and longitude. Their existing rows are what connect the car to its stored readings.

1. In **Devices**, open **Family Car** rather than adding a new device.
2. Open **Connection** and click the X control labelled **Detach physical device** in the Tracker settings. This disconnects the old tracker immediately. It keeps Family Car and its measurements, but clears the old source mappings.
3. Enter the replacement's **Unique ID** and select its **Device model**. Configure the physical tracker to send to **Url for GPS tracker**, using the manufacturer's setup instructions, then save the connection.
4. Open **Mapping** and reconnect the incoming fields to the existing measurements. Tracker location fields arrive as `position.latitude` and `position.longitude`; map them to the car's existing latitude and longitude rows. Reconnect speed or other readings you use, checking their units.
5. Click **Save** and wait for the tracker to send a fresh position. Check **Value** and **Last update**. [Connection Diagnostics](connection-diagnostics.md) helps if readings do not arrive.
6. Open the dashboard **Map** widget for Family Car, select **History**, and choose dates spanning the replacement. The route uses the same retained coordinate measurements from both trackers. Open the device's **Logs** tab to inspect the individual readings and timestamps. See [Tracking What Matters](../dashboards/tracking-what-matters.md).

Keep the measurement rows and change their **Connector key**. Removing a row and adding another with the same name does not reconnect the original history. Copying the digital device also creates a different record, so it is not the way to replace a tracker.

Any gap while the tracker was broken or disconnected remains a gap: Chirp can only store positions that were reported. How far back you can look depends on [your subscription's retention period](../account/subscription.md#keeping-your-data-history).

### Replacing a sensor at home

The same principle applies to **Living Room Temperature**. Open that existing device, detach the old source, and supply the replacement sensor's connection details. For LoRaWAN, the detach control is beside **Device EUI**; enter the new EUI, key, and matching profile. Reconnect the new temperature field to the existing temperature measurement and check fresh readings before relying on its automations.

## The tabs

### Device info

This is where you manage the sensor's identity:

- **Photos** — Add or change photos of the sensor. This is handy when you have several similar-looking sensors and need to tell them apart during a battery change or troubleshooting.
- **Device name** — Update the name anytime. If you originally called it "Sensor 3," now's a good time to rename it to something more useful like "Kitchen Temperature" or "Basement Humidity."
- **Application** — Select the home setup this device belongs to, or **Default** to leave it outside a named application.

### Connection

This tab shows how the sensor connects to Chirp and lets you adjust its profile. It also carries the sensor's connection diagnostics, which tell you whether data is arriving and being saved — the place to look when a sensor is quiet or a reading is missing. See [Connection Diagnostics](connection-diagnostics.md).

**For LoRaWAN sensors:**

- **Connector type** — Shows which connection this sensor uses — LNS, Tracker, MQTT or Emulator. You can switch a [pretend sensor](pretend-sensors.md) over to the real connection here when your hardware arrives (and back again if you want to test something).
- **Device EUI** — The unique identifier that links this profile to the physical sensor. This field is locked once set. If you need to change it (for example, if you're replacing a broken sensor with a new one), click the **detach** button (X icon) to unbind the physical sensor first. The digital device and its retained measurement history remain in place. Reconnect the replacement's source mappings before expecting new readings.
- **Device profile** — Switch between template-based and manual configuration. If you originally set up the sensor manually, you can switch to a template later (or vice versa).
- **Data sending interval** — Where you tell Chirp how often this sensor sends. A sensor's sending schedule is set on the sensor itself and varies by brand — sometimes preconfigured by the manufacturer, sometimes set when you install it — so enter the schedule the sensor is actually on. A daily sensor → **1 day**, a monthly one → **1 month**. The field defaults to **1 hour**, but that's only a placeholder. Connection diagnostics uses that schedule to spot overdue readings. The command screen checks last-seen time separately; see [Sending a command](commands/executing-commands.md#if-the-device-is-offline). Pick a number and a unit (minute, hour, day, week, or month).
- **Code functions** — The sensor's payload codec: the logic that decodes raw data into the named fields you see in the Mapping tab. When a device profile template is selected, this field is pre-filled with the template's codec. If your readings look wrong — missing fields, incorrect values — you can edit the code directly. For the full explanation, see [Adding Sensors](adding-sensors.md).

**For tracker devices:**

- **Unique ID** — The tracker's identifier (locked once set).
- **Device model** — The selected tracker model.
- **Url for GPS tracker** — The endpoint your tracker sends data to. You can copy this again if you need to reconfigure the tracker.

### Mapping {#metrics}

This tab shows what the sensor measures and how each measurement is mapped to a data template.

**Table columns:** Metrics template, Unit, Type, Data type, Connector key, Value, Last update.

Here's what each column means:

- **Metrics template** — The data template assigned to this measurement. Select from the dropdown to change it.
- **Connector key** — The raw name the sensor uses for this reading (e.g., `temp_c`). Map it to the right template so Chirp knows what the number means.
- **Value** — The most recent reading for this measurement.
- **Last update** — When the last reading came in.

You can add new measurement rows or remove existing ones. Adding or removing a template row takes effect immediately. Choosing another template on a row also replaces its measurement assignment, so avoid that when you want to retain its history. Changes to **Connector key** take effect when you click **Save**.

### Keep the asset recognizable

Name the device for what you follow, such as **Family Car**, and use its photo to distinguish it from similar devices. Keep installation notes and service records separately; the measurement history records readings rather than a diary of maintenance.

### Commands & States

For a saved MQTT or LoRaWAN connection, this tab lets you define and run actions. A pretend sensor offers it when **Support commands** is on. Tracker connections do not offer commands. See [Controlling Your Devices](commands/README.md).

### Logs

The Logs tab shows stored readings for this digital device's attached measurements, within your retention period. Keeping those measurements lets you review readings supplied by both the old hardware and its replacement. Readings are grouped by the minute. A little status indicator in the sensor's header shows its live connection, so you can see at a glance whether it's sending data right now.

Click a minute to expand it and see the individual readings:

| Column | What it shows |
|--------|---------------|
| **Key** | The normalized name of the measurement |
| **Type** | The data type of the value |
| **Value** | The actual reading |
| **Status** | Processing status (currently empty for standard readings) |

**Date filtering:** Click the date button in the top-right corner to pick a time range — useful for investigating when something happened. Choose a preset like "Last week" or set a custom date range.

If the Logs tab is empty and you're not sure why, the Connection tab's diagnostics will tell you whether anything is reaching Chirp in the first place. See [Connection Diagnostics](connection-diagnostics.md).

## Quick actions from sensor lists

You don't always need to open the full detail view. From any sensor list, the row action buttons let you:

- **Edit** (pencil icon) — Open the full detail page
- **Copy** (clone icon) — Create a new sensor pre-filled with the same settings
- **Delete** (trash icon) — Remove the sensor (with a confirmation dialog)

For more about what your sensors measure and how to customize it, see [Data Templates](data-templates.md). For room-based naming and dashboard organization, see [Rooms](rooms.md).

A physical-device copy starts new measurement rows: open it after saving and reconnect its **Connector keys**. An emulator copy carries its generated readings and reporting settings; give it a new Device ID.

For a replacement, use the existing device instead of **Copy**. Copy is for adding a separate device; its similar name and settings do not make it the same digital twin.

## Keep a home setup together

The **Application** field on **Device Info** lets you put this sensor into a setup such as Home Watch. Select the application and save, or choose **Default** to keep the sensor ungrouped. [Organizing Content](../applications/organizing-content.md) explains how the dashboard, rule, and alarm definition join it.
