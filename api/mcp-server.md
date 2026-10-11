---
description: Connect your favorite AI app straight to your Chirp home with MCP — sign in, no API key needed.
---

# MCP Server

You can ask the AI app you already use to help set up your Chirp home. Connect it through **MCP**, then ask it to add a sensor, create an alert, or build an automation. It can make those changes in your home rather than just describe the steps.

**MCP (Model Context Protocol)** is the connection that lets an AI client find and call Chirp's operations. Sign in with your Chirp account and work within the home and permissions you already have. Reading sensor history is available alongside the setup work.

You can bring [Claude Code](https://claude.com/claude-code), Claude Desktop, ChatGPT, Codex, Cursor, or Grok to your home through this connection.

Because MCP is a shared standard rather than a deal with one company, that list keeps growing. If your AI app supports MCP, it can talk to your home.

The best part: there's no key to generate, copy, or paste. You sign in with your usual Chirp account in your browser, and the connection carries exactly your own permissions — nothing more. If you can't see something in the Chirp app, your AI app can't see it either.

## The address to connect to

```
https://mcp-auth.chirpwireless.io/mcp
```

The connection uses Streamable HTTP, which the clients below handle for you — you just paste the address.

## Connecting Claude Code

1. Add Chirp as a connection:

   ```
   claude mcp add --transport http chirp https://mcp-auth.chirpwireless.io/mcp
   ```

2. Run `/mcp` inside Claude Code. Your browser opens for sign-in.
3. Sign in with your usual Chirp account and approve the connection.
4. Back in Claude Code, `/mcp` now shows Chirp as connected — and the tools are there. Try asking it which of your sensors went quiet this week.

## Connecting Claude Desktop

1. Open **Settings** → **Connectors**.
2. Click **Add custom connector**.
3. Paste `https://mcp-auth.chirpwireless.io/mcp` as the address.
4. Click **Connect**. Your browser opens for sign-in.
5. Sign in with your usual Chirp account.
6. Check the connector shows as active in the Connectors list. You're done — start a chat and ask it about your home.

## Connect Grok

Grok can answer questions about your Chirp home and switch connected devices on or off. Set up the connection on your phone or computer; you can use it without owning a car.

1. Open [Grok Connectors](https://grok.com/connectors) and sign in to your Grok account.
2. Choose **New Connector**, then **Custom**.
3. Paste `https://mcp-auth.chirpwireless.io/mcp` into the server URL field.
4. Follow the sign-in prompt, use your usual Chirp account, and approve the connection. There is no Chirp or xAI API key to enter.
5. In a Grok conversation, ask *“Use Chirp to tell me which home is selected and list my devices.”* Make sure it sees the home you intended.
6. Ask about a reading, such as *“What is the living room temperature, and how recent is it?”* To try control, ask which commands are saved for a named plug or lamp, then ask Grok to run one.

[Grok's connector guide](https://docs.x.ai/grok/connectors) describes the custom connection flow. If you use a Grok Business or Enterprise account, your team administrator must add the connector first; see [the administrator instructions](https://docs.x.ai/grok/connector-management).

A device needs mapped readings to answer a question about its state. For switching, first save the device's supported actions under **Commands & States** in Chirp; [Creating Commands](../devices/commands/creating-commands.md) explains how. Grok can use those actions with your permissions. Its confirmation prompts belong to Grok, so the wording may differ from Chirp's built-in assistant.

Once this works, the same Grok account can bring your home into a voice conversation in the car. See [Use Chirp from Your Tesla](../ai-assistant/tesla-grok.md).

## Connecting a different AI app

ChatGPT, Codex, Cursor and the rest work the same way — they just put the setting in a different place. Look for **Connectors**, **Integrations**, or **MCP servers** in your app's settings, choose whatever it calls "add a custom server", and paste the same address. If your app is configured from a file or a terminal instead, add the address as a **Streamable HTTP** server.

Whichever app you use, the rest is identical: your browser opens, you sign in as yourself, and it sees exactly what you see. Your app's own documentation will tell you where its MCP setting lives.

## Choosing which home it sees

If you're only in one home, skip this — everything just works.

The plain `/mcp` address checks which home is selected in Chirp on every request. After switching homes, ask your AI app to check the selected home before continuing. There is no need to reconnect.

If you'd rather pin the connection to a specific home — handy if you look after a holiday flat as well as your own place, and want each AI client fixed to one — use the address with the home's ID in it:

```
https://mcp-auth.chirpwireless.io/o/{organizationId}/mcp
```

You'll find the ID for a home in the Chirp web app. You can only connect to a home you're a member of; anything else is refused.

## What your AI app can do

Once connected, your AI client can work across your home on your behalf. Here's what it can reach:

| Area | What your AI app can do |
|---|---|
| **Sensors** | List the sensors in your home, see their details, and add a new one for you — a LoRaWAN sensor or a tracker — picking from the available sensor profiles. |
| **Readings** | Read mapped measurements, such as room temperature or a smart plug's reported on/off state. |
| **Switching things on or off** | Run a command already saved on a device and check its execution status — for example, ask it to turn off a connected plug. Device confirmation depends on the hardware and configured verification. |
| **Pretend sensors** | Set up an emulated sensor, change what it reports, send a one-off reading to test an alert, and move a sensor between pretend and real. It can put any of your real sensors onto the emulator, and take a pretend one live onto a LoRaWAN connection. |
| **Connections** | See how your home is connected and set up a new connection for a sensor. |
| **Automations** | Go through the automations you've built and tell you what each one does. |
| **Alerts** | Look at your alerts, summarize what's been triggering and how often, clear one that you've dealt with, and set up which alerts reach you and where. |
| **Dashboards** | List your dashboards and inspect which readings their widgets are configured to show. |
| **History** | Look back over when your alerts fired and when your automations ran, and map out which sensor is measuring what. |
| **Household** | Look up your home's details and members, invite someone new, and set what they're allowed to see. |

Everything it does runs with your permissions. For destructive or important actions, Chirp supplies safety information that a compatible AI app can use to ask before it continues.

## If something is missing

If Grok sees the wrong devices, check [which home is selected](#choosing-which-home-it-sees). If a reading is missing or old, open the device in Chirp and check its mapping and last update. A missing action needs to be saved under **Commands & States**, with permission for your account to use it.

If a command is accepted or queued, ask Grok to check its status again. The request has entered the delivery process; the plug's reported state or [command verification](../devices/commands/verification.md) tells you the result.

## How your AI app knows what an action does

Chirp publishes a readable name, description, and safety notes with each action. AI apps that support these notes can use them to decide whether to run an action immediately or ask you to confirm.

| Safety note | Examples | What it tells the app |
|---|---|---|
| **Only reads** | List sensors, read alert history, inspect widget settings | The action does not change your home. |
| **Changes or removes something** | Remove a sensor, switch a device, change a connection, update alert recipients | The action can affect your home or equipment, so the app can ask for confirmation. |
| **Looks outside your home** | Search a product catalog or the web for hardware | The action accesses information beyond your Chirp data. |

Creating a sensor or dashboard changes your home, but it does not overwrite or switch off anything already there and can be reversed by deleting the new item. Chirp therefore does not describe creation as destructive.

These notes help the AI app explain an action; they are not permission checks. Each app decides how to present confirmations. Chirp still enforces your account permissions, so the app cannot do anything that your account is not allowed to do.

## How this differs from the AI Assistant in the app {#how-this-differs-from-the-ai-helper-in-the-app}

Chirp’s built-in [AI Assistant](../ai-assistant/README.md) works like an experienced integrator by your side. It can add sensors, build automations, and configure alerts from the home project you describe. Open it using **AI Chat** in the sidebar; you can start without connecting an external AI client.

MCP is for when you'd rather bring your own AI app to the same home — because you live in your desktop client all day, because you want your home's data in the same conversation as everything else you're working on, or simply because you prefer that assistant. Both talk to the same home and respect the same permissions.

## How this differs from the API

The [REST API](public-rest-api.md) is for code *you* write — a script that exports readings into a spreadsheet every Sunday, or a bridge to another home platform. It runs on a key you create in [Settings → API Keys](../settings/api-keys.md), with exactly the scopes you give it.

MCP is for an AI client acting **as you**, in a conversation, with your own sign-in and your own permissions. No key to manage, and nothing to write. If you want something to run unattended on a schedule, use the API. If you want to ask questions and get things done in the moment, use MCP.
