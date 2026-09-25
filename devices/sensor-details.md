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

## Swap between an emulator and hardware

**Swap connection** is available when there is an eligible connection involving the emulator: emulator to real hardware, or real hardware to emulator. It is not a physical-to-physical replacement control.

1. Open **Connection** and click **Swap connection**. The connection picker shows eligible destinations and unlocks the target identity fields.
2. Choose the destination, fill its required configuration, and review mappings and commands for the new source.
3. Click **Save** to apply the swap. **Cancel swap** exits swap editing before saving and restores the original connection fields.
4. Confirm the new source supplies the expected readings. Keep the retained measurement identities; generated readings and real readings both remain subject to the history retention period.

For one physical sensor replacing another, use **Detach physical device**, bind the replacement and restore its key mappings. Detach takes effect immediately; it does not wait for the page's Save button. It removes the physical binding and source mappings while retaining the twin and its measurement channels.

## The tabs

### Device info

This is where you manage the sensor's identity:

- **Photos** — Add or change photos of the sensor. This is handy when you have several similar-looking sensors and need to tell them apart during a battery change or troubleshooting.
- **Device name** — Update the name anytime. If you originally called it "Sensor 3," now's a good time to rename it to something more useful like "Kitchen Temperature" or "Basement Humidity."
- **Application** — Select the home setup this device belongs to, or **Default** to leave it outside a named application.


**Photo controls:** Use **Add photo** or drag PNG/JPG files onto the upload area. You can keep up to three photos; the UI recommends 5 MB per photo. The first photo is the cover. Use the remove control on a photo to remove it from the edited list, then save. The name is required; **Application** assigns the twin to a named setup, or **Default** leaves it outside a named application. Save profile changes before leaving the page.

### Connection

This tab shows how the sensor connects to Chirp and lets you adjust its profile. It also carries the sensor's connection diagnostics, which tell you whether data is arriving and being saved — the place to look when a sensor is quiet or a reading is missing. See [Connection Diagnostics](connection-diagnostics.md).

**For LoRaWAN sensors:** Follow [LoRaWAN Devices](lorawan-devices.md) for every identity, profile, codec and interval field. Detach before changing a bound physical identifier; keep the twin and its measurement rows, then restore the source mappings.

### Mapping {#metrics}

The **Mapping** tab connects incoming data keys to retained measurement channels. Use the same measurement rows when a sensor is replaced: changing an incoming key is different from replacing the measurement itself.

| Column or control | Purpose and configuration |
| --- | --- |
| **Device data key** | Select a received source field, such as `temperature` or `vibration.rms`. This is the incoming connector key. Options appear after messages arrive; a blank choice records nothing for this measurement. Save changes to this key with **Save**. |
| **Value** | Latest received value for the selected source key. This snapshot is not the historical record. |
| **Last update** | When that source key was last received. An empty value means no corresponding received value is available. |
| **Normalized key** | Choose the metric template defining the measurement. Only Telemetry templates are offered. A template already assigned to this device is disabled in the dropdown. |
| **Unit** | The template's unit, shown for reference. Set or change it in [metric templates](data-templates.md); the mapping does not perform unit conversion. |
| **Type** | Read-only template value type: Integer, Float, String or Boolean. It controls conversion of incoming readings. |
| **Data type** | Telemetry in this mapping form. Reported switch states can be recorded as telemetry too. |
| **Add key** | Add a mapping row, then select a template and an incoming key. |
| **+ Add new metric** | Opens **Add Metric** from the Normalized key dropdown. Enter a non-empty **Normalized key**, choose **Type** (initially String), and keep **Data type** as Telemetry. **Add** creates the template and selects it; **Cancel** closes without creating it. This compact dialog has no unit selector; use the full metric catalog to configure units. |
| **Remove** | Removes the row and its measurement assignment immediately on a saved device. This is not the procedure for changing hardware. |

Selecting a template adds its measurement immediately on an existing device. Selecting a different template on an existing row removes the old measurement assignment and creates the new one. Closing the page without clicking Save does not undo those actions. Preserve templates during replacement and change only source-key assignments, then save.

After saving mappings, allow a fresh message and check **Logs**. A field can appear in the incoming snapshot before its mapping is complete; older messages are not backfilled. Match template types to the actual values: `"ON"` and `"OFF"` are strings, while `true` and `false` are booleans. See [metric templates](data-templates.md) for conversion and rejection rules.

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

**Date filtering:** Click the date button in the top-right corner to pick a time range — useful for investigating when something happened. Choose a preset like "Last week" or set a custom date range.

If the Logs tab is empty and you're not sure why, the Connection tab's diagnostics will tell you whether anything is reaching Chirp in the first place. See [Connection Diagnostics](connection-diagnostics.md).

The date button shows the current preset or date range. Choose a quick range or a custom start/end range and click **Apply changes**. **Clear filter** resets the selection. Available dates and presets are limited by your plan's retention. **Timestamp** identifies each reading; **Key** is the normalized measurement name, followed by **Type** and **Value**. Expand/collapse the minute groups to inspect individual readings. **No logs found** means no retained readings match the range; check mapping and a fresh message before widening it. If loading fails, reload the page.

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

## Protocol setup references

Use [LoRaWAN Devices](lorawan-devices.md) or [MQTT Devices](mqtt-devices.md) for the complete connection fields, then return here for common profile, mapping and history controls.
