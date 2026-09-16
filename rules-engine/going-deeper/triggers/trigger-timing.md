---
description: Choose when a Chirp trigger reacts, learn what interrupts its wait, and decide when an active condition returns to normal.
---

# Trigger Timing

A trigger checks your device readings for a condition, such as a window being open. Timing lets you choose whether to react straight away or wait. A short window opening may be normal; one that lasts ten minutes may be worth an alert.

When the condition qualifies, that device's trigger becomes **active** and can start its connected automation. **Clearing** means it has returned to normal. Each watched device has its own wait and state. If you have not created a trigger yet, start with [Triggers](../triggers.md).

## Immediately or Only if it lasts

Under **When should it start?**, choose:

- **Immediately** to react when the reported data meets the condition, without adding a wait.
- **Only if it lasts** to require a qualifying period. A reading that makes the condition false interrupts that period, even if the condition is true again at the original finish time.

For a wait, enter a whole number and choose **seconds**, **minutes**, **hours**, or **days**. The shortest duration is **10 seconds**, the longest is **30 days**, and the starting choice is **10 minutes**.

<figure><img src="../../../.gitbook/assets/trigger-time-window.jpg" alt="Chirp trigger timing controls set to Only if it lasts for ten minutes"><figcaption>The timing controls work with the condition you chose above them.</figcaption></figure>

## What if the window closes and opens again?

For a ten-minute window-open condition, this is how reported changes affect the wait:

| Reported time | What the sensor reports | What it means |
|---|---|---|
| 18:00 | Open | The qualifying period begins. |
| 18:04 | Closed | The first opening did not last long enough. |
| 18:07 | Open again | A new qualifying period begins. |
| 18:10 | Still open | Only three minutes of the new period have passed, so the first deadline cannot qualify. |
| 18:17 | No closed report since 18:07 | The new ten-minute period can qualify. |

The wait requires a qualifying period, not just an open reading at the beginning and another open reading at the original deadline. A reported closed state in between matters.

## What happens between reports

No new message does not cancel the wait. Chirp continues evaluating the state established by the reports it has received. A ten-minute wait can finish before another message from a sensor that reports every 15 minutes.

Check how your sensor reports changes before choosing the duration. A window sensor needs to report closed as well as open. A motion sensor must report no motion if you want that change to interrupt a movement condition. Silence after a motion message does not by itself mean movement stopped. Missing or unreadable data is not a confirmed return to normal.

## Decide when the trigger returns to normal

With **Clear by a separate condition** off, the trigger clears when an evaluation shows that the starting condition is false. In the window example, the reported closed state clears that window's active condition. Another window's wait is unaffected.

Use a separate recovery condition when a different reading or a longer recovery is needed:

1. Under **Clear behavior**, turn on **Clear by a separate condition**.
2. Add the reading, comparison, and recovery value.
3. Choose **Immediately**, or **Only if it lasts** with a recovery duration.
4. Review the selected devices and preview, then save. The recovery readings need to be supplied too.

For example, you could detect humidity **above 75% for 20 minutes** and clear it only after humidity stays **below 65% for 30 minutes**. These example values are yours to adjust. If humidity drops to 70% after activation, the trigger stays active because it has not met the separate recovery condition. A reported rise above the recovery threshold during its wait means that recovery period does not qualify.

Clearing requests resolution of associated trigger alerts through connected automations that are still running. If you stopped the automation first, check **Alarm → Inbox** for an alert needing manual resolution. Clearing does not undo a command to a lamp, relay, or other device.

## Does the automation run only once?

Not necessarily. More readings can signal the same active condition again, and the connected automation can run again subject to execution-rate limits and its schedule. If the automation sends a command, that command can be repeated.

How often an alarm sends notifications is a separate setting in its alarm definition. The trigger's wait is neither a notification interval nor a timer between automation runs.

If you use `vars.timestamp` in a message, it gives the original activation time. Repeated signals for the same active condition keep that value. The automation's execution history shows individual run times.

## Allow the response only at certain hours

A trigger's wait and an automation's schedule do different jobs. The wait checks how long the condition qualifies; the schedule limits when the automation may respond.

1. Open the automation's Start Event properties and turn on **Enable Schedule**.
2. Select **Change schedule**, choose the days and **From**/**To** hours, and set the **Time Zone**.
3. Save the automation and build and deploy the updated version. See the [Automation Node Guide](../../reference/automation-node-guide.md) for the fields.

The trigger keeps watching and waiting outside those hours. The automation checks the schedule when it processes a trigger signal; an attempt outside its hours is skipped and recorded in history. A response is not guaranteed to finish at the exact moment the wait ends.

Suppose the schedule is 23:00–06:00. A window-open period beginning at 22:55 can qualify at 23:05 and lead to a response inside those hours. A signal processed at 06:05 is outside the window. The clock reaching 23:00 does not itself start an automation: a later trigger signal is needed. Another matching report from an already active trigger may provide it.

## Choosing a useful setup

- **Window left open:** wait ten minutes and raise an alert. A short opening is filtered when the closed report arrives before the period qualifies.
- **Shower humidity:** use a sustained high-humidity condition without a schedule if it matters throughout the day. The automation can alert you or send a supported command to a dehumidifier; clearing does not automatically turn it off.
- **Water detected:** choose **Immediately** and leave the automation schedule off when you want a response at any hour. The alert depends on the sensor's report and your configured delivery settings.

## See also

- [Triggers](../triggers.md) — create the condition and connect the automation
- [Use a Trigger with Multiple Devices](multiple-devices.md) — separate waits for several home devices
