---
description: Make Chirp react now or only after a condition lasts, and combine that wait with overnight automation hours.
---

# Trigger Timing

Some sensor changes need an immediate response. Others are normal when they last only a moment. Trigger timing lets you choose which is which before an automation sends an alert or controls a device.

Timing does not choose the sensors. It controls how long each selected device's condition must stay true.

## Immediately or Only if it lasts

Open **When should it start?** in the trigger and choose:

- **Immediately** when the first matching reading should activate the trigger.
- **Only if it lasts** when Chirp should start a countdown and react only if the condition is still true when that countdown finishes.

<figure><img src="../../../.gitbook/assets/trigger-time-window.jpg" alt="A Chirp humidity trigger set to Only if it lasts for 10 minutes"><figcaption></figcaption></figure>

For a delayed trigger:

1. Select **Only if it lasts**.
2. Enter the wait as a whole number.
3. Choose seconds, minutes, hours, or days.

The shortest wait is 10 seconds and the longest is 30 days. A new delayed trigger starts with 10 minutes selected.

## What happens between reports

No new sensor message does not cancel the countdown. Chirp continues using the condition state it already knows until a relevant reading changes it.

Match the wait to how often the sensor reports. If a door sensor reports only every 15 minutes, a 10-minute wait may finish before a second report confirms that the door is still open.

## Decide when the trigger returns to normal

The usual clear behavior is simple: when the starting condition no longer matches, that device's trigger state clears.

Turn on **Clear by a separate condition** when recovery needs a different threshold or its own wait. For example, start a humidity trigger after the reading stays above 75% for 20 minutes, then clear it only after humidity stays below 65% for 30 minutes. That gap prevents the alert from repeatedly opening and clearing around one borderline value.

Each watched device clears separately. A normal reading from one window does not cancel the timer or active condition for another window.

## Add hours with Enable Schedule

The trigger's wait and the automation's schedule are two controls:

- **Only if it lasts** filters out conditions that end too quickly.
- **Enable Schedule** on the Start Event limits the hours when the automation may respond.

The trigger continues watching outside those hours. When it activates, the automation checks the schedule before it runs.

## Examples

### Freezer door at night

Create a trigger for `door_open = true` and choose **Only if it lasts — 10 minutes**. On the automation's Start Event, enable a schedule from 23:00 to 06:00. Opening the freezer briefly for a late-night snack does not finish the countdown. A door left open for 10 minutes during those hours starts the automation, which can wake you with an alert before the food warms up.

### Sustained movement in a garage

Motion can be ordinary when someone walks to a car and leaves. Set the motion condition to last 10 minutes and let the automation run only overnight. A short visit ends before the wait completes; continuing movement during the night starts the security alert.

### Shower humidity

Bathroom humidity often rises briefly during a shower. Use a 30-minute duration without a schedule so Chirp ignores the expected spike but starts the dehumidifier if damp air lingers. The duration is useful here even though the automation should work all day.

### Water leak

For a leak sensor, choose **Immediately** and leave the schedule off. Water needs a response at any hour, and waiting would add risk rather than reduce a false alarm.

## See also

- [Triggers](../triggers.md) — define the condition and connect it to an automation
- [One Automation for Multiple Devices](multiple-devices.md) — give each selected device its own countdown
- [Automation Node Guide](../../reference/automation-node-guide.md) — configure the Start Event schedule
