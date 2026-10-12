---
description: Replace a car tracker or home sensor while keeping its digital device, reconnect measurements, and review retained readings.
---

# What do I see on a sensor's details page?
The detail view belongs to your device's digital twin: the lasting record of your car, home sensor, or controllable device. It brings together its name, connection, measurements, and retained readings. You can change the hardware supplying those readings without creating another digital device. See [Sensors](README.md) for an introduction to the digital twin concept.

## How do I open a sensor's details?
There are several ways to open a sensor's details:

- **From Devices** — Click **Devices** in the sidebar, then click any sensor row to open its detail page.
- **From a connection** — Open your LNS connection's **Connected Devices** tab, or open your Tracker connection's sensor list, and click a sensor row.
- **Edit button** — Click the pencil icon on any sensor row to jump straight into editing.

## How do I replace my car's tracker?
Keep **Family Car** when a faulty GPS tracker is replaced. The car's record stays in Chirp; only the hardware sending its readings changes.

Before starting, have the new tracker's identifier and model ready, and make sure you can edit devices. Note which measurements are already attached, especially latitude and longitude. Their existing rows are what connect the car to its stored readings.

1. In **Devices**, open **Family Car** rather than adding a new device.
2. Open **Connection** and click the X control labeled **Detach physical device** in the Tracker settings. This disconnects the old tracker immediately. It keeps Family Car and its measurements, but clears the old source mappings.
3. Enter the replacement's **Unique ID** and select its **Device model**. Configure the physical tracker to send to **Url for GPS tracker**, using the manufacturer's setup instructions, then save the connection.
4. Open **Mapping** and reconnect the incoming fields to the existing measurements. Tracker location fields arrive as `position.latitude` and `position.longitude`; map them to the car's existing latitude and longitude rows. Reconnect speed or other readings you use, checking their units.
5. Click **Save** and wait for the tracker to send a fresh position. Check **Value** and **Last update**. [Connection Diagnostics](connection-diagnostics.md) helps if readings do not arrive.
6. Open the dashboard **Map** widget for Family Car, select **History**, and choose dates spanning the replacement. The route uses the same retained coordinate measurements from both trackers. Open the device's **Logs** tab to inspect the individual readings and timestamps. See [Tracking What Matters](../dashboards/tracking-what-matters.md).

Keep the measurement rows and change their **Device data key**. Removing a row and adding another with the same name does not reconnect the original history. Copying the digital device also creates a different record, so it is not the way to replace a tracker.

Any gap while the tracker was broken or disconnected remains a gap: Chirp can only store positions that were reported. How far back you can look depends on [your subscription's retention period](../account/subscription.md#keeping-your-data-history).

### Replacing a sensor at home

The same principle applies to **Living Room Temperature**. Open that existing device, detach the old source, and supply the replacement sensor's connection details. For LoRaWAN, the detach control is beside **Device EUI**; enter the new EUI, key, and matching profile. Reconnect the new temperature field to the existing temperature measurement and check fresh readings before relying on its automations.

## How do I swap between an emulator and hardware?
**Swap connection** exists for one job: moving a device between a practice sensor (the emulator) and real hardware, in either direction. It does not handle swapping one physical sensor for another.

1. Open **Connection** and click **Swap connection**. A picker lists the destinations you can move to, and the identity fields for the new source become editable.
2. Pick where the device is going, enter whatever that connection asks for, then look over the mappings and commands, because they now come from a different source.
3. Click **Save** to make the swap real. Changed your mind first? **Cancel swap** closes swap editing and puts the original connection fields back.
4. Wait for a reading and check that the new source sends what you expect. The measurements keep their identities through the swap, and both generated and real readings count toward your history retention period.

Replacing one physical sensor with another is a different job: click **Detach physical device**, attach the new sensor, and restore its key mappings. Detaching happens the moment you click it, without waiting for **Save**. The physical binding and the source mappings go, while the digital device and its measurement channels stay.

## What do the sensor detail tabs show?
### Device info

This is where you manage the sensor's identity:

- **Photos** — Add or change photos of the sensor. This is handy when you have several similar-looking sensors and need to tell them apart during a battery change or troubleshooting.
- **Device name** — Update the name anytime. If you originally called it "Sensor 3," now's a good time to rename it to something more useful like "Kitchen Temperature" or "Basement Humidity."
- **Application** — Select the home setup this device belongs to, or **Default** to leave it outside a named application.


**Photos:** click **Add photo**, or drop PNG or JPG files onto the upload area. Chirp keeps up to three per device and suggests staying near 5 MB each. The first one becomes the cover. To drop a photo, use the remove control on it, then save. A device must have a name, and the **Application** choice puts it into a named home setup or, as **Default**, leaves it standalone. Save your changes to this tab before you leave the page.

### Connection

This tab shows how the sensor connects to Chirp and lets you adjust its profile. It also carries the sensor's connection diagnostics, which tell you whether data is arriving and being saved — the place to look when a sensor is quiet or a reading is missing. See [Connection Diagnostics](connection-diagnostics.md).

**For LoRaWAN sensors:** Follow [LoRaWAN Devices](lorawan-devices.md) for every identity, profile, codec and interval field. Detach before changing a bound physical identifier; keep the twin and its measurement rows, then restore the source mappings.

### Mapping {#metrics}

The **Mapping** tab connects incoming data keys to retained measurement channels. When a sensor is replaced, keep the existing measurement rows and only point them at the new incoming key; swapping a key and replacing a measurement are two different things.

| Column or control | Purpose and configuration |
| --- | --- |
| **Device data key** | Pick the incoming field this row listens to, for example `temperature` or `vibration.rms`. The choices fill in once messages have arrived, and leaving it blank means this measurement records nothing. Click **Save** to keep a changed key. |
| **Value** | Latest received value for the selected source key. This snapshot is not the historical record. |
| **Last update** | When that source key was last received. An empty value means no corresponding received value is available. |
| **Normalized key** | Choose the metric template that defines the measurement. Only Telemetry templates are listed, and any template this device already uses appears grayed out. |
| **Unit** | The template's unit, displayed for reference only. Edit it in [metric templates](data-templates.md); mapping never converts units for you. |
| **Type** | Read-only template value type: Integer, Float, String or Boolean. It controls conversion of incoming readings. |
| **Data type** | Telemetry in this mapping form. Reported switch states can be recorded as telemetry too. |
| **Add key** | Adds an empty mapping row; pick a template and an incoming key for it. |
| **+ Add new metric** | Opens **Add Metric** straight from the Normalized key dropdown. Type a **Normalized key** (it cannot be empty), set **Type** (it starts as String), and leave **Data type** on Telemetry. **Add** creates the template and picks it for this row; **Cancel** closes the dialog without creating anything. There is no unit field in this small dialog, so set units later in the full metric catalog. |
| **Remove** | On a saved device this deletes the row and its measurement assignment right away. It is not how you change hardware. |

Selecting a template adds its measurement immediately on an existing device. Choosing another template for a row that already exists drops the old measurement assignment and sets up the new one in its place. Closing the page without clicking Save does not undo those actions. Preserve templates during replacement and change only source-key assignments, then save.

After you save mappings, wait for a new message and look at **Logs**. A field may show up in the incoming snapshot before its mapping is finished, and messages that arrived earlier are not filled in afterwards. Choose template types that fit the real values: `"ON"` and `"OFF"` are strings, whereas `true` and `false` are booleans. See [metric templates](data-templates.md) for conversion and rejection rules.

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

The date button shows whichever preset or range is active. Pick a quick range, or enter your own start and end, then click **Apply changes**; **Clear filter** resets it. Your plan's retention sets how far back the dates and presets go. Each reading carries a **Timestamp**, then the normalized measurement name as **Key**, then **Type** and **Value**, and the minute groups open and close so you can inspect single readings. If you see **No logs found**, nothing retained matches that range, so check the mapping and wait for a fresh message before you widen the dates. When loading fails, reload the page.

## Which quick actions are in the sensor lists?
You don't always need to open the full detail view. From any sensor list, the row action buttons let you:

- **Edit** (pencil icon) — Open the full detail page
- **Copy** (clone icon) — Create a new sensor pre-filled with the same settings
- **Delete** (trash icon) — Remove the sensor (with a confirmation dialog)

For more about what your sensors measure and how to customize it, see [Data Templates](data-templates.md). For room-based naming and dashboard organization, see [Rooms](rooms.md).

A physical-device copy starts new measurement rows: open it after saving and reconnect its **Device data keys**. An emulator copy carries its generated readings and reporting settings; give it a new Device ID.

For a replacement, use the existing device instead of **Copy**. Copy is for adding a separate device; its similar name and settings do not make it the same digital twin.

## How do I keep a home setup together?
The **Application** field on **Device Info** lets you put this sensor into a setup such as Home Watch. Select the application and save, or choose **Default** to keep the sensor ungrouped. [Organizing Content](../applications/organizing-content.md) explains how the dashboard, rule, and alarm definition join it.

## Where can I find protocol setup guides?
The full list of connection fields lives in [LoRaWAN Devices](lorawan-devices.md) and [MQTT Devices](mqtt-devices.md). Come back to this page for the profile, mapping and history controls that every sensor shares.
