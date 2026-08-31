---
description: Apply one trigger to a group of devices, combine their readings, and control when a Chirp automation starts.
---

# Triggers

A trigger starts an automation when device data matches a condition. One trigger can include up to **500 devices**, so the same automation can respond to an entire device group.

Before triggers, each automation could listen to only one device's sensor. If you wanted the same response for nine windows, you needed nine automations. With a trigger, you define the condition once, select all nine window devices, and connect one automation. Each watched device is evaluated independently: one device can start the automation without changing the state or countdown of the others.

A trigger can act immediately or wait until the condition has remained true for a set time. For example, Chirp can ignore a refrigerator door opened briefly and alert you only if it remains open for 10 minutes.

## Before you start

Decide which devices need the same response and which reading the trigger will evaluate, such as temperature, humidity, motion, or whether a door is open.

The devices that provide the condition reading labeled **Devices answering this key are the watched ones** receive independent evaluations. If a device is missing from the trigger's device list, open its **Mapping** tab and confirm that its incoming data is mapped to a reading used by the trigger. See [Data Templates](../../devices/data-templates.md).

You can create the trigger before the automation, but the trigger does not send an alert or control equipment by itself. After saving it, connect it to an automation's Start Event.

## Create a trigger

1. Open **Rules Engine → Triggers**.
2. Click **Add trigger**.
3. Complete the **Create trigger** dialog from top to bottom.

### 1. Name the trigger

Enter a **Name** that describes the situation, such as `Refrigerator door left open` or `Bathroom humidity remains high`. This is the name you will select later when configuring the automation.

### 2. Define what should start the automation

Under **What should start the rule?**, click **Add normalized key** and select the reading to evaluate.

For each reading, set:

- **Is** — the comparison operator. Number readings offer **equals**, **is greater than**, and **is less than**. Text and yes/no readings offer **equals**.
- **Value** — the value to compare with the sensor reading.

Use **Add check on ‹reading›** when one reading needs another comparison. Use **Add normalized key** when the condition also depends on a different reading.

When you add more than one check, choose how the checks are combined:

- **AND** means every check must be true. For example, `temperature > 18` AND `temperature < 24` defines a range.
- **OR** means any check can be true. For example, `status = open` OR `status = forced` accepts either state.

There is a separate **AND/OR** choice between different readings. It combines the readings used for one watched device; it never combines the watched devices with one another.

The reading marked **Devices answering this key are the watched ones** determines which devices receive independent evaluations. An additional reading must be available from every watched device or from exactly one selected device that supplies a shared value for all of them.

For example, each window device can provide its own open-or-closed reading while one thermostat provides the shared heating status. The thermostat participates in the trigger, but it does not receive its own window evaluation. Chirp will not save a combination where only some watched devices provide the additional reading.

### 3. Choose when the trigger starts

Under **When should it start?**, choose one timing mode:

- **Immediately** — start the automation as soon as the condition becomes true. Use this when you need device grouping without a delay.
- **Only if it lasts** — start the automation only after the condition has remained true for the duration you enter.

For **Only if it lasts**, select seconds, minutes, hours, or days. New triggers default to 10 minutes. The allowed range is 10 seconds to 30 days.

Set the duration longer than the sensor's reporting interval. If a sensor sends no new value during the wait, the countdown continues; silence does not reset it. A 10-minute duration on a sensor that reports every 15 minutes would still be based on only one reading.

<figure><img src="../../.gitbook/assets/trigger-time-window.jpg" alt="The Create trigger dialog with a humidity condition and Only if it lasts set to 10 minutes"><figcaption></figcaption></figure>

### 4. Configure clear behavior

By default, the trigger clears on the first reading that no longer satisfies the starting condition.

Turn on **Clear by a separate condition** when returning to normal requires a different condition or its own delay. For example, a motion trigger can start after 10 minutes of activity and clear only after the area has remained quiet for five minutes.

### 5. Select devices

Under **Devices**, select every device that should provide data to the trigger. The list becomes available after you select a normalized key and includes devices that provide at least one required reading.

Use **Search devices**, **Select all**, **Select all shown**, **Clear selection**, and **Load more devices** to manage the selection. A trigger requires at least one device and accepts up to 500. The limit includes watched devices and devices supplying shared readings.

If an expected device is missing, open its **Mapping** tab and map its incoming data to a reading used by the trigger. If a device has two sensors mapped to the same reading, choose which sensor the trigger should use. A sensor without a source mapping cannot supply readings to a trigger.

### 6. Review and save

**How this trigger will run** shows one row for every watched device. A device selected only to supply a shared value appears in the **Uses** column instead of receiving its own row. Check the **Evaluated device** and **Uses** columns before saving.

<figure><img src="../../.gitbook/assets/trigger-device-group.jpg" alt="The device picker and the How this trigger will run table, one row per watched device"><figcaption></figcaption></figure>

Click **Create trigger**. Chirp now monitors the saved device group, but the trigger will not perform an action until an automation uses it.

## Use the trigger in an automation

1. Open the automation that should respond to the trigger.
2. Select the **Start Event** node.
3. Click the pencil beneath the node to open its properties.
4. Set **Start source** to **Trigger condition**.
5. Select the trigger under **Trigger condition**.
6. Save, build, and deploy the automation as usual.

Set **Start source** to **Sensor reading** when an automation should continue to start directly from one sensor. A Start Event uses one source or the other, not both.

The selector currently shows only the first page of triggers. If the trigger you need is not listed, it cannot yet be selected from this field.

## Name the device in an alert

A trigger-started automation provides the name of the watched device that met the condition as `vars.device_name`. Include it in the alarm's message so the alert identifies the affected device:

```
"Window left open: " + vars.device_name
```

The device name is not added automatically.

`vars.value` is not available to a trigger-started automation. A trigger reports that a condition held; it does not pass one reading as the event value. Update any existing expression that expects `vars.value` before changing its Start Event to a trigger.

The available trigger variables are:

| Variable | Value |
|---|---|
| `vars.device_name` | Name of the watched device whose condition started the automation |
| `vars.subject_kind` | Type of watched resource; currently `device` |
| `vars.subject_id` | ID of the watched device whose condition started the automation |
| `vars.sensor_id` | Sensor ID used to associate the run and any alarm with the watched device |
| `vars.detector_id` | ID of the trigger that started the automation |
| `vars.timestamp` | Unix timestamp for the trigger signal |

While a condition remains active, later readings can start the connected automation again. Chirp limits rapid duplicate execution, but an action should still be safe to repeat. For example, use an alarm definition that continues the same incident instead of assuming the automation can run only once.

## Combine a trigger with a schedule

**Enable Schedule** on the Start Event also applies to trigger-started automations. The trigger watches and counts continuously; the schedule is checked when the countdown completes and the automation starts.

For a schedule of 22:00–06:00 and a 10-minute trigger:

- a condition that begins at 21:55 and completes at 22:05 can start the automation;
- a condition that completes at 06:05 cannot start the automation.

This lets an event that continues into your scheduled hours still receive a response.

## Change or remove a trigger

Editing a trigger's condition can restart active countdowns. Chirp warns you before saving a change that resets the current trigger state.

Deleting a trigger cannot be undone. It stops future monitoring and prevents connected automations from starting again. Resolve or review any outstanding alarms first, and check which automations use it before deleting it.

## Troubleshooting

| Problem | What to check |
|---|---|
| A device is missing from the selection | Confirm its data is mapped to the required reading on the device's **Mapping** tab. |
| A device is listed but cannot supply a reading | Confirm the sensor has a source mapping. If several sensors answer the same reading, select the intended sensor. |
| The trigger will not save | Confirm the duration is between 10 seconds and 30 days. Then review **How this trigger will run** for an unanswered reading or a shared reading supplied by more than one selected device. |
| The automation starts but an expression fails | Remove uses of `vars.value`; use the trigger variables listed above. |
| The alert does not identify the device | Add `vars.device_name` to the alarm message. |
| The automation runs again while the condition is still active | Later readings can produce another run. Make downstream actions safe to repeat. |
| A countdown restarted after editing | Changes to the condition can reset active countdowns; Chirp warns before saving. |

## See also

- [Trigger Alarms and Actions](../your-first-automation/trigger-alarms-and-actions.md) — choose what the automation does
- [CEL for Home Automations](../reference/cel-for-home-automations.md) — use trigger variables in expressions
- [Safety and Alerting](../examples/safety-and-alerting.md) — adapt complete home-safety examples
