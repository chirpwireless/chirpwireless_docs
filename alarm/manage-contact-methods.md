# Manage Contact Methods

When Chirp fires an alarm, notifications go to the contact methods you have set up. The **Settings** tab on the Alarm page is where you manage these contacts — add new ones, verify them, control which channels are active, and remove contacts you no longer need.

## Email

Email is the baseline notification channel.

### Enabling and disabling

An **On/Off** toggle at the top of the Email section controls whether email notifications are delivered. Turning it **Off** stops ALL alarm notifications via email — a confirmation dialog appears before this takes effect. Turn it back **On** to resume delivery. The toggle may be disabled if no email contacts are configured or if the channel is not available in the current account context.

### Adding a contact

Click the add button to enter a new email address. Chirp sends a verification email immediately. The contact appears in your list with an unverified indicator until the recipient clicks the verification link.

### Verification

Each email address must be verified before it receives alarm notifications. Unverified contacts show a warning indicator. If a verification email was not received, you can resend it.

### Removing a contact

Click the remove button next to a contact to delete it. A confirmation dialog appears before the contact is removed. Your primary email contact (the first one in the list) cannot be removed.

Contacts cannot be edited after creation. To change an email address, remove the old one and add the new one.

## SMS

SMS is present in the Alarm settings and selectable as a delivery channel in [escalation steps](escalation-chains.md). The SMS section works the same way as Email: add contacts, verify them, enable or disable the channel with the On/Off toggle, and remove contacts you no longer need.

Turning SMS **Off** stops all alarm notifications via SMS. The same confirmation dialog appears before disabling.

## Push notifications

Push notifications are available when enabled for your account. When available, a push notification section appears at the top of the Settings tab with setup instructions.

## How contacts and channels connect to alarms

The contacts you set up here are the people available in the **Choose recipients** dropdown when you configure [escalation steps](escalation-chains.md) in an alarm definition. Each escalation step can select different recipients and different channels, so you can route Critical alarms to one set of contacts and Low-priority alarms to another.

If you turn a channel **Off** in Settings, that channel is disabled for delivery across ALL alarm definitions and ALL escalation steps that use it. Turning the channel back On resumes delivery for all affected alarms.
