---
description: Learn how to create a Chirp trigger on its own, how it differs from a rule, and how to connect it to a home automation.
---

# Triggers

A **trigger** watches device readings for a condition you choose, such as a freezer door staying open for ten minutes. When that condition is met, the trigger can start a connected **rule**, also called an automation. The rule defines the response, such as raising an alert.

For example, if you want an alert when the freezer door is left open, the **trigger** checks the door readings and the ten-minute wait. The **rule** contains the steps that raise the alert. Creating the trigger alone does not send an alert; you need to connect it to a running automation.

You create and save these separately. You do not need a rule to create a trigger: open **Rules Engine → Triggers**, select **Add trigger**, fill in the condition and devices, then select **Create trigger**. Connect it to an automation when you are ready to set up the response.

Triggers have two separate choices:

- **When to react** — immediately, or only after the condition has stayed true for a set time.
- **What to watch** — one device, or several devices that should all use the same condition and automation.

Selecting several devices does not create a reusable room or device group elsewhere in Chirp. Those devices belong to this trigger, and Chirp keeps a separate condition and timer for each one.

## Is a trigger the same as a rule?

No. The trigger checks whether the condition for a response has been met. The rule carries out the response. You save these separately and then connect them.

| Name in Chirp | What it does | Where to find it |
|---|---|---|
| **Trigger** | Watches a condition and remembers its timing for each selected device. | **Rules Engine → Triggers** |
| **Rule** or **automation** | Carries out the steps in your flowchart. | **Rules Engine → Rules** |
| **Start Event** | Selects the sensor reading or saved trigger that starts the rule. | The automation's canvas |

Picking a sensor inside an automation is not the same as creating a trigger. That choice starts the rule from sensor readings directly. A saved trigger can start more than one rule, while each rule chooses one start source.

An **alarm definition** is separate too: it sets up the alert and its delivery. The trigger watches the condition; the rule's **Set Alarm** step raises the alert.

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

## From a trigger to a running automation

A trigger is a saved **start source**, not a node that you drag onto the automation canvas. Creating it and connecting it to an automation happen in two different tabs:

1. Open **Rules Engine → Triggers**, select **Add trigger**, configure the condition, timing, and devices, and select **Create trigger**.
2. Return to the **Rules** tab. The **Add Rule** button is available there, not on the Triggers tab.
3. Select **Add Rule**, or edit an existing automation that should respond.
4. Find the **Start Event** already placed on the canvas. Select it and use the pencil beneath the node to open its properties.
5. Change **Start source** to **Trigger condition**, then select the trigger you saved.
6. Select **Save** at the bottom of the Start Event panel. This applies the trigger to the diagram.
7. Add the alert, command, enrichment, or other nodes that define the response. Then select **Save** in the automation editor.
8. Build the automation and deploy the resulting artifact. Only a deployed automation can respond when the trigger becomes active.

Creating a trigger does not create an automation, add a node to the canvas, or select the trigger automatically. The trigger decides **when and for which device** the automation starts; the nodes after the Start Event decide **what happens next**.

## What you need first

Use the organization containing your devices, with permission to create or edit Rules Engine items. At least one device must supply a mapped reading used by the condition. A **normalized key** is the common name of that reading, such as temperature or door state.

You can save the trigger before creating an automation or setting up its alert. If a device has several sensors for the same reading, choose the one you want Chirp to watch.

## Create a trigger

1. Open **Rules Engine → Triggers**.
2. Select **Add trigger**.
3. Give the trigger a clear **Name**, such as `Freezer door left open`.
4. Under **What should start the rule?**, select a normalized key—the common reading name Chirp uses across devices.
5. Choose the comparison under **Is** and enter the **Value**.
6. Under **When should it start?**, select **Immediately** or **Only if it lasts**.
7. Set a separate clear condition if one normal reading should not clear the trigger.
8. Select the device or devices under **Devices**.
9. Check **How this trigger will run**. Each **Evaluated device** row is watched separately; **Uses** shows any shared reading. Resolve any missing or ambiguous input, then select **Create trigger**.

You return to the **Triggers** tab with a saved trigger. It has not created a rule or added anything to a canvas. The condition can be monitored, but it will only lead to an alert or device action once you [connect and deploy an automation](#from-a-trigger-to-a-running-automation).

<figure><img src="../../.gitbook/assets/trigger-time-window.jpg" alt="The Chirp trigger form with a condition and Only if it lasts selected"><figcaption></figcaption></figure>

One trigger can use up to 10 reading keys, select up to 500 devices, and wait from 10 seconds to 30 days.

Read [Trigger Timing](triggers/trigger-timing.md) for countdown, clearing, schedule, and practical examples. Read [One Automation for Multiple Devices](triggers/multiple-devices.md) when the same setup belongs on several sensors.

## Combine readings

Use **Add check on ‹reading›** to add another comparison for the same reading. Use **Add normalized key** when another kind of reading belongs in the condition.

- **AND** means every check must match.
- **OR** means at least one check must match.

The form also has an AND/OR choice between different reading keys. These choices are evaluated separately for each watched device. They can include a reading supplied by one shared device, such as the heating status from a home controller. This does not require every watched device to match at once. See [shared readings](triggers/multiple-devices.md).

## Where triggers can be used

In the current automation editor, the Start Event is the only place where you select a saved trigger. Triggers are not available on gateways, Set Alarm, Execute Command, Enrichment, or other nodes later in the automation.

One saved trigger can be selected by several automations. When it becomes active, every deployed automation that uses it can run. Each individual automation still has exactly one Start Event and one start source.

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

On the **Triggers** tab, select **Edit** beside the trigger, change its settings, and select **Save changes**. If Chirp warns that the countdowns will restart, confirm **Save** only when you want the affected devices to start their wait again. Every automation using that trigger will use its updated monitoring condition. You do not build or deploy the trigger itself.

To remove a trigger, select its trash icon and confirm **Delete**. Monitoring stops, Chirp requests clearing of alerts associated with its active conditions, and rules using it stop receiving its signals. The rules themselves remain saved, and device commands already sent are not reversed. The **Trash** tab restores deleted rules, not triggers; trigger deletion cannot be undone there. Automatic clearing uses the connected rules that are still running. If you stopped a rule before deleting its trigger, check **Alarm → Inbox** for alerts that still need to be resolved.

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
