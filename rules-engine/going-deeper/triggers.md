---
description: Understand how a trigger watches your home sensors, detects a condition, and starts an automation that can alert you or operate a device.
---

# Triggers

A **trigger** watches information sent by your devices and detects a condition you choose. That condition could be a window left open, a water leak, or humidity staying too high for half an hour. You tell Chirp what to look for, which devices to watch, and whether to react straight away or wait to see if the condition lasts.

The trigger can then start a **rule**, also called an automation, which contains the steps that respond. Suppose you want an alert when a window has been open for ten minutes. The trigger checks the window readings and the wait. The automation raises the alert so you can decide whether to close the window.

You create the trigger and automation separately and connect them. A trigger can be saved before you have an automation. On its own, it does not send an alert, turn off a light, or operate another device.

## Is a trigger the same as a rule?

No. The trigger detects the condition; the rule carries out the response. Both are in **Rules Engine**, with separate **Triggers** and **Rules** tabs.

| Name in Chirp | Meaning |
|---|---|
| **Trigger** | The condition to watch, its devices, and its timing. It also defines when the condition returns to normal. |
| **Rule** or **automation** | The steps performed in response, such as raising an alert or sending a supported device command. |
| **Start Event** | The first node in the automation's diagram. You use it to choose what starts the automation. |

A saved trigger can start more than one automation. An **alarm definition** is a separate setup for handling and delivering an alert; the automation's **Set Alarm** step raises it.

## When do I need a trigger?

Use **Immediately** when a matching reading should lead to a response without an added wait, such as a leak sensor reporting water. Choose **Only if it lasts** when a brief change is normal, such as opening a window for a moment.

You can also select several devices in one trigger. Each window can have its own ten-minute wait while using the same automation to raise an alert.

Not every automation needs a saved trigger. Its Start Event offers two choices:

- **Sensor reading** starts from incoming readings from one selected sensor. Put any comparisons or decisions inside the automation.
- **Trigger condition** starts from a saved trigger that checks the condition and timing first.

Picking a device and sensor under **Sensor reading** does not create a trigger. Choose one start source. Whichever source you use, the automation must be running, and its schedule and execution-rate limits still apply.

## What you need first

Use the organization containing your devices and an account with permission to create or edit Rules Engine items. Check that the device is sending the reading you want to watch.

Chirp uses a **normalized key** as the common name for a reading, such as humidity or window state. The device's incoming value must be connected to that key on its **Mapping** tab. See [Data Templates](../../devices/data-templates.md).

Check the actual values: an open window might be represented by text, a number, or a Boolean value. If the trigger form reports that two sensors answer the same key, follow its link to **Mapping** and leave one intended mapped sensor for that key. There is no sensor-choice dropdown inside the trigger form.

You can create the trigger before its automation or alert exists. You will need an [alarm definition](../../alarm/set-up-a-home-alert.md) later if the response should notify you.

## Create a trigger

For this example, use a window sensor that reports the Boolean value `true` when open and `false` when closed. If your sensor uses another type or different values, use those instead.

1. Open **Rules Engine → Triggers** and select **Add trigger**.
2. Enter a **Name**, such as `Window left open`.
3. Under **What should start the rule?**, select **Add normalized key** and choose the key for your window reading.
4. Set **Is** to **equals** and **Value** to `true` for this example.
5. Under **When should it start?**, choose **Only if it lasts**, enter `10`, and choose **minutes**.
6. Leave **Clear by a separate condition** off. A reported closed state will return this trigger to normal. [Trigger Timing](triggers/trigger-timing.md#decide-when-the-trigger-returns-to-normal) explains how to use a different recovery condition or wait.
7. Under **Devices**, select the window device.
8. Check **How this trigger will run**. Your window should appear as an **Evaluated device**, with its reading under **Uses**. Resolve any reported problem.
9. Select **Create trigger**.

You return to the **Triggers** list with the trigger saved. It can watch incoming data, but it has not created an automation or configured an alert. The next section connects it to a response.

<figure><img src="../../.gitbook/assets/trigger-time-window.jpg" alt="Chirp trigger form showing a humidity comparison and a ten-minute wait"><figcaption>The same form supports other readings. This example screen uses humidity; choose the key and value reported by your window sensor for the walkthrough above.</figcaption></figure>

### Choose and combine comparisons

Numbers support **equals**, **is greater than**, and **is less than**. Text and Boolean readings use **equals**. Chirp shows a value field suited to the reading's type. A **Reported over the last … days** hint describes recent data; it does not define all the values a sensor can send.

**Add check on ‹reading›** adds another comparison for the same reading. **Add normalized key** includes another reading. Use **AND** when all checks must match or **OR** when any check may match. There is also an AND/OR choice between different keys.

These controls combine readings for each watched device; they do not require all selected windows to be open together. Every key needs a valid input, even in an OR condition. A trigger accepts up to **10 distinct reading keys** across its starting and clear conditions, and **500 selected devices**, including any shared-reading providers. Delayed conditions range from **10 seconds to 30 days**.

## From a trigger to a running automation

1. Go to **Rules Engine → Rules**. Select **Add Rule**, or edit an automation that should respond.
2. Select its **Start Event**, the first node already on the diagram. Use the pencil beneath it to open the properties.
3. Set **Start source** to **Trigger condition** and choose your saved trigger.
4. Select **Save** at the bottom of that panel.
5. Add and connect the response steps. For an alert, use **Set Alarm**, select an alarm definition, and enter a message. Connect the flow to an End Event. See [Send Alerts and Run Actions](../your-first-automation/trigger-alarms-and-actions.md).
6. Save the automation, then [build and deploy it](publish-and-run-an-automation.md). This makes the saved automation available to run; check that it is running.

The trigger itself has no Build or Deploy step. Saved triggers are selected in the Start Event, not in decision gateways or action nodes later in the diagram.

## Try it with a test device

Start with a spare window sensor and an automation that only raises a test alert.

1. Confirm that the open and closed values arrive in the device's mapped reading.
2. Open the test sensor and wait for its open report, then allow the configured ten-minute duration.
3. Look at the automation's [execution history](../reference/debugging-automations.md) and **Alarm → Inbox**. If an alarm appears but no notification reaches you, check its recipients and delivery settings.
4. Close the sensor, confirm that its closed report arrives, and check that the condition clears.
5. Try a short opening followed by a closed report before the duration ends. That period should not qualify.

Chirp can only judge the data it receives. No new report does not cancel the wait. Further matching readings can also run the automation again while the condition is active. Read [Trigger Timing](triggers/trigger-timing.md) before adding device commands.

## Change or remove a trigger

Select **Edit** beside the trigger, make your changes, and select **Save changes**. If a warning says the countdowns will restart, review it before confirming **Save**. The affected waits need to qualify again. Changes apply to every automation using that trigger, without building or deploying the trigger itself.

Removing a watched device stops this trigger from watching it and requests clearing of its associated active trigger alert. Check any existing alert for that device.

To delete the trigger, select its trash icon and confirm **Delete**. This stops monitoring and pending waits. Connected automations remain saved but receive no more signals from that trigger. The **Trash** tab restores deleted rules, not triggers. Trigger deletion cannot be undone there and does not undo commands already sent.

Automatic clearing of associated alerts uses connected automations that are still running. This applies when a condition returns to normal, a watched device is removed, or the trigger is deleted. If you stopped the automation first, check **Alarm → Inbox** for alerts that still need to be resolved.

## Fix common problems

| Problem | What to do |
|---|---|
| My device is missing or unavailable | Check **Mapping**. It must supply a required reading through a mapped sensor. Resolve duplicate sensors for the same key there. |
| The preview cannot use my selected devices | Check missing readings and shared providers. See [Use a Trigger with Multiple Devices](triggers/multiple-devices.md). |
| There is a warning beside the trigger | Its telemetry mapping changed. Review the device's mapping, then edit the trigger and check its inputs and preview before saving. |
| I cannot save | Complete the name, comparison values, duration, and devices. If the form says it cannot display this condition, it cannot safely save edits to that trigger. |
| A saved trigger is missing | The Triggers list and Start Event selector currently show only the first page. They display a notice when more exist; the selector cannot choose a trigger beyond that page. |
| I saved the trigger but got no alert | Connect a deployed, running automation with a **Set Alarm** step. Check received readings, duration, schedule, execution history, and alert delivery settings. |
| The action happens more than once | Further readings can signal an active condition again. Notification intervals are separate from automation execution limits. |

## Include the device in the alert

Put this expression in the **Set Alarm** node's **Motivation Message** to identify the affected device:

```cel
"Window left open: " + vars.device_name
```

Chirp does not add the name automatically. A trigger-started automation provides device and trigger identity information, but **no `vars.value`**. Update any expressions that use it before changing an existing automation from **Sensor reading** to **Trigger condition**. Use enrichment to obtain another reading when needed.

`vars.timestamp` is the time the trigger activated, in whole Unix seconds. Repeated signals for that active occurrence keep the same timestamp. It is not the time of each later reading or automation run. The [CEL guide](../reference/cel-for-home-automations.md) lists the available variables.

## See also

- [Trigger Timing](triggers/trigger-timing.md) — waiting, returning to normal, and repeated responses
- [Use a Trigger with Multiple Devices](triggers/multiple-devices.md) — one condition for several home devices
- [Create an Automation](../your-first-automation/create-an-automation.md) — build the response diagram
