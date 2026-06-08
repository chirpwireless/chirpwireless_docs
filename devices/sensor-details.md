---
description: Open any sensor to view live readings, edit its settings, and browse its full data history.
---

# Sensor Details

Every sensor in Chirp has a detail view where you can see everything about it — its name, photos, connection settings, what it measures, and its complete data history. This is the same dialog you used when first adding the sensor, but now it shows live data and lets you make changes.

## Opening sensor details

There are several ways to open a sensor's details:

- **From Devices** — Click **Devices** in the sidebar, then click any sensor row to open its detail dialog.
- **From a connection** — Open your LNS connection's **Connected Devices** tab, or open your Tracker connection's sensor list, and click a sensor row.
- **Edit button** — Click the pencil icon on any sensor row to jump straight into editing.

## The four tabs

### Device info

This is where you manage the sensor's identity:

- **Photos** — Add or change photos of the sensor. This is handy when you have several similar-looking sensors and need to tell them apart during a battery change or troubleshooting.
- **Device name** — Update the name anytime. If you originally called it "Sensor 3," now's a good time to rename it to something more useful like "Kitchen Temperature" or "Basement Humidity."

### Connection

This tab shows how the sensor connects to Chirp and lets you adjust its profile.

**For LoRaWAN sensors:**

- **Connector type** — Shows which connection this sensor uses (LNS). You can switch to a different connection if needed.
- **Device EUI** — The unique identifier that links this profile to the physical sensor. This field is locked once set. If you need to change it (for example, if you're replacing a broken sensor with a new one), click the **detach** button (X icon) to unbind the physical sensor first. The profile and all its history are preserved.
- **Device profile** — Switch between template-based and manual configuration. If you originally set up the sensor manually, you can switch to a template later (or vice versa).
- **Data sending interval** — Where you tell Chirp how often this sensor sends. A sensor's sending schedule is set on the sensor itself and varies by brand — sometimes preconfigured by the manufacturer, sometimes set when you install it — so enter the schedule the sensor is actually on. A daily sensor → **1 day**, a monthly one → **1 month**. The field defaults to **1 hour**, but that's only a placeholder. If nothing arrives within the interval the sensor shows as offline; entering the right schedule keeps a healthy sensor from looking offline between reports. Pick a number and a unit (minute, hour, day, week, or month).
- **Code functions** — The sensor's payload codec: the logic that decodes raw data into the named fields you see in the Metrics tab. When a device profile template is selected, this field is pre-filled with the template's codec. If your readings look wrong — missing fields, incorrect values — you can edit the code directly. For the full explanation, see [Adding Sensors](adding-sensors.md).

**For tracker devices:**

- **Unique ID** — The tracker's identifier (locked once set).
- **Device model** — The selected tracker model.
- **Url for GPS tracker** — The endpoint your tracker sends data to. You can copy this again if you need to reconfigure the tracker.

### Metrics

This tab shows what the sensor measures and how each measurement is mapped to a data template.

**Table columns:** Metrics template, Unit, Type, Data type, Connector key, Value, Last update.

Here's what each column means:

- **Metrics template** — The data template assigned to this measurement. Select from the dropdown to change it.
- **Connector key** — The raw name the sensor uses for this reading (e.g., `temp_c`). Map it to the right template so Chirp knows what the number means.
- **Value** — The most recent reading for this measurement.
- **Last update** — When the last reading came in.

You can add new measurement rows or remove existing ones. Removing a data template row takes effect on the server immediately. Other changes are saved when you click **Save**.

Below the main metrics table, a **User Metadata** section lets you add your own notes or tags to the sensor — things like "Installed: March 2025" or "Battery type: CR2032."

### Logs

The Logs tab is your sensor's raw data diary. Every reading the sensor has sent is recorded here, grouped by timestamp.

Click a timestamp to expand it and see the individual readings:

| Column | What it shows |
|--------|---------------|
| **Key** | The raw measurement name from the sensor |
| **Type** | The data type of the value |
| **Value** | The actual reading |
| **Status** | Processing status (currently empty for standard readings) |

**Date filtering:** Click the date button in the top-right corner to pick a time range — useful for investigating when something happened. Choose a preset like "Last week" or set a custom date range.

## Quick actions from sensor lists

You don't always need to open the full detail view. From any sensor list, the row action buttons let you:

- **Edit** (pencil icon) — Open the full detail dialog
- **Copy** (clone icon) — Create a new sensor pre-filled with the same settings
- **Delete** (trash icon) — Remove the sensor (with a confirmation dialog)

For more about what your sensors measure and how to customize it, see [Data Templates](data-templates.md). To organize sensors by room, see [Rooms](rooms.md).
