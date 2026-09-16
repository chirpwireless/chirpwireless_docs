---
description: Let your home act on its own — automations that watch your sensors and respond, from an alert to flipping a switch.
---

# Make Your Home Work for You

An **automation**, called a **rule** in Chirp, is a set of saved steps that responds to a sensor reading or a monitored condition. It can decide whether to alert someone, fetch another reading for context, or send a command to a device you have set up to control.

For example, an automation can raise an alert when basement humidity is high. With a compatible smart plug and a saved command, it can also request that a dehumidifier turns on. A sent command is not proof that the appliance started; [command verification](../devices/commands/verification.md) explains how to check reported feedback.

A **trigger** watches for the condition, such as a window left open for ten minutes. The **rule** contains the response steps. You save them separately in the **Triggers** and **Rules** tabs under **Rules Engine**, then connect them. Saving a trigger alone does not set up a response. [Learn how triggers and rules fit together](going-deeper/triggers.md#is-a-trigger-the-same-as-a-rule).

## What You Get

**A visual workflow designer.** Every automation is a visual flowchart built using BPMN (Business Process Model and Notation), an industry-standard way to represent workflows. You can see the entire chain of "if this, then that" at a glance. Drag nodes onto a canvas, connect them with arrows, and watch your logic take shape. Most home automations can be built this way without writing traditional code.

**Smart expressions with CEL.** When simple thresholds are not enough, you can write conditions using [CEL](https://cel.dev) (Common Expression Language) — a safe, sandboxed expression language for precise logic inside the visual workflow. CEL lets you combine sensor values, compare readings from different rooms, calculate differences between indoor and outdoor temperatures, classify readings into severity levels, and build exactly the logic you need. That means Chirp is not limited to simple "if value > X" rules — you can model sophisticated home automations with branching, fallbacks, and dynamic alert messages.

**Your home can act, not just alert.** An automation doesn't have to stop at telling you something's wrong — it can do something about it. With an Execute Command step it can flip a switch, dim a light, or nudge the thermostat on its own, the moment a condition is met. "If the basement gets damp, turn on the dehumidifier" is a single automation now, start to finish. See [When an Automation Runs a Command](reference/automation-runs-a-command.md).

**Build before it goes live.** Nothing runs until you say so. After designing your automation, you build and deploy it explicitly. This means you can experiment freely in the editor without worrying about accidentally triggering alerts or actions in your home.

**Version history and easy recovery.** Every save is recorded. If you change something and your automation stops behaving the way you want, you can look back at previous versions and restore any one of them. Your saved work is always recoverable.

## How Automations Fit Together

Automations sit between your sensors and what happens next. A Start Event can run on every reading from one sensor, or it can wait for a saved trigger condition that watches one or several devices. The automation must be running, and its schedule and execution-rate limits determine whether it processes each reading or trigger signal. An active trigger can signal again, so its response may repeat.

```
Sensor reading or trigger signal arrives
       |
  Automation evaluates conditions
       |
  Conditions met? --> Send an alert  and/or  run a command on a device
       |
  Not met? --> No action, wait for next reading
```

You choose the Start source, define the conditions, and decide what happens—an alert, an action on a device, or both. Chirp handles the rest around the clock. See [Triggers](going-deeper/triggers.md) to check a condition before starting the response, immediately or after a wait, for one device or several.

## Getting Started

This section walks you through everything from your very first automation to advanced patterns:

- **[Your First Automation](your-first-automation/)** — A hands-on tutorial that takes you from a blank canvas to a working humidity alert in minutes. Start here.
- **[Going Deeper](going-deeper/)** — Learn how to pull data from multiple sensors, write richer expressions, and publish your automation so it runs on live data.
- **[Managing Automations](managing-automations/)** — Keep things organized with version history, editing controls, and recovery options.
- **[Examples](examples/)** — Ready-to-adapt automation ideas for comfort, energy, and safety around the home.

## Finding the Automation Page

In the Chirp sidebar, click **Rules engine**. This opens the automation page at `/rules`, where all your automations live. From here you can create new automations, manage existing ones, check what is running, and browse the trash for anything you have deleted.

## Looking something up?

If you need to check how a specific node works, what a CEL expression does, or what a build error means, head to the [Reference](reference/README.md) section.
