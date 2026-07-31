---
description: Connect your favorite AI app straight to your Chirp home with MCP — sign in, no API key needed.
---

# MCP Server

You've probably got an AI app you already like talking to. Chirp's MCP server lets you point that app at your own home, so you can ask it *"which sensors have stopped reporting?"* or say *"add this new sensor for me"* right where you're already working — and it can actually go and do it.

MCP (Model Context Protocol) is simply an agreed way for an AI app to reach out and use something else safely. Chirp speaks it, so the app you already use can connect to your home without any custom plumbing on your side — [Claude Code](https://claude.com/claude-code), Claude Desktop, ChatGPT, Codex, Cursor, and others all support it.

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

## Connecting a different AI app

ChatGPT, Codex, Cursor and the rest work the same way — they just put the setting in a different place. Look for **Connectors**, **Integrations**, or **MCP servers** in your app's settings, choose whatever it calls "add a custom server", and paste the same address. If your app is configured from a file or a terminal instead, add the address as a **Streamable HTTP** server.

Whichever app you use, the rest is identical: your browser opens, you sign in as yourself, and it sees exactly what you see. Your app's own documentation will tell you where its MCP setting lives.

## Choosing which home it sees

If you're only in one home, skip this — everything just works.

The plain `/mcp` address follows whichever home is currently selected in the Chirp app. Switch homes in the app and reconnect, and your AI client sees the new one.

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
| **Switching things on** | See what a device is set up to do, do it, and check the device actually got the message — so *"turn on the lamp"* works from the app you're already in. |
| **Pretend sensors** | Set up an emulated sensor, change what it reports, send a one-off reading to test an alert, and move a sensor between pretend and real. It can put any of your real sensors onto the emulator, and take a pretend one live onto a LoRaWAN connection. |
| **Connections** | See how your home is connected and set up a new connection for a sensor. |
| **Automations** | Go through the automations you've built and tell you what each one does. |
| **Alerts** | Look at your alerts, summarize what's been triggering and how often, and send a test notification so you can check it lands on your phone. |
| **Dashboards** | List your dashboards and pull the data behind a widget, so it can chart or explain a reading you're looking at. |
| **History** | Search back through your home's activity, export a slice of it, and map out which sensor is measuring what. |
| **Household** | Look up your home's details and members, invite someone new, and set what they're allowed to see. |

Everything it does runs with your permissions, and destructive or important actions are shown to you before they happen — same as anywhere else in Chirp.

## How this differs from the AI Helper in the app

Chirp already has an [AI Helper](../ai-assistant/README.md) built into the app: open **AI Chat** in the sidebar and it's right there, knows your home, and needs no setup at all. For most people, most of the time, that's the one to use.

MCP is for when you'd rather bring your own AI app to the same home — because you live in your desktop client all day, because you want your home's data in the same conversation as everything else you're working on, or simply because you prefer that assistant. Both talk to the same home and respect the same permissions.

## How this differs from the API

The [REST API](public-rest-api.md) is for code *you* write — a script that exports readings into a spreadsheet every Sunday, or a bridge to another home platform. It runs on a key you create in [Settings → API Keys](../settings/api-keys.md), with exactly the scopes you give it.

MCP is for an AI client acting **as you**, in a conversation, with your own sign-in and your own permissions. No key to manage, and nothing to write. If you want something to run unattended on a schedule, use the API. If you want to ask questions and get things done in the moment, use MCP.
