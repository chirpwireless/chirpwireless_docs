# Notification Severity

Chirp uses five severity levels to classify alarms by urgency. Each level carries its own notification repeat policy — how often Chirp re-sends the notification while the alarm stays active. You can adjust these policies to match how your household responds to different kinds of alerts.

## Opening the severity settings

Click the **Notification Severity** button in the Alarm page header. This button is visible on all tabs (Inbox, Alarm definitions, and Settings). It opens a modal titled **Notification severity** with the subtitle: *"Choose how often notifications should be sent. You can enable a one-time notification or set a repeat interval."*

## The five severity levels

| Level | Typical use |
|---|---|
| **Critical** | Emergencies — water leaks, smoke detection, security breaches. You want to know immediately and be reminded until you act. |
| **High** | Urgent — freezer temperature spikes, failed sensors. Needs prompt attention but may not be a safety issue. |
| **Medium** | Notable — humidity drifting outside comfort range, unusual energy patterns. Worth knowing about, but action can wait. |
| **Low** | Routine — minor fluctuations, background conditions changing. Awareness-level information. |
| **Info** | Background — periodic status updates, sensor health confirmations. No action expected. |

## Configuring repeat behavior

For each severity level, you can set:

- **One-time notification** — Toggle this On to send a single notification when the alarm fires. No repeats. Turn it Off to use a recurring interval.
- **Repeat interval** — When one-time is Off, set how often the notification re-sends (a number + unit: Hours or Days). The alarm keeps repeating at this interval until someone resolves it.

## Per-alarm overrides

The severity policy sets the default repeat behavior for every alarm at that level. If a specific alarm needs different timing, you can override the policy directly in the [alarm definition](set-up-a-home-alert.md) using the **Custom Notification interval** toggle.

When an alarm has a custom interval, it uses that setting instead of the global policy for its severity level.

## Tips

- **Start with one-time for Info and Low.** These are awareness-level notifications — repeated reminders for background information can become noise.
- **Use recurring intervals for Critical and High.** You want persistent reminders for emergencies and urgent issues until someone resolves them.
- **Revisit your settings after the first week.** Once you see how your alarms behave in practice, adjust the intervals to match your household's response patterns.
- **Severity also controls push behavior.** If you use the [Chirp Alerts app](chirp-alerts-app/alert-behavior.md), the severity you assign here determines whether an alert triggers a full-screen alarm on your phone (critical), a prominent notification (important), or a quiet notification (information).
