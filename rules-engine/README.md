---
description: Let your home react on its own — build visual automations that watch sensors and send alerts when something needs you.
---

# Make Your Home Work for You

Your sensors are always listening — temperature shifts, doors opening, moisture creeping into the basement. Automations let your home **react** to those readings on its own. Instead of checking the dashboard yourself, Chirp watches for the conditions you care about and takes action the moment they happen.

An automation is a set of instructions you build once: "when this sensor reads something I care about, do this." It could be as simple as sending you a notification when the basement gets too humid, or as layered as comparing indoor and outdoor temperatures before deciding whether to sound an alert.

## What You Get

**A visual workflow designer.** Every automation is a visual flowchart built using BPMN (Business Process Model and Notation), an industry-standard way to represent workflows. You can see the entire chain of "if this, then that" at a glance. Drag nodes onto a canvas, connect them with arrows, and watch your logic take shape. Most home automations can be built this way without writing traditional code.

**Smart expressions with CEL.** When simple thresholds are not enough, you can write conditions using [CEL](https://cel.dev) (Common Expression Language) — a safe, sandboxed expression language for precise logic inside the visual workflow. CEL lets you combine sensor values, compare readings from different rooms, calculate differences between indoor and outdoor temperatures, classify readings into severity levels, and build exactly the logic you need. That means Chirp is not limited to simple "if value > X" rules — you can model sophisticated home automations with branching, fallbacks, and dynamic alert messages.

**Build before it goes live.** Nothing runs until you say so. After designing your automation, you build and deploy it explicitly. This means you can experiment freely in the editor without worrying about accidentally triggering alerts or actions in your home.

**Version history and easy recovery.** Every save is recorded. If you change something and your automation stops behaving the way you want, you can look back at previous versions and restore any one of them. Your saved work is always recoverable.

## How Automations Fit Together

Automations sit between your sensors and your alerts. Your sensors send data to Chirp continuously. When a reading arrives, Chirp checks it against any running automations. If the conditions match, the automation takes action — usually raising an alert that sends you a notification.

```
Sensor reading arrives
       |
  Automation evaluates conditions
       |
  Conditions met? --> Raise alarm --> Notification sent to you
       |
  Not met? --> No action, wait for next reading
```

You build the automations. You choose the sensors, define the conditions, and pick the alerts. Chirp handles the rest — around the clock, whether you are home or away.

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
