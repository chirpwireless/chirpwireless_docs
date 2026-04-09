# Check and Clear Alerts

When an alert rule fires, Chirp keeps a record of it in your Notifications inbox. This is where you go to see what happened, when it happened, and whether it still needs your attention. Once you have dealt with the issue, you can mark the alert as resolved or delete it if you no longer need the record.

## Quick Check: The Notifications Drawer

You do not always need to open the full Notifications page. Chirp shows an unread notification indicator so you can peek at what is new from wherever you are:

- **On desktop**, click the notification icon next to your avatar in the sidebar. A drawer slides in from the right showing your latest unread alerts. Click any alert to mark it as read. Click **Mark all as read** at the top to clear them all at once.
- **On mobile**, tap the bell icon in the top header. The same drawer opens. When you close it, all alerts are automatically marked as read.

A badge with a count appears on the icon whenever you have unread notifications. If there is no badge, you are all caught up.

The drawer is a quick glance — it tells you whether something needs your attention. For reviewing details, resolving alerts, or searching through past alerts, open the full Notifications page from the sidebar.

## The Full Alerts Inbox

Open **Notifications** from the sidebar. The page opens at `/notifications` on the **Inbox** tab — this is your complete alert history.

### What You See

Each alert in the list shows:

| Column | What it tells you |
|---|---|
| **Subject** | The headline you wrote when creating the rule — e.g., *"Basement humidity is too high."* |
| **Status** | Either **Alarm** (still active, still repeating) or **Resolved** (handled, no more repeats). |
| **Type** | Critical, Important, or Information — so you can prioritize at a glance. |
| **Message** | The description you wrote in the alert rule. |
| **Date & Time** | When the alert fired. |

Use the **search bar** at the top to find specific alerts by subject or message — helpful if you are looking for all alerts related to a particular sensor or event.

### If Nothing Is Here Yet

If no alert rules have fired, the inbox shows: *"No notifications yet"* with a note: *"To see notifications, create a rule and let it generate activity."* Head to [Set Up a Home Alert](set-up-a-home-alert.md) to create your first rule.

## Understanding Alert Statuses

### Alarm

The alert rule fired and the condition was met on your sensor. While an alert has this status, Chirp keeps sending repeat notifications at the interval you configured (hourly for Critical, every 4 hours for Important, daily for Information).

In other words: if you see **Alarm**, Chirp is still actively telling you about this issue.

### Resolved

Someone marked the alert as resolved, or the sensor reading returned to normal. Chirp stops sending repeat notifications for this alert. The record stays in the inbox so you can look back at what happened and when.

## Resolving an Alert

### One at a Time

Find the alert in the list and click the **Mark as resolved** button on its row. The status changes from **Alarm** to **Resolved** immediately. The button label then changes to **Resolved** and becomes inactive — it stays visible so you can see the alert has been handled.

### Several at Once

If a situation triggered multiple alerts — maybe a power outage set off temperature alarms on every sensor in the house — you can resolve them all together:

1. Use the **checkbox** on each alert you want to resolve, or click the **select-all checkbox** in the header to select all active alerts. (Only alerts with **Alarm** status are selectable.)
2. A button appears showing **"(N) Mark as resolved"** with the count of selected alerts.
3. Click it. All selected alerts move to **Resolved**.

## Opening Alert Details

On mobile, each alert row has a chevron that opens the full detail page at `/notifications/:alarmId`. On desktop, alert detail pages are not directly accessible — the table does not support row-click navigation. Instead, use the per-row actions: **Mark as resolved** button, and the actions menu which offers **Go to rule page** and **Delete**.

On the detail page you see:

- The full **subject** and **message**
- The **type** (Critical, Important, or Information)
- The current **status** with a hover tooltip explaining what it means

From the detail page you can:

- **Go to rule page** — opens the alert rule that created this alarm, so you can review or adjust the conditions. Useful if an alert keeps firing and you want to tweak the threshold.
- **Mark as resolved** — same as from the list, but here you are looking at the full context first.
- **Delete** — permanently removes the alert. A dialog asks *"Are you sure you want to delete the alarm?"* Click **Yes, delete** to confirm, or **Cancel** to keep it.

## Deleting Alerts

Deleting removes an alert permanently — it will not appear in searches or in the inbox anymore. This is different from resolving: a resolved alert stays in the inbox as a historical record, while a deleted alert is gone.

Delete alerts when the record itself is not useful anymore. For alerts you want to keep for reference (e.g., to check when the last water leak happened), resolve them instead.

You can delete from the alert detail page or from the actions menu on each row in the inbox list.

## Daily Use Tips

- **Check the drawer first.** The notification icon gives you a fast answer to "has anything happened?" without navigating away from whatever you are doing. If the badge shows a count, glance at the drawer. If something looks serious, open the full inbox.
- **Resolve alerts when you have actually handled them.** Marking an alert as resolved tells Chirp to stop repeating the notification. If you resolve it but the underlying issue is not fixed, the rule will fire again and create a new alarm.
- **Use search for recurring patterns.** If you suspect a sensor is triggering too often, search for its name in the inbox to see the history. That might be a signal to adjust the threshold in the alert rule rather than keep resolving alerts.
