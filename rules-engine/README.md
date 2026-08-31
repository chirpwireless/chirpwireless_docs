---
description: Let your home act on its own — automations that watch your sensors and respond, from an alert to flipping a switch.
---

# Make Your Home Work for You

Your sensors are always listening — temperature shifts, doors opening, moisture creeping into the basement. Automations let your home **react** to those readings on its own. Instead of checking the dashboard yourself, Chirp watches for the conditions you care about and takes action the moment they happen.

An automation is a set of instructions you build once: "when this sensor reads something I care about, do this." And "do this" now really means *do*. An automation can send you a notification when the basement gets too humid — or it can switch the dehumidifier on by itself; it can warn you about a leak, or shut the water off the moment the sensor gets wet. Your home doesn't just tell you something's happening anymore — it can handle it. See [When an Automation Runs a Command](reference/automation-runs-a-command.md).

## What You Get

**A visual workflow designer.** Every automation is a visual flowchart built using BPMN (Business Process Model and Notation), an industry-standard way to represent workflows. You can see the entire chain of "if this, then that" at a glance. Drag nodes onto a canvas, connect them with arrows, and watch your logic take shape. Most home automations can be built this way without writing traditional code.

**Smart expressions with CEL.** When simple thresholds are not enough, you can write conditions using [CEL](https://cel.dev) (Common Expression Language) — a safe, sandboxed expression language for precise logic inside the visual workflow. CEL lets you combine sensor values, compare readings from different rooms, calculate differences between indoor and outdoor temperatures, classify readings into severity levels, and build exactly the logic you need. That means Chirp is not limited to simple "if value > X" rules — you can model sophisticated home automations with branching, fallbacks, and dynamic alert messages.

**Your home can act, not just alert.** An automation doesn't have to stop at telling you something's wrong — it can do something about it. With an Execute Command step it can flip a switch, dim a light, or nudge the thermostat on its own, the moment a condition is met. "If the basement gets damp, turn on the dehumidifier" is a single automation now, start to finish. See [When an Automation Runs a Command](reference/automation-runs-a-command.md).

**Build before it goes live.** Nothing runs until you say so. After designing your automation, you build and deploy it explicitly. This means you can experiment freely in the editor without worrying about accidentally triggering alerts or actions in your home.

**Version history and easy recovery.** Every save is recorded. If you change something and your automation stops behaving the way you want, you can look back at previous versions and restore any one of them. Your saved work is always recoverable.

## How Automations Fit Together

Automations sit between your sensors and what happens next. A Start Event can run on every reading from one sensor, or it can wait for a saved trigger condition that watches one or several devices. When the selected source fires, the automation takes action—sending an alert, controlling a device, or both.

```
Sensor reading or trigger signal arrives
       |
  Automation evaluates conditions
       |
  Conditions met? --> Send an alert  and/or  run a command on a device
       |
  Not met? --> No action, wait for next reading
```

You choose the Start source, define the conditions, and decide what happens—an alert, an action on a device, or both. Chirp handles the rest around the clock. See [Triggers](going-deeper/triggers.md) when a condition should wait or apply to several devices.

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
