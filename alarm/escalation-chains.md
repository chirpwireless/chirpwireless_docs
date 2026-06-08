---
description: Build a step-by-step chain so an unresolved home alert reaches more people until someone responds.
---

# Escalation Chains

When an alarm fires and nobody resolves it, you do not want it to disappear into a missed notification. Escalation chains make sure the right people find out — starting with the first person who should know, and reaching out to others if the alarm stays unresolved.

## How escalation works

Every alarm definition includes an **Escalation chain** — a sequence of steps that tell Chirp who to notify and when.

The first step always fires **immediately** when the alarm is triggered. If nobody resolves the alarm within a configurable delay, the next step fires, notifying additional recipients through additional channels. This continues through each step until the alarm is either resolved or every step has been executed.

**Resolving an alarm stops escalation.** Once you or another household member marks the alarm as resolved in the [Inbox](check-and-clear-alerts.md), no further escalation steps fire for that event.

## Setting up an escalation chain

When you [create or edit an alarm definition](set-up-a-home-alert.md), the **Escalation chain** section appears in the alarm form.

### The first step

The first step is always present and cannot be removed. Its delay is set to **Immediate** — recipients in this step are notified the moment the alarm fires.

For each step, you configure:

- **Notify** — Select one or more household members from the **Choose recipients** dropdown. **Required** — you must select at least one person or the definition cannot be saved.
- **Via** — Select the delivery channels. Email and SMS are selectable in every step. Push notifications are delivered through the [Chirp Alerts app](chirp-alerts-app/) and appear when enabled for your account (see [Manage Contact Methods](manage-contact-methods.md)).

### Adding more steps

Click **Add step** to add an escalation step. Each additional step has:

- **After** — A configurable delay. This is how long Chirp waits after the previous step before firing this one. The alarm must still be unresolved for this step to execute.
- **Notify** — Recipients for this step (can be different from earlier steps).
- **Via** — Channels for this step (can also be different).

You can add as many steps as your household needs. Only the first step is permanent — additional steps can be removed with the delete button.

### Reordering and removing

Additional steps appear in order below the first step. Remove a step by clicking the trash icon on its row. The first step cannot be removed.

## Example: household escalation

Imagine a water leak sensor in the basement triggers an alarm at 2 AM:

1. **Step 1 (Immediate):** Notify the homeowner via email and push notification.
2. **Step 2 (after a configurable delay):** If the alarm is still unresolved, notify the homeowner's partner via SMS.
3. **Step 3 (after another configurable delay):** If still unresolved, notify a trusted neighbor or caretaker via email and SMS.

Without escalation, that 2 AM leak notification might sit unread until morning. With a well-configured chain, someone in your household or support network will know about it — even if the first person misses the alert.

## Tips

- **Put the most likely responder in the first step.** They get the notification immediately and can resolve the alarm before anyone else is disturbed.
- **Use different channels for different steps.** If the first step sends email and the second sends SMS, you increase the chance that someone actually sees the notification.
- **Keep escalation chains short and purposeful.** Two or three steps cover most home scenarios. Each step should reach someone who can actually act on the alarm.
- **Test your escalation.** Trigger a test alarm and walk through the chain to make sure each step reaches the right person through the right channel.
