# Set Up a Home Alert

An alert rule tells Chirp exactly what to watch for on a sensor and who to notify when it happens. Once you have created a rule, it runs continuously — checking your sensor data and reaching out to you the moment something crosses the line you set.

This guide walks you through creating an alert from start to finish, managing the rules you have already created, and fine-tuning how often alerts repeat.

## Before You Start

You will need:

- **A sensor that is connected and sending data.** If you have not added one yet, follow [Connect Your First Sensor](../first-steps/connect-your-first-sensor.md).
- **At least one verified email address** in your notification contacts. Check the **Settings** tab in Notifications at `/notifications/settings`. If nothing is there, see [Manage Contact Methods](manage-contact-methods.md) to add one.

## Creating an Alert Rule

Open **Notifications** from the sidebar and switch to the **Rules** tab. Click **Add Rule** to start the guided setup.

### Pick Your Sensor

The first screen is titled **"1 / Choose a device"**. You will see your connected sensors listed. Tap the one you want this rule to watch — maybe the basement humidity sensor, or the front door contact sensor.

Click **Choose** to continue.

### Tell Chirp What to Watch For

The screen moves to **"2 / Add conditions to the device"** with the hint *"Select the conditions under which the trigger should occur."*

This is where you define the condition that matters. For example:

- Humidity **above 80%** (basement flood risk)
- Temperature **above 5°C** (fridge too warm)
- Door status **equals "open"** (unexpected entry)

Set your condition and click **Continue**.

### Write the Alert Message

The screen shows **"3 / Set up alerting message"**. This is what you will see in your email when the alert fires. Make it clear enough that you will know exactly what is happening without opening the app.

Fill in:

- **Subject** — a short headline, e.g., *"Basement humidity is too high"*
- **Message** — a sentence or two with context, e.g., *"The humidity sensor in the basement is reading above 80%. Check for water leaks near the washing machine or sump pump."*
- **Notification type** — choose how urgent this alert is:

| Type | What it means | How often it repeats by default |
|---|---|---|
| **Critical** | Something that needs your immediate attention | Every hour |
| **Important** | Something you should know about soon | Every 4 hours |
| **Information** | Good to know, but not urgent | Once a day |

For a water leak sensor, **Critical** makes sense — you want to know right away and be reminded until you deal with it. For a garden moisture alert, **Information** is enough — a once-daily nudge is plenty.

Click **Continue**.

### Choose Who Gets Notified

The screen shows **"Select notification recipients"**. If you have one email contact, it is shown as your default recipient without a checkbox.

To choose from multiple contacts — for example, to also notify your partner — click **"Add email"**. This switches to multi-select mode where all your email contacts appear with checkboxes. Your first contact is automatically selected. Once in multi-select mode, click **"Add recipients"** if you need to enter a brand-new email address right here.

Verified contacts have active checkboxes. Unverified contacts appear with a disabled checkbox — they need to be verified first (see [Manage Contact Methods](manage-contact-methods.md)).

Click **Continue**.

### Name Your Alert

The final screen shows **"4 / Set up rule name and description"**. Give it a name you will recognize later in the list — something like *"Basement leak warning"* or *"Front door opened late at night."*

The description is optional, but handy if you have several similar alerts and want to remember why each one exists.

Click **Create rule**. You are taken back to the Rules list, where your new alert appears with its toggle switched on. It is now watching your sensor.

---

## Managing Your Alert Rules

Once you have created alert rules, you can manage them from the **Rules** tab at `/notifications/rules`. This section covers turning rules on and off, editing them, and deleting rules you no longer need.

Each rule in the list shows its name, description, connected sensor, alert type, and an on/off toggle.

### Turning an Alert On or Off

Flip the **status toggle** next to any rule to temporarily disable it without losing the configuration. Flip it back to resume. Useful if a sensor is being moved or serviced and you do not want false alerts.

### Editing a Rule

Click the actions menu on a rule and choose **Edit**. A dialog titled **"Edit rule details"** appears asking *"Select the section you want to edit."* Pick what you want to change:

- **Conditions** — change what the rule watches for
- **Notification details** — update the message, subject, or alert type
- **Notification recipients** — change who gets notified
- **Name and description** — rename or re-describe the rule

The editor opens directly at the section you chose. Make your changes and click **Save changes**.

### Deleting a Rule

Click the actions menu and choose **Delete**. Chirp asks: *"Are you sure you want to delete the rule?"* and notes that *"Once deleted, all connected devices will no longer follow this rule."* Click **Yes, delete** to confirm.

### When the List Is Empty

If you have not created any rules yet, you will see *"There is no rule yet"* with a friendly prompt to add your first one.

---

## Fine-Tune How Often Alerts Repeat

After setting up your rules, you may want to adjust how frequently Chirp reminds you about active alerts. The default repeat intervals (hourly for Critical, every 4 hours for Important, daily for Information) work well for most homes. But if you want to adjust them — maybe you want Important alerts every 2 hours instead of 4, or Information alerts every other day — you can change the global timing.

### How to Open the Timing Settings

In the Notification Center, look for the **"Notification types settings"** button. On desktop, it is in the page header and visible from the Inbox, Rules, and Settings tabs. On smaller screens, it is available at the bottom of the Inbox and Rules tabs.

Clicking it opens a popup with three sections:

- **Critical Notification interval**
- **Important Notification interval**
- **Information Notification interval**

### Changing the Repeat Interval

For each type, you can set:

- **How often** — a number plus a unit (**Hours** or **Days**). For example, "2 Hours" means Chirp re-sends the notification every 2 hours while the alert is still active.
- **One-time notification** — a toggle that tells Chirp to send just one notification and not repeat at all. Good for informational alerts where a single heads-up is enough.

### Overriding for a Specific Rule

You can also set a custom repeat interval on an individual rule. During rule creation or editing (in the alert message step), toggle **Custom Notification interval** to set an interval that applies only to that rule. This overrides whatever you have set in the global timing settings.

For example, you might keep Critical alerts at 1-hour globally but set your basement leak rule to repeat every 2 hours because that particular sensor is less urgent than a true emergency.

## Tips for Home Alerts

- **Start with one or two alerts and see how they feel.** It is easy to set up alerts for everything, but if your phone buzzes constantly, you will start ignoring them. Begin with the alerts that matter most — water leaks, security sensors, temperature extremes — and add more as needed.
- **Use Information type for nice-to-know alerts.** Garden moisture low? Good to know once a day. Front door opened at 2 AM? That deserves Critical.
- **Name alerts clearly.** When an alert fires while you are in the middle of something, the name in your email is all you see. *"Basement leak warning"* tells you what to do. *"Rule 3"* does not.
