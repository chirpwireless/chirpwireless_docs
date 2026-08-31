---
description: Use one Chirp trigger and automation for several devices while checking every sensor and countdown separately.
---

# One Automation for Multiple Devices

When the same idea applies to several sensors, you do not need to copy the automation. Select those devices in one trigger and connect that trigger to one automation.

This is a per-trigger selection, not a saved household group. You can choose a different set of devices in every trigger.

## What stays separate

The reading labeled **Devices answering this key are the watched ones** decides which selected devices Chirp checks independently.

If one trigger watches nine windows:

- every window has its own open-or-closed state;
- every window has its own “Only if it lasts” countdown;
- one open window does not advance another window's timer;
- the automation is told which window met the condition.

That means one automation can alert for the kitchen window tonight and the bedroom window tomorrow without mixing the two events.

## Build the device selection

1. Add the reading that defines the trigger condition.
2. Open **Devices** after the reading has been selected.
3. Find the sensors with **Search devices**, or use **Select all shown** when the same trigger belongs on the whole list.
4. If one device maps several sensors to the same reading, choose the correct sensor.
5. Inspect **How this trigger will run** and create the trigger only when every expected device has its own row.

You can select as many as 500 participants. That total includes devices watched independently and any device that supplies one shared reading.

<figure><img src="../../../.gitbook/assets/trigger-device-group.jpg" alt="The Chirp device selector and run preview showing one row for each watched device"><figcaption></figcaption></figure>

If a sensor is not available, check its **Mapping** tab. Its incoming value must be mapped to one of the readings used in the trigger.

## Conditions using more than one reading

Suppose every room sensor reports both temperature and humidity. A trigger can require `temperature > 26` AND `humidity > 70`, then evaluate that pair separately in every selected room.

Every watched device must provide each reading used this way. Chirp will not guess how to fill a missing input.

## Add one shared reading

One extra device can provide context for all watched devices. For example:

- each window sensor provides its own `window_open` reading;
- one thermostat provides the home's `heating_on` reading;
- the trigger checks every window separately against that one heating status.

The thermostat appears under **Uses** in the preview instead of getting a window row. A shared reading must come from exactly one selected provider; otherwise Chirp refuses the ambiguous setup.

## Say which device needs attention

Use `vars.device_name` in the alert created by the automation:

```cel
"Window still open: " + vars.device_name
```

The trigger also supplies the watched device and sensor IDs. It does not supply `vars.value`, because the automation receives the trigger's condition change rather than an individual sensor event.

## See also

- [Triggers](../triggers.md) — create the saved condition
- [Trigger Timing](trigger-timing.md) — immediate and delayed reactions
- [Data Templates](../../../devices/data-templates.md) — check sensor mappings
