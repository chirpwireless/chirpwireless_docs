---
description: Ask Chirp AI Chat about your sensors and use supported setup tasks for devices, alerts, and automations in your home.
---

# Your Home AI Helper

Chirp's **AI Helper** is the chat interface for asking about your sensors and getting help with supported setup tasks. It can look up readings, help add a supported sensor, create an alert definition, build an automation, or run a command already configured on a device.

Open **AI Chat** in the sidebar and describe the device or job. The helper uses the data and operations available through your account in the selected home's workspace. Check which sensor and time period an answer refers to before relying on it.

Some steps still need the interface. The helper **cannot currently save or edit a trigger**—the monitoring condition that can start an automation. It can explain the choices; you create the trigger in [Rules Engine → Triggers](../rules-engine/going-deeper/triggers.md).

<figure><img src="../.gitbook/assets/ai-assistant.jpg" alt="The Chirp AI Helper ready to set up sensors, automations, and alerts"><figcaption></figcaption></figure>

## More than a chat box

Plenty of apps have a chat bubble that spits out canned answers. Chirp's helper is different in three ways that matter:

**It can look up your sensor data.** Ask for a named sensor and time range so the helper can retrieve relevant readings. Check the timestamps and coverage in the result, especially if a sensor has stopped reporting.

**It rolls up its sleeves.** This is the big one. The helper doesn't just tell you *how* to set up an automation — it can build it for you, write the logic, test it, and switch it on. It can walk you through adding a new sensor, and create an alert that pings you when something's wrong. You describe what you want; it handles the how.

**It remembers, and it always asks first.** It keeps track of your conversation so you can refine things ("send that alert to my partner too") without starting over. And before anything important or permanent — like deleting a device or an automation — it stops and asks you to confirm. Nothing big happens without your say-so.

## What it can do for you

* **Answer questions about available home data** — live readings, which sensors are online, yesterday's trends — and draw you a chart on the spot. See [Talking to Your Home](talking-to-your-home.md).
* **Set things up for you** — add a sensor, build and switch on an automation, create an alert, or stand up a pretend sensor to try things with before your hardware arrives. See [Let the Helper Set It Up](let-ai-set-it-up.md).
* **Switch things on and off** — run a saved device command and inspect its status, after showing you what it's about to do. See [Ask It to Turn Things On](let-ai-set-it-up.md).
* **Explain how Chirp works** — it searches the help guides and trusted smart-home know-how to walk you through anything. Built on [what it knows](what-it-knows.md).

## One thing to know

The helper can operate your home, not just describe it. For a connected lamp with a saved command, ask *"turn on the lamp"*. The helper can run that command and report its available execution status (see [Ask It to Turn Things On](let-ai-set-it-up.md)). Automations can do the same on their own: a rule can flip a switch when something happens (see [When an Automation Runs a Command](../rules-engine/reference/automation-runs-a-command.md)), so *"if the basement gets damp, turn on the dehumidifier"* is something it can both set up and do. You can still press the button yourself any time from [Device Commands](../devices/commands/) or a dashboard [Control widget](../dashboards/adding-widgets/control-widget.md). And because switching something on is a real, physical thing to do, it always shows you what it's about to send and waits for your OK.

It also keeps to the basics you'd expect: it only ever works with your home, never anyone else's, and you should keep account passwords and unrelated secrets out of the conversation. See [Your Privacy](your-privacy.md).

## Availability

The helper comes with your Chirp plan, with a monthly number of requests included; higher plans include more. If you'd rather not worry about the limit, you can connect your own AI key and keep chatting. You'll see how many requests you have left above the message box.

Prefer your own AI app? You can connect one — like Claude Code or Claude Desktop — straight to your home, sign in with your usual Chirp account, and ask it the same things from your desktop. See [MCP Server](../api/mcp-server.md).

The helper is powered by [SyntheticBrew](https://syntheticbrew.ai/), the AI agent runtime built by our team. In CHIRP, that runtime works with your home's device information and the actions available to your account. A capability described on the runtime website is not automatically an action available for every home device.
