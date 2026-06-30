---
description: Let a Chirp automation act on its own — the Execute Command step sends a device a command when conditions are met.
---

# When an Automation Runs a Command

This is a big one. Until now, when an automation noticed something, the most it could do was *tell* you — send an alert and leave the doing to you. The **Execute Command** step changes that. Your automations can now *act*: flip a switch, dim a light, nudge the thermostat, all by themselves, the instant the conditions you set are met.

Think about what that unlocks. Before, "the basement is damp" got you a notification — and then you went down and switched on the dehumidifier yourself. Now the automation can turn the dehumidifier on for you, the moment the humidity climbs. A leak under the sink used to mean a frantic dash to the stopcock; now the automation can shut the water off the second the sensor gets wet, then tell you it did. Too hot in the nursery? The fan comes on by itself. Your home stops just warning you about things and starts handling them.

It all runs on the same [device controls](../../devices/commands/) you already use by hand — the automation just presses one of the buttons you've already set up. So everything that keeps manual controls safe and tidy (sensible value limits, a check that it really happened, a history of every action) applies here too.

## Before you start

The Execute Command step runs a command your device **already has**. It doesn't create new ones. So first:

1. **The device has to be controllable** — connected over Zigbee/MQTT, or a Class C LoRaWAN device (those listen all the time, so they're always ready to receive a command).
2. **The device needs at least one command set up** — do that on the device's **Commands & States** tab first. See [Setting up a command](../../devices/commands/creating-commands.md).
3. **You have permission to control it** — same as your home's sharing settings.

If a device doesn't have any commands yet, there'll be nothing to run — set the command up first, then come back to your automation.

## Adding an Execute Command step

1. Open your automation in the [Visual Editor](visual-editor.md) and switch to **Editing**.
2. Drag **Execute Command** from the palette onto the canvas. It sits with the other action steps, like Set Alarm.
3. Wire it into your flow. Usually it comes after a gateway: the automation checks a condition, and the branch that means "do it now" leads into the Execute Command step.
4. Click the step to open its settings and fill in the fields below.
5. Click **Save**, then **Build** and switch the automation on. Nothing is sent until the automation is built and running.

## What you fill in

| Field | What it's for |
|---|---|
| **Name** | A label for the step. Leave it blank and pick a command, and it fills in with the command's name. Example: "Turn on dehumidifier". |
| **Device** | A search box listing your devices. Pick the one you want the automation to control. |
| **Command** | A list of that device's commands. It wakes up once you've picked a device, then shows everything the device can do. |
| **Parameters** | Shows up once you pick a command, with a row for each thing the command needs (a brightness level, a target temperature, on or off). Each one is either a fixed **Value** or an **Expression** — see below. |
| **Inputs / Outputs** | Optional, for advanced setups — named expressions if you want to prepare or pass along values. Most home automations don't need these. |

There are **Save** and **Cancel** buttons at the bottom.

### Fixed value, or worked out on the fly

For each thing the command needs, you choose how to fill it in:

* **Value** — a fixed setting you type in. Use this when it's always the same: turn the plug `on`, set brightness to `30`, target `21` degrees. Chirp checks it's a sensible value (in range, right kind of thing) before it'll let you save.
* **Expression** — a little [CEL](cel-for-home-automations.md) formula worked out when the automation runs. This is where it gets clever: the reading that set the automation off is available as `vars.value`, so the command can respond to *how* things are — turn the fan up higher the hotter it gets, instead of just on or off.

Put together, it's lovely and flexible: a gateway decides *whether* to act, and an expression decides *how much* — so one automation can both react and respond in proportion.

## What happens when it runs

1. The automation reaches the Execute Command step.
2. Each setting is worked out — fixed values as-is, expressions calculated from the current reading.
3. The command is sent to the device, over Zigbee/MQTT or LoRaWAN, exactly as if you'd pressed it yourself.
4. It's logged in the device's history with how it went (sent, confirmed, delivered, or didn't work), so you can always see what your home did and when.

Because it goes through the normal controls, any "check it actually worked" you set up on that command applies here too. See [Making sure it worked](../../devices/commands/verification.md).

## Doing *and* telling, together

Acting doesn't mean you stop getting told. The best automations do both — shut the water off **and** send you an alert, so the problem is handled *and* you know about it. A common shape:

| Step | Node | What it does |
|---|---|---|
| Notice | Start Event → Gateway | Watch the leak sensor; branch when it gets wet |
| Act | Execute Command | Send "turn off" to the water shutoff |
| Tell | Set Alarm | Fire a Critical alert so you know the water was shut off and why |

If the action itself might miss — say the device is briefly offline — attach a [Boundary Error Event](automation-node-guide.md#boundary-error-event) to the Execute Command step and send the error path to a Set Alarm, so you still hear about it if the command doesn't go through.

## A home example

Keep the basement dry, hands-free. The Start Event watches the basement humidity sensor. A gateway routes any reading above 70% down a "too damp" branch. On that branch:

1. An **Execute Command** step sends "turn on" to the dehumidifier's smart plug.
2. A **Set Alarm** step sends you a gentle heads-up that the dehumidifier kicked in — no action needed from you, just good to know.

The damp gets dealt with the moment it shows up, and you're kept in the loop. That's the difference between a home that nags you and one that quietly looks after itself.

## Related pages

* [Controlling Your Devices](../../devices/commands/) — set up the commands an automation can run, and run them yourself
* [Automation Node Guide](automation-node-guide.md) — every node, including Execute Command, in detail
* [CEL for Home Automations](cel-for-home-automations.md) — the formulas behind dynamic values
* [Control widget](../../dashboards/adding-widgets/control-widget.md) — the same controls, right on your dashboard
