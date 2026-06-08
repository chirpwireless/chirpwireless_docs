---
description: See how critical, default, and quiet alerts behave on your phone based on the severity you assign.
---

# Alert Behavior

The Chirp Alerts app handles three types of alert delivery, each with different behavior on your phone. The severity you assign to an alarm definition on the web platform determines which type your phone receives.

## Critical

A critical alert triggers a full-screen alarm on your phone:

- A **pulsing warning icon** fills the screen
- The **alarm sound loops continuously** with vibration (repeating pattern)
- The screen shows the **device name**, **alert message**, and **timestamp**

This is designed to get your attention when your phone is locked or in silent mode. On supported devices with the right permissions granted, the alarm can appear over other apps.

You have two options:

- **Close** — silences the alarm sound on your phone. The alert is NOT resolved in Chirp — other household members still see it as active, and escalation continues if configured.
- **Dismiss & Acknowledge** — silences the alarm AND resolves the alert in Chirp. The alert is marked as resolved for everyone.

Use critical for emergencies: water leaks, security breaches, fire detection, freezer failures — anything that needs immediate human response.

## Important

An important alert shows as a prominent notification on your phone. It appears visibly — more noticeable than a standard notification — but does not trigger the full-screen alarm, alarm sound loop, or vibration pattern.

Use important for situations that need prompt attention but are not emergencies: temperature spikes, sensor failures, unusual readings that should be investigated soon.

## Information

An information alert arrives as a quiet notification without sound or vibration. It does not interrupt what you're doing.

Use information for routine awareness: a door opening during the day, periodic status confirmations, background monitoring events you want to be aware of but don't need to act on immediately.

## How Severity Connects to the Web

The three alert behaviors above are determined by the severity you choose when creating an alarm definition on the web platform. You configure severity in the [alarm definition](../set-up-a-home-alert.md), and the platform controls how that severity translates into phone behavior.

For the full severity configuration — including repeat intervals and per-alarm overrides — see [Notification Severity](../notification-severity.md).

## Delivery Notes

Push notification delivery depends on your phone's settings and state:

- If the app has been force-stopped (Android: Settings → Apps → Force Stop) or terminated by swiping it away (iOS), delivery may be limited until the app is opened again.
- Battery optimization features on some Android devices may delay delivery. Granting the app permission to run in the background improves reliability.
- For the most dependable coverage, keep the app installed and signed in on all household members' phones, and configure [escalation chains](../escalation-chains.md) so that if one person does not respond, the alert escalates to the next.
