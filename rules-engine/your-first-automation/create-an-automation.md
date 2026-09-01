---
description: Open the editor, name an automation, choose a Sensor reading or Trigger condition start, and save the first version.
---

# Create an Automation

This page walks you through opening the automation editor, naming your first automation, deciding what starts it, and saving your initial draft.

## Open the Rules Engine

1. Click **Rules engine** in the Chirp sidebar. This takes you to `/rules`.
2. Click the **Add Rule** button. A new blank editor opens.

You are now looking at the visual workflow canvas — a large open area with a small palette of node types on the left. The canvas already contains a **Start Event** node (a circle with an envelope icon). This is where every automation begins.

## Name Your Automation

At the top of the editor, you will see a name field. Click it and type a name that tells you what this automation does — for example:

- "Basement Humidity Alert"
- "Living Room Temp Warning"
- "Garden Moisture Check"

You can also add a description: click the three-dot menu next to the name and select **Edit description**. This is optional but helpful if you have several automations and want to remember the purpose of each one.

## Choose What Starts the Automation

The **Start Event** is the automation's entry point. Its **Start source** offers two choices:

| Start source | Use it when |
|---|---|
| **Sensor reading** | One sensor should run the automation every time it reports. The normalized reading value is available as `vars.value`. |
| **Trigger condition** | Chirp should evaluate a saved condition first—immediately or after a wait, for one device or several devices. |

This tutorial uses **Sensor reading** for one basement humidity sensor:

1. Click the **Start Event** node on the canvas (the circle with the envelope icon).
2. A properties panel opens on the right side of the screen.
3. Set **Start source** to **Sensor reading**.
4. In **Device**, search for and select the basement sensor.
5. In **Sensor**, choose its humidity reading. This field becomes available after you pick the device.

Every time that sensor reports humidity, this automation will now start and evaluate the reading.

To start from a condition instead:

1. Leave the editor and open **Rules Engine → Triggers**.
2. Select **Add trigger**, configure and create the trigger, then return to the **Rules** tab.
3. Create a new automation or reopen this one in Edit mode.
4. Select the Start Event and use the pencil beneath it to open the properties panel.
5. Choose **Trigger condition**, select the saved trigger, and select **Save** at the bottom of the panel.
6. Save the automation separately from the editor toolbar, then build and deploy it when the workflow is complete.

The trigger selector does not create triggers, and a trigger is not a node in the palette. This path lets one automation cover several similar devices or ignore a condition that ends before its timer finishes. See [Triggers](../going-deeper/triggers.md) for the complete workflow.

At this stage, you are still working entirely visually. As you build more advanced automations, some fields let you add CEL expressions for precise conditions or message text, but most of the structure stays BPMN-based and easy to follow.

### Optional: Restrict When It Runs

If you only want this automation to run during certain hours—for example, overnight—turn on **Enable Schedule** in the Start Event and choose the days, time range, and time zone. Schedule limits the start source you selected; it is not a third source.

For now, leave the schedule off so the automation evaluates every reading around the clock.

## Save Your Work

Click the **Save** button in the top-right corner of the editor. Your automation is saved as its first version.

You will notice the editor shows a save indicator in the header area — it cycles through **Saving...** and then **Saved** to confirm your work is persisted. From this point on, Chirp also autosaves periodically while you are working, so you do not need to worry about losing progress if you step away.

## View Mode vs. Edit Mode

Now that your automation exists, there are two ways to look at it:

- **View mode** — Opens when you click an automation's name in the list. You can see the full diagram, inspect node properties, and browse version history, but you cannot change anything. This is useful for reviewing automations without accidentally modifying them.
- **Edit mode** — Opens when you click the **Edit** button or use the mode selector in the editor header. In this mode you can change the diagram, update properties, and save new versions.

While you are in edit mode, the automation is locked to you — nobody else in your household can edit it at the same time. The lock is released automatically when you leave the editor or when the session times out after inactivity.

## What You Have So Far

Your automation is saved and ready for logic. Right now it has a Start Event bound to your sensor — but it does not do anything with the data yet. In the next step, you will add a decision point that checks whether the reading is above your threshold.

For a full tour of the canvas, palette, and properties sidebar, see the [Visual Editor](../reference/visual-editor.md) reference.

**Next:** [Add Conditions and Branches](add-conditions-and-branches.md)
