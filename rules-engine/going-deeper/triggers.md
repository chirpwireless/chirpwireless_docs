---
description: Create a condition that starts a Chirp automation now or after a delay for one sensor or several similar devices.
---

# Triggers

A **trigger** is a condition Chirp watches before starting an automation. It answers questions such as “Has this door been open too long?” or “Is any leak sensor wet?” and tells the automation which device caused it.

Triggers have two separate choices:

- **When to react** — immediately, or only after the condition has stayed true for a set time.
- **What to watch** — one device, or several devices that should all use the same condition and automation.

Selecting several devices does not create a reusable room or device group elsewhere in Chirp. Those devices belong to this trigger, and Chirp keeps a separate condition and timer for each one.

## Trigger or Sensor reading?

Open the automation's **Start Event** and choose the source that matches what you want:

| What should happen? | Choose | Then configure |
|---|---|---|
| Run the automation every time one sensor sends a reading | **Sensor reading** | Pick the device and sensor in the Start Event. |
| Wait until a condition is true | **Trigger condition** | Create a trigger and choose **Immediately**. |
| Ignore a brief door opening, motion event, or humidity spike | **Trigger condition** | Choose **Only if it lasts** and set the wait. |
| Use one automation for several similar devices | **Trigger condition** | Select those devices in the trigger. |
| Limit either choice to certain hours | Keep that start source | Turn on **Enable Schedule** in the Start Event. |

There are only two Start sources. A schedule is an optional time restriction, while immediate or delayed timing is part of the trigger itself.

## What happens when a trigger fires

The trigger watches and remembers the condition; the automation decides what to do about it.

1. Chirp evaluates the trigger whenever relevant device data arrives.
2. The trigger activates immediately or after its configured wait.
3. Chirp sends the watched device's identity to every running automation connected to that trigger.
4. The automation follows its diagram to send an alert, check more data, or control something.

A saved trigger does nothing visible until you connect it to an automation and deploy that automation.

## Create a trigger

1. Open **Rules Engine → Triggers**.
2. Select **Add trigger**.
3. Give the trigger a clear **Name**, such as `Freezer door left open`.
4. Under **What should start the rule?**, select a normalized key—the common reading name Chirp uses across devices.
5. Choose the comparison under **Is** and enter the **Value**.
6. Under **When should it start?**, select **Immediately** or **Only if it lasts**.
7. Set a separate clear condition if one normal reading should not clear the trigger.
8. Select the device or devices under **Devices**.
9. Check **How this trigger will run**, then select **Create trigger**.

<figure><img src="../../.gitbook/assets/trigger-time-window.jpg" alt="The Chirp trigger form with a condition and Only if it lasts selected"><figcaption></figcaption></figure>

One trigger can use up to 10 reading keys, select up to 500 devices, and wait from 10 seconds to 30 days.

Read [Trigger Timing](triggers/trigger-timing.md) for countdown, clearing, schedule, and practical examples. Read [One Automation for Multiple Devices](triggers/multiple-devices.md) when the same setup belongs on several sensors.

## Combine readings

Use **Add check on ‹reading›** to add another comparison for the same reading. Use **Add normalized key** when another kind of reading belongs in the condition.

- **AND** means every check must match.
- **OR** means at least one check must match.

The form also has an AND/OR choice between different reading keys. These choices combine readings for one watched device. They never make one device's state depend on another watched device's state.

## Connect the trigger to an automation

1. Create or edit the automation that should respond.
2. Select the **Start Event** and open its properties.
3. Change **Start source** to **Trigger condition**.
4. Pick the saved trigger in **Trigger condition**.
5. Save, build, and deploy the automation.

Set the source back to **Sensor reading** only when you want every event from one selected sensor. The Start Event cannot use both sources together.

The Trigger condition field currently loads only the first page of triggers. A trigger outside that first page cannot yet be chosen from the field.

## Use the device identity in your automation

The trigger signal provides:

| Variable | What it tells you |
|---|---|
| `vars.device_name` | Name of the watched device that met the condition |
| `vars.subject_kind` | Kind of watched item; currently `device` |
| `vars.subject_id` | ID of the watched device |
| `vars.sensor_id` | Sensor associated with the automation run and any alert |
| `vars.detector_id` | ID of the trigger |
| `vars.timestamp` | Trigger signal time in Unix seconds |

It does not provide `vars.value`. The trigger starts the automation with a condition transition, not with one normalized sensor event. This is true for immediate and delayed triggers.

Use the device name in an alert so you know which sensor needs attention:

```cel
"Freezer door left open: " + vars.device_name
```

Chirp does not add the name automatically.

## Change or remove a trigger

Changing a condition can restart countdowns that are already running. Chirp warns you before it resets that state.

Removing a trigger stops future monitoring and prevents its connected automations from starting again. Check the automations that use it before confirming the deletion.

## Fix common problems

| Problem | Check this |
|---|---|
| A device is missing | Make sure its sensor data is mapped to a reading used by the trigger. |
| Chirp cannot choose a sensor | If more than one sensor supplies the same reading, select the intended one. |
| The trigger will not save | Check the duration, then inspect every row in **How this trigger will run**. |
| An expression says `vars.value` is missing | Replace it with trigger context such as `vars.device_name`, or use enrichment to fetch another reading. |
| An alert does not name the sensor | Include `vars.device_name` in the alert message. |

## See also

- [Create an Automation](../your-first-automation/create-an-automation.md) — choose and configure a Start Event
- [Trigger Timing](triggers/trigger-timing.md) — filter brief events and apply schedules
- [One Automation for Multiple Devices](triggers/multiple-devices.md) — watch several devices independently
- [CEL for Home Automations](../reference/cel-for-home-automations.md) — use the available variables
