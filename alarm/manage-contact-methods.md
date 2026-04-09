# Manage Contact Methods

When Chirp detects something that needs your attention, it sends a notification to the contact methods you have set up. Right now, that means email — and you can add addresses for everyone in your household who should be in the loop.

This page covers adding, verifying, and removing email contacts, as well as enabling or disabling delivery.

## Where to Find Contact Settings

Open **Notifications** from the sidebar and switch to the **Settings** tab at `/notifications/settings`.

## Email — Your Primary Contact Method

The **EMAIL NOTIFICATIONS** section manages your email contacts and controls whether email delivery is active.

### How Contacts Are Organized

Your first email address is your **primary contact**. It appears as the default destination — shown as *"Send e-mail to [address]"* — and does not have the same edit and remove controls as additional contacts.

Additional contacts (up to **4 total**) appear below the primary and each has its own edit and remove actions.

### Adding an Email Address

Click **Add e-mail address** (or **Add one more e-mail address** if you already have contacts) to add a new address.

After adding an address, Chirp shows an **"E-mail verification required"** warning explaining that a verification link was sent. The person who owns the address needs to click the link in that email to confirm.

If the verification email does not arrive, click the **Resend link** action in the warning to send it again.

**Common situation:** You add your partner's email while setting up an alert. The address appears in your contacts immediately, but it will not actually receive notifications until your partner clicks the verification link. A quick text message reminding them to check their inbox can save some confusion.

### Removing an Email Address

Click the remove action next to a secondary contact. Chirp asks to confirm:

> *"Remove e-mail address"*
> *"Are you sure you want to remove [address]? This e-mail address will no longer receive notifications."*

Click **Yes, remove** to confirm, or **No, cancel** to keep it.

The primary contact does not have a remove button — only additional contacts can be removed.

### Turning Email On or Off

The email section has an **On/Off toggle** at the top. When you turn email off, a confirmation asks:

> *"Are you sure you want to turn off e-mail?"*
> *"You will not receive any e-mail."*

Click **Yes, turn off** to confirm, or **No, cancel** to keep it active.

Turning off email stops **all** email notifications from **all** alert rules — not just one rule. This is a global switch. If you want to stop notifications from a specific rule, it is better to disable that individual rule from the Rules tab.

## SMS — Coming Soon

{% hint style="info" %}
**Text message alerts are not available yet.** The SMS section shows a **"Coming soon..."** badge. When this feature becomes available, you will be able to add phone numbers and receive text alerts alongside email.
{% endhint %}

## Selecting Contacts When Creating Alert Rules

The contacts you manage here become available when creating or editing alert rules. For the full recipient selection flow, see [Set Up a Home Alert](set-up-a-home-alert.md).

## Tips

- **Complete verification promptly.** An unverified address shows a warning in the Settings tab with a **Resend link** action. If a family member's address is not verified, notifications will not reach them as expected.
- **Use separate addresses for different household members.** Rather than sending every alert to one shared family email, give each person their own contact. Then you can choose who gets notified for what — maybe water leak alerts go to everyone, but garden moisture alerts only go to the person who tends the plants.
- **Review contacts when household members change.** If a roommate moves out or a family member changes their email, update the contacts here so alerts keep reaching the right people.
