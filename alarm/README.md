# Alarm

Your sensors watch your home around the clock, but you are not always looking at the dashboard. The Alarm section bridges that gap — when a reading crosses a threshold you care about, Chirp notifies you through the channels you choose so you can act before a small problem becomes a bigger one.

> **How triggers and response work together:** The [Rules Engine](../rules-engine/README.md) decides _when_ an alarm is raised — it evaluates sensor data and fires an alarm when conditions are met. The Alarm section defines _what happens after_ the alarm fires: who gets notified, through which channels, how often, how escalation proceeds if nobody responds, and when notifications are suppressed.

## What you will find here

The Alarm page has three tabs:

- **Inbox** — Every alarm event that has fired, with its current status. Filter by severity or status, search by title, resolve alarms, or jump to the originating rule.
- **Alarm definitions** — Your alarm configurations. Each definition sets the severity, escalation chain, notification schedule, suppression window, and message for a specific type of alert. Click **Add alarm rule** to create a new one.
- **Settings** — Your contact methods. Add or verify email and SMS contacts, enable or disable delivery per channel, and manage push notification setup when enabled for your account.

A **Notification Severity** button in the page header (visible on all tabs) opens a separate modal for controlling how often each severity level repeats.

## Severity levels

Chirp uses five severity levels to prioritize alarms:

| Level | When to use it |
|---|---|
| **Critical** | Emergencies requiring immediate action — water leaks, fire alarms, security breaches |
| **High** | Urgent situations that need prompt attention — freezer temperature spikes, failing sensors |
| **Medium** | Important but not time-critical — humidity drifting out of range, unusual energy use |
| **Low** | Routine awareness — minor fluctuations, scheduled check-ins |
| **Info** | Background monitoring — status confirmations, periodic health reports |

Each level has its own notification repeat policy that you can configure in [Notification Severity](notification-severity.md).

## Escalation

When an alarm fires and nobody resolves it, Chirp can escalate — notifying additional people through additional channels after a configurable delay. This means your home is never left unattended just because one person missed a notification.

For full details, see [Escalation Chains](escalation-chains.md).

## Where to go next

- [Set Up a Home Alert](set-up-a-home-alert.md) — Walk through creating an alarm definition: name, severity, escalation chain, schedule, message.
- [Escalation Chains](escalation-chains.md) — How multi-step escalation works for unresolved alarms.
- [Notification Severity](notification-severity.md) — Configure how often each severity level repeats.
- [Check and Clear Alerts](check-and-clear-alerts.md) — Review what has happened, resolve alarms, and keep your inbox manageable.
- [Manage Contact Methods](manage-contact-methods.md) — Add email addresses, verify them, and manage notification channels.
- [Chirp Alerts App](chirp-alerts-app/) — Install the mobile app for push notifications. Critical alerts ring with an alarm sound and vibration until silenced or acknowledged.
