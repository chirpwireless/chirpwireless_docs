---
description: Set up your smart home with an experienced helper beside you — add sensors, build automations, and configure alerts through conversation.
---

# Your Home AI Helper

Chirp's **AI Helper** is like having an experienced smart-home integrator beside you. Tell it what you want your home to do, and it can add sensors, build automations, and set up alerts for you. You bring the idea; the helper works through the configuration with you.

Connecting a home can mean learning unfamiliar radio types, device codes, and automation settings before anything useful happens. The helper explains the choices as you go and makes changes in Chirp, so *“help me monitor the basement”* can become a sensor, an alert, and an automation you can open and inspect.

Open **AI Chat** in the sidebar. Start with one job, such as adding a new temperature sensor or creating an alert when a connected door sensor reports open. The helper asks for missing details, and you can adjust the setup in the same conversation.

<figure><img src="../.gitbook/assets/ai-assistant.jpg" alt="The Chirp AI Helper ready to set up sensors, automations, and alerts"><figcaption></figcaption></figure>

## More than a chat box

**It does the setup with you.** Ask for an automation and the helper can write its logic, build it, switch it on, and test sample readings. It can register sensors and configure who receives an alert, rather than leave you to follow a list of settings yourself.

**You can start before the parcel arrives.** Ask for a pretend sensor, send a test reading, and try out the response. You can prepare the dashboard and automation while you are still choosing or waiting for hardware.

**You stay involved where it matters.** The conversation remembers what you are working on, so *“send that alert to my partner too”* builds on the existing task. Running a device command or deleting a sensor brings up a confirmation. Read the proposed action, then choose **Confirm Action** or **Cancel**.

## What it can do for you

* **Connect and configure** — add a sensor, choose its connection, map its readings, and check whether messages are arriving.
* **Make your home respond** — build an automation, create its alert, and refine the threshold or recipients in conversation. See [Let the Helper Set It Up](let-ai-set-it-up.md).
* **Prepare your views** — create dashboards and folders, arrange an existing dashboard's layout, and get guidance on which widgets suit your rooms. See [Prepare a dashboard](let-ai-set-it-up.md#prepare-a-dashboard).
* **Try an idea with pretend sensors** — generate readings and exercise an automation before connecting real hardware.
* **Operate a connected device** — run a saved command after confirmation, then inspect its status.
* **Understand what happened** — compare temperatures, explore a sensor's history, or find devices that stopped reporting. See [Talking to Your Home](talking-to-your-home.md).

The helper can explain saved triggers, but **cannot currently save or edit them in chat**. Set up that monitoring condition on the [Triggers page](../rules-engine/going-deeper/triggers.md); the automation is the response.

## One thing to know

The automation the helper creates is yours to inspect and adjust in the [Rules Engine](../rules-engine/README.md). You can follow its steps, test its decisions, and change the setup as your home changes.

For direct control, ask it to run a command already configured on a connected lamp or smart plug. It shows what it will send and waits for your confirmation. The reported result distinguishes command status from optional checks of the device's state. You can also use [Device Commands](../devices/commands/) or a dashboard [Control widget](../dashboards/adding-widgets/control-widget.md).

The helper uses your access to the home selected in Chirp. [Your Privacy](your-privacy.md) explains permissions, model providers, and saved conversations.

## Availability

The helper comes with your Chirp plan, with a monthly number of requests included; higher plans include more. If you'd rather not worry about the limit, you can connect your own AI key and keep chatting. You'll see how many requests you have left above the message box.

Prefer your own AI app? You can connect one — like Claude Code or Claude Desktop — straight to your home, sign in with your usual Chirp account, and ask it the same things from your desktop. See [MCP Server](../api/mcp-server.md).

The helper is powered by [SyntheticBrew](https://syntheticbrew.ai/), the AI agent runtime built by our team. In CHIRP, that runtime works with your home's device information and the actions available to your account. That connects the conversation to the setup work you can do in Chirp.
