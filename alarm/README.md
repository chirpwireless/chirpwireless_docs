---
description: See how Chirp turns sensor readings into home alerts, with an Inbox, alarm rules, and contact settings.
---

# Alarm

An alarm in Chirp is a record of something in your home that needs attention, such as a leak sensor reporting water. The Alarm section keeps those events in an Inbox and sends notifications to the people you choose.

Three pieces work together. A saved **alarm definition** says what message to send and who should receive it. A **rule**, or automation, raises an event using that definition. The **delivery channel** carries the notification by email, SMS, or push to your phone.

Start with [Set Up a Home Alert](set-up-a-home-alert.md) to configure the notification and its responding automation. A separate [trigger](../rules-engine/going-deeper/triggers.md) can watch for a condition, such as a door staying open; the automation supplies the response.

## What you will find here

The Alarm page has three tabs:

- **Inbox** — Every alarm event that has fired, with its current status. Filter by severity or status, search by title, resolve alarms, or jump to the originating rule.
- **Alarm definitions** — Your alarm configurations. Each definition sets the severity, escalation chain, notification schedule, suppression window, and message for a specific type of alert. Click **Add alarm rule** to create a new one.
- **Settings** — Your contact methods. Add or verify email and SMS contacts, enable or disable delivery per channel, and manage push notification delivery through the [Chirp Alerts app](chirp-alerts-app/).

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
