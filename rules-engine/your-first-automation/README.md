---
description: A ten-minute tutorial to build your first automation — a basement humidity alert, from blank canvas to working rule.
---

# Build Your First Smart Home Rule

The best way to learn how automations work is to build one. In this tutorial, you will create a simple automation that watches a humidity sensor in your basement and raises an alert when the reading gets too high.

By the end, you will have a complete automation that:

1. Listens for humidity readings from a basement sensor
2. Checks whether the humidity is above 70%
3. Raises an alert if it is, or does nothing if the reading is normal

Do not worry about getting everything perfect on your first try. You can always edit your automation later, undo changes, or restore a previous version. The editor saves your work automatically, and nothing runs in your home until you explicitly build and deploy it.

## What You Will Need

- A sensor already registered in Chirp (any humidity or temperature sensor will do — the steps are the same regardless of sensor type)
- An alert rule set up in the [Alerts](../../alarm/) section (the automation will trigger this alert when the condition is met)

If you do not have an alert rule yet, you can still follow along and add it later.

## The Three Steps

We will build this automation in three short steps:

1. **[Create an Automation](create-an-automation.md)** — Open the editor, name your automation, and choose which sensor to watch.
2. **[Add Conditions and Branches](add-conditions-and-branches.md)** — Set up a decision point that checks the humidity level and routes to different actions depending on the reading.
3. **[Trigger Alarms and Actions](trigger-alarms-and-actions.md)** — Connect your conditions to an alert so Chirp notifies you when something needs attention.

Each step builds on the previous one, so follow them in order. The whole process takes about ten minutes.
