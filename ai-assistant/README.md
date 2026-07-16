---
description: The Chirp AI Helper knows your home and sets up sensors, automations, and alerts for you — all in plain language.
---

# Your Home AI Helper

Smart homes are supposed to be simple, but setting one up rarely feels that way — there's jargon, fiddly settings, and a different app for everything. Chirp's AI Helper fixes that by putting a friendly smart-home expert right inside the app. You talk to it like a person, and it gets things done.

It knows your home inside out — every sensor, every reading, the whole history — so it can answer "is the back door shut?" in a heartbeat. And it goes further: ask it to add a sensor, set up an automation, or create an alert, and it'll actually do the work, showing you what it's about to change and waiting for your OK first. Open it from **AI Chat** in the sidebar.

<figure><img src="../.gitbook/assets/ai-assistant.jpg" alt="The Chirp AI Helper ready to set up sensors, automations, and alerts"><figcaption></figcaption></figure>

## More than a chat box

Plenty of apps have a chat bubble that spits out canned answers. Chirp's helper is different in three ways that matter:

**It actually knows your home.** Its answers come from your real sensors and your real history — checked the moment you ask — not from generic guesses. If it can't find something, it says so instead of making it up. That's what makes it safe to rely on.

**It rolls up its sleeves.** This is the big one. The helper doesn't just tell you *how* to set up an automation — it can build it for you, write the logic, test it, and switch it on. It can walk you through adding a new sensor, and create an alert that pings you when something's wrong. You describe what you want; it handles the how.

**It remembers, and it always asks first.** It keeps track of your conversation so you can refine things ("make that 10 minutes instead") without starting over. And before anything important or permanent — like deleting a device or an automation — it stops and asks you to confirm. Nothing big happens without your say-so.

## What it can do for you

* **Answer anything about your home** — live readings, which sensors are online, yesterday's trends — and draw you a chart on the spot. See [Talking to Your Home](talking-to-your-home.md).
* **Set things up for you** — add a sensor, build and switch on an automation, create an alert. See [Let the Helper Set It Up](let-ai-set-it-up.md).
* **Explain how Chirp works** — it searches the help guides and trusted smart-home know-how to walk you through anything. Built on [what it knows](what-it-knows.md).

## One thing to know

The helper answers questions about your home and builds your automations for you. And automations can now do more than warn you — a rule can flip a switch on a device all by itself when something happens (see [When an Automation Runs a Command](../rules-engine/reference/automation-runs-a-command.md)). So *"if the basement gets damp, turn on the dehumidifier"* is something it can set up — not just *"tell me about it."* For flipping a switch yourself, right now, there's still [Device Commands](../devices/commands/) — on the device or a dashboard [Control widget](../dashboards/adding-widgets/control-widget.md). And as always, before anything important it shows you what it'll do and waits for your OK.

It also keeps to the basics you'd expect: it only ever works with your home, never anyone else's, and it never touches passwords or billing. See [Your Privacy](your-privacy.md).

## Availability

The helper comes with your Chirp plan, with a monthly number of requests included; higher plans include more. If you'd rather not worry about the limit, you can connect your own AI key and keep chatting. You'll see how many requests you have left above the message box.

Prefer your own AI app? You can connect one — like Claude Code or Claude Desktop — straight to your home, sign in with your usual Chirp account, and ask it the same things from your desktop. See [MCP Server](../api/mcp-server.md).

Everything above works today, and the helper keeps getting smarter the more it's used — the brains behind it run on an engine we built ourselves and improve all the time. We've even shared it openly as [Synthetic Brew](https://github.com/syntheticinc/syntheticbrew), for anyone curious about how it works under the hood.
