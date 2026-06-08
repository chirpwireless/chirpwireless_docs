---
description: Review what fired in your Inbox, filter by severity or status, and resolve home alerts to stop escalation.
---

# Check and Clear Alerts

When an alarm fires, Chirp records it in your Inbox. This is where you see what happened, when it happened, and whether it still needs your attention. Resolving an alarm stops its [escalation chain](escalation-chains.md) — no further steps fire once the event is marked as resolved.

The Inbox is the default tab when you open the **Alarm** page from the sidebar.

## Filtering

Two dropdown filters sit above the alarm list:

| Filter | Options |
|---|---|
| **Severity** | All severity, Critical, High, Medium, Low, Info |
| **Status** | All status, Active, Resolved |

Use these to focus on what matters right now — for example, show only **Critical** + **Active** to see emergencies that still need attention.

## Searching

A search input lets you filter by alarm title. Start typing and the list narrows to matching results. If nothing matches, Chirp shows: *"We can't find your alarm."*

## Alarm list

On desktop, each alarm appears as a row with these columns:

| Column | What it shows |
|---|---|
| **Alarm** | The alarm title (or definition name), with a status indicator — a warning triangle for active alarms, a checkmark for resolved ones. |
| **Message** | The notification message body. |
| **Severity** | The severity level, color-coded. |
| **First trigger** | When the alarm first fired. |
| **Last trigger** | When the alarm most recently fired. |
| **Actions** | **Mark as resolved** button and a link to the originating rule. |

On mobile, alarms appear as compact cards with the same information in a condensed layout.

### Empty state

If no alarms have fired yet, the Inbox shows: *"No alarms yet — To see alarms, create a rule and let it generate activity."*

## Resolving an alarm

Click **Mark as resolved** on an active alarm to mark it as resolved. This does two things:

1. The alarm status changes from **Active** to **Resolved** — the indicator switches from a warning triangle to a checkmark.
2. Any remaining [escalation steps](escalation-chains.md) for this event are cancelled. No further notifications are sent.

Resolved alarms stay in the Inbox for your records. They do not disappear.

## Going to the originating rule

Each alarm has a link that navigates to the automation in the Rules Engine that triggered it (at `/rules/:ruleId/view`). This is useful when you need to understand why the alarm fired — what conditions were met, what sensor data triggered it, and whether the rule logic needs adjusting.

## Tips

- **Resolve alarms when the issue is handled.** An unresolved alarm continues to escalate and re-send notifications. Resolving it is how you tell Chirp "I've seen this and it's under control."
- **Use severity filters during busy periods.** If you have many alarms, filter to Critical and High first to prioritize what needs immediate action.
- **Check the originating rule if an alarm seems wrong.** If an alarm fires unexpectedly, the Rules Engine rule might have a condition that is too sensitive or a sensor that is reporting unexpected data.
- **Resolve alerts from your phone.** If you have the [Chirp Alerts app](chirp-alerts-app/managing-alerts.md) installed, you can resolve and manage alerts directly from your phone without opening the web platform.
