---
description: Watch several home devices with one Chirp trigger, keep their waits separate, and use a shared reading when the condition needs it.
---

# Use a Trigger with Multiple Devices

A trigger checks readings for a condition you choose. If you want the same alert for several windows, you can select them in one trigger and connect it to one automation. You do not need a separate copy for every window.

Each window is still checked on its own. The kitchen window can reach its ten-minute wait before the bedroom window, and the automation receives the identity of the window that needs attention. Start with [Triggers](../triggers.md) if you have not created one yet.

## Separate devices, separate waits

Every watched device has its own condition state and start or recovery wait. Closing one window does not cancel another window's wait. The automation can respond to different windows at different times.

AND/OR joins readings within each evaluation, not all the selected windows into one condition. The selection is saved inside this trigger; it does not create a household group that other triggers automatically reuse.

## Choose the devices

1. Add the reading keys used by the trigger and any separate recovery condition.
2. Open **Devices** and use **Search devices** to find your devices. A listed compatible device supplies at least one of those keys.
3. Select the windows to watch. **Select all shown** selects eligible results already loaded; use **Load more devices** for further results. The button becomes **Select all** when all results for that search are loaded.
4. You can search for another device without losing earlier selections. **Clear selection** removes the whole selection.
5. Look at **How this trigger will run**, resolve any problems, and then save the trigger.

At least one device must be watched. You can select up to **500 devices**, including those that supply a shared reading. The starting and recovery conditions together can use up to **10 distinct reading keys**.

If a device is missing or unavailable, check its **Mapping** tab. It needs an incoming sensor value mapped to a required key. If two mapped sensors answer the same key, use the form's Mapping link to resolve that ambiguity. The trigger form does not let you choose between duplicate sensors. Check other uses of the mapping before changing it.

## Use two readings from every device

Suppose each room sensor provides temperature and humidity. You could require temperature above an illustrative **26°C AND humidity above 70%**, with your chosen duration. Chirp checks the pair of readings within each selected room device.

Every watched device must supply both readings in that arrangement. The form will report a missing input rather than guess which other device should supply it.

## Add a reading shared by all watched devices

A **shared reading** comes from one selected device and supplies information for every watched device. For example, each window could provide its open state, while one home controller supplies whether the heating is on.

To set up that example:

1. Add the window-state and heating-state keys with the comparisons you need.
2. Select the window devices and the controller that supplies the heating reading.
3. Check that **Devices answering this key are the watched ones** appears for the window-state key.
4. Check the preview: the windows should appear under **Evaluated device**, and **Uses** should name the shared heating reading and its controller.

The controller supplies context; it does not get its own window-evaluation row. Its heating reading can affect all the windows, but each window still keeps its own state and wait.

For each additional key, Chirp accepts either a reading from every watched device or a reading from exactly one selected provider. That provider can also be one of the watched devices. Different shared keys can use different providers. If several possible providers make the setup ambiguous, change the selection or mappings as described by the preview.

## Understand the preview

**How this trigger will run** describes the result of your selection:

| Column | What to look for |
|---|---|
| **Check** | A number for each independent evaluation. |
| **Evaluated device** | The window or other device whose condition will be watched. |
| **Uses** | Its own input readings and any shared reading, with the shared provider named. |

Every window you intend to watch should have a row. A device chosen only to supply a shared reading need not have one. Fix unanswered or ambiguous readings before saving.

## Say which device needs attention

In your automation's **Set Alarm** node, use this expression in **Motivation Message**:

```cel
"Window left open: " + vars.device_name
```

Chirp does not automatically add the name. The trigger also supplies the watched device and sensor IDs, but it does **not** supply `vars.value`: the automation receives a trigger signal rather than one sensor reading. See [CEL for Home Automations](../../reference/cel-for-home-automations.md) if you need more detail or another reading through enrichment.

## Add or remove devices later

Open the trigger's **Edit** form, update **Devices**, and review the preview before selecting **Save changes**. Read any warning about restarting countdowns. The change applies to all automations using that trigger.

Removing a watched device stops this trigger from watching it and requests clearing of its associated active trigger alert through connected, running automations. If an automation was stopped first, check **Alarm → Inbox** for an alert needing manual resolution.

If a warning appears beside the trigger after you change a device's mapping, review that mapping and the trigger's selected inputs. Save only once the preview describes the intended setup.

## See also

- [Triggers](../triggers.md) — create a trigger and connect an automation
- [Trigger Timing](trigger-timing.md) — immediate responses, waits, and recovery
- [Data Templates](../../../devices/data-templates.md) — understand reading keys and mappings
