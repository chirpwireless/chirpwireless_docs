# Create an Automation

This page walks you through opening the automation editor, naming your first automation, choosing the sensor that triggers it, and saving your initial draft.

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

## Choose Your Sensor

The Start Event is the trigger for your automation. It decides which sensor's readings will kick off the logic every time new data arrives.

1. Click the **Start Event** node on the canvas (the circle with the envelope icon).
2. A properties panel opens on the right side of the screen.
3. In the **Device** dropdown, search for and select the device you want to monitor (for our example, the basement humidity sensor).
4. In the **Sensor** dropdown, select the specific sensor on that device (this dropdown becomes available after you pick a device).

That is all you need for a basic trigger. Every time your basement sensor sends a new humidity reading, this automation will evaluate it.

At this stage, you are still working entirely visually. As you build more advanced automations, some fields let you add CEL expressions for precise conditions or message text, but most of the structure stays BPMN-based and easy to follow.

### Optional: Restrict When It Runs

If you only want this automation to run during certain hours — for example, only overnight when you are not home to check things yourself — toggle the **Enable Schedule** switch in the Start Event properties. You can pick a time range and time zone.

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

**Next:** [Add Conditions and Branches](add-conditions-and-branches.md)
