---
description: Add a Set Alarm node and a motivation message so your automation notifies you when the basement gets too humid.
---

# Send Alerts and Run Actions

Your automation can now tell the difference between a normal humidity reading and a high one. The last piece is connecting the "high humidity" path to an action that actually notifies you. In this step, you will add a Set Alarm node so Chirp sends an alert when the basement gets too humid.

## Before you start: create an alarm definition

The Set Alarm node triggers an existing **Alarm Definition** — it does not create one from scratch. Before continuing, make sure you have at least one alarm definition configured in the [Alarm](../../alarm/) section.

If you already created an alarm definition for basement humidity, select it here. Otherwise, follow [Set Up a Home Alert](../../alarm/set-up-a-home-alert.md) first. The automation will reference that alarm definition.

## Add a Set Alarm Node

1. From the palette, drag a **Set Alarm** node onto the canvas (it looks like a rounded rectangle with a bell icon).
2. Connect the "High humidity" path from your Exclusive Gateway to this Set Alarm node — draw an arrow from the gateway's high-humidity branch to the Set Alarm node.
3. Click the **Set Alarm** node to open its properties panel.

## Configure the Alarm

In the properties panel you will see a header that reads: **"Select an alarm. A new alarm can be created on the Alarms page."** This is a reminder that the Set Alarm node triggers an existing Alarm Definition — it does not define severity, notification channels, or escalation steps. All of that is configured once in the [Alarm](../../alarm/) section and reused by every automation that references it.

Fill in the following fields:

| Field | What to enter |
|---|---|
| **Name** | A label for this node on the canvas — for example, "Alert: high humidity" |
| **Choose Alarm** | A searchable autocomplete field — start typing an alarm name and select the one you created on the Alarm page. |
| **Motivation Message** | A multiline CEL expression that builds the notification text. The placeholder shows an example: `"Temperature is " + string(vars.temp) + " degrees"`. See below for more detail. |

### Writing a Motivation Message

The motivation message is what you (and anyone else in your household) will see when the alert arrives. The field is multiline, so you can write longer messages comfortably. This is one of the places where Chirp uses CEL inside the visual automation: the workflow stays drag-and-drop, but the message field can generate text dynamically from the live sensor data.

This tutorial uses a **Sensor reading** start, so its CEL expression can include the incoming value:

```cel
"Humidity is " + string(vars.value) + "% in the basement"
```

When the sensor reads 78%, the notification will say: **Humidity is 78% in the basement**

You can make the message as detailed as you like:

```cel
"Basement humidity reached " + string(vars.value) + "% — check for leaks or ventilation issues"
```

If you came from the [Triggers guide](../going-deeper/triggers.md), use a message such as `"Window left open: " + vars.device_name` instead. A **Trigger condition** start has no `vars.value`; the trigger has already checked its condition, so it does not need the humidity comparison from this sensor-based tutorial.

Click **Save** in the properties panel.

## Add an End Event After the Alarm

Every path in your automation needs to end somewhere. After the Set Alarm node, add an **End Event** so the automation knows this branch is complete.

1. Drag an **End Event** from the palette.
2. Connect the Set Alarm node to this End Event.

You can name the End Event by clicking it and typing a label like "Alert sent" in the properties panel. This is optional but makes the diagram easier to read.

## The Complete Automation

Your finished automation looks like this:

```
Start Event (Basement Humidity Sensor)
       |
  Script Task ("Classify reading")
       |
  Exclusive Gateway
      / \
     /   \
  [High]  [Normal - Default]
    |         |
 Set Alarm   End Event
 ("Alert:     ("No action")
  high
  humidity")
    |
 End Event
 ("Alert sent")
```

For a reading processed by the running automation:

- If humidity is above 70%, the automation takes the left path, raises the alarm. Its delivery settings determine who receives a notification and when.
- If humidity is at or below 70%, the automation takes the right path and ends quietly.

## Save and Review

Click **Save** to persist your work. Take a moment to look at the diagram — can you follow the logic from start to finish? Are both paths connected to End Events? Do the labels make sense?

This is a good time to double-check the gateway conditions: click the Exclusive Gateway and verify the condition on the "High humidity" flow is `vars.level == "high"` and the "Normal" flow is set as the default.

## What Happens Next: Building and Deploying

Your automation is saved, but it is **not running yet**. Saving keeps your design safe in Chirp — it does not start processing live sensor data.

To make your automation live:

1. Click the **Build** button to validate your automation and create a deployable artifact
2. Deploy the artifact so it starts evaluating incoming sensor data

This build-before-deploy approach means you can freely experiment in the editor without worrying about triggering accidental alerts. When you are confident the automation is correct, you publish it.

The full walkthrough for building and deploying is in [Publish and Run an Automation](../going-deeper/publish-and-run-an-automation.md).

## You Did It

You have built a complete automation from scratch — one that watches a real sensor, evaluates a condition, and raises an alert when something needs your attention. From here, you can:

- **[Go deeper](../going-deeper/)** — Learn how to pull data from multiple sensors, write richer expressions, and manage the build-deploy lifecycle.
- **[Browse examples](../examples/)** — See ready-made automation ideas for comfort, energy, and safety around the home.
- **Edit and improve** — Your automation is saved and versioned. Come back anytime to adjust thresholds, add more branches, or change the alert message.
