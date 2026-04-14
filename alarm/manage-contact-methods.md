# Manage Contact Methods

When Chirp fires an alarm, notifications go to the contact methods you have set up. The **Settings** tab on the Alarm page is where you manage these contacts — add new ones, verify them, and remove ones you no longer need.

## Email

Email is the baseline notification channel — it is always available.

### Adding a contact

Click the add button to enter a new email address. Chirp sends a verification email immediately. The contact appears in your list with an unverified indicator until the recipient clicks the verification link.

### Verification

Each email address must be verified before it receives alarm notifications. Unverified contacts show a warning indicator. If a verification email was not received, you can resend it.

### Removing a contact

Click the remove button next to a contact to delete it. A confirmation dialog appears before the contact is removed. Your primary email contact (the first one in the list) cannot be removed.

Contacts cannot be edited after creation. To change an email address, remove the old one and add the new one.

## SMS

SMS notifications are available when enabled for your account. When available, the SMS section appears in the Settings tab with the same add, verify, and remove workflow as email.

## Push notifications

Push notifications are available when enabled for your account. When available, a push notification section appears at the top of the Settings tab with setup instructions.

## How contacts connect to alarms

The contacts you set up here are the people available in the **Choose recipients** dropdown when you configure [escalation steps](escalation-chains.md) in an alarm definition. Each escalation step can select different recipients and different channels, so you can route Critical alarms to one set of contacts and Low-priority alarms to another.
