# Set Up a Home Alert

An alarm definition tells Chirp what to do when an automation in the [Rules Engine](../rules-engine/README.md) fires an alarm — who to notify, how urgently, through which channels, and what happens if nobody responds.

To create one, open the **Alarm** page from the sidebar, switch to the **Alarm definitions** tab, and click **Add alarm rule**.

## Alarm name

Give your alarm a clear name that describes what it watches for. This name appears in the Inbox when the alarm fires, so make it specific enough to act on at a glance.

| Field | Detail |
|---|---|
| **Alarm name** | Text field. Placeholder: *Enter name*. Required. |

## Severity

Choose how urgent this alarm is. The severity level controls how often notifications repeat (based on your [Notification Severity](notification-severity.md) settings) and how the alarm appears in the Inbox.

| Field | Detail |
|---|---|
| **Choose severity** | Dropdown. Options: Critical, High, Medium, Low, Info. Required. |

After you select a severity, a note appears below the dropdown showing the current repeat policy for that level — for example, how frequently notifications re-send if the alarm stays active. You can override this with a custom interval (see below).

## Custom notification interval

By default, the alarm uses the repeat policy from your [Notification Severity](notification-severity.md) settings. Turn this on to override that policy for this specific alarm.

| Field | Detail |
|---|---|
| **Custom Notification interval** | Toggle (Off by default). When On, shows interval and one-time controls. |
| **Interval** | Number + unit (Hours or Days). |
| **One-time notification** | Toggle. When On, the alarm sends one notification and does not repeat. |

## Escalation chain

The escalation chain determines who gets notified and when. The first step fires immediately. If the alarm is not resolved, additional steps fire after configurable delays.

This section is covered in detail on the [Escalation Chains](escalation-chains.md) page. In brief:

- The first step is always **Immediate** and cannot be removed.
- Click **Add step** to add escalation tiers with configurable delays.
- Each step has: **Notify** (recipients), **Via** (channels — Email and SMS are selectable; Push when enabled).
- Unresolved alarms continue through the configured chain until someone marks the event as resolved in the [Inbox](check-and-clear-alerts.md).

## Schedule

Control when this alarm is active. By default, alarms are active 24/7.

| Field | Detail |
|---|---|
| **Schedule** | Shows the current schedule or "24/7 by default". |
| **Change schedule** | Button that opens a popover with day-of-week toggles and a time range (From / To). |

Use scheduling for alarms that only matter during certain hours — for example, a "front door opened" alarm that you only want between 11 PM and 6 AM.

## Suppress duplicates

Prevent the same alarm from firing repeatedly within a short window. This is useful for sensors that report frequently — without suppression, a sensor reading every 30 seconds could generate dozens of identical alarms.

| Field | Detail |
|---|---|
| **Suppress duplicates within this window (in minutes)** | Slider. Range: 1–60 minutes. |

## Message

The message appears in every notification sent by this alarm. Write it so the recipient immediately understands what happened and what to do.

| Field | Detail |
|---|---|
| **Theme** | The notification subject line. Placeholder: *Fire alarm in the kitchen*. Required. |
| **Message body** | The notification body text (multiline, 3 rows). Placeholder: *Your text here*. Required. |

## Saving and managing

Click **Add new alarm rule** to create the definition (or **Save** if editing an existing one). Click **Cancel** to discard changes.

Once created, your alarm definition appears in the **Alarm definitions** tab:

- **Toggle** the switch to enable or disable the alarm without deleting it.
- **Edit** to reopen the definition and change any field.
- **Delete alarm** (available inside the edit form) permanently removes the definition.

## Home examples

- **Basement flood alarm:** Severity Critical, immediate notification to homeowner via email and push, escalation to partner via SMS if unresolved. Schedule: 24/7. Suppression: 5 minutes.
- **Freezer temperature spike:** Severity High, notify homeowner. Theme: "Freezer temperature rising." Message: "The kitchen freezer sensor has reported an unusual reading."
- **Front door after bedtime:** Severity Medium, schedule active 11 PM – 6 AM only. Notify both household members immediately.
