---
description: Get programmatic access to your home's sensor data for scripts, spreadsheets, and smart-home integrations.
---

# API

Chirp's **API** lets you bring your home into scripts and tools you build yourself. Pull sensor readings into a personal report or send an existing device command from an integration, using the same home workspace as your dashboards and automations.

An **API**, or application programming interface, is how software requests those operations. The [REST API](public-rest-api.md) is the starting point for a script; [MCP](mcp-server.md) connects an AI client that can help configure your home through conversation.

Begin with the [REST API](public-rest-api.md), which uses ordinary web requests. You will need an [API key](../settings/api-keys.md), a credential for your integration, and the identifier of the home it belongs to. The key's **scopes** are the operations it is allowed to use. The [API reference](https://api.chirpwireless.io/) lists those requirements for each call.

## REST is the way in

For home scripts and integrations, the **REST API** is the practical starting point: plain HTTPS and JSON that works from any language, tool, or no-code automation. Almost anything you'd want at home — read a sensor's latest value, pull history into a spreadsheet, bridge readings into another smart-home platform — is a REST call. See [REST API](public-rest-api.md).

A **gRPC API** also exists — the advanced / on-premise path. It is not the normal homeowner path: for home scripts and tools use REST, and reach for gRPC only if you specifically need it for an on-premise or typed service-to-service integration. See [gRPC API](grpc-api.md).

## Bringing your own AI app

If you'd rather not write code at all, the **MCP server** connects an AI client like Claude Code or Claude Desktop directly to your home. You sign in with your usual Chirp account — no key to create — and the AI app can then list your sensors, check your alerts, or add a device for you, with exactly your own permissions. See [MCP Server](mcp-server.md).

## Signing requests

Each request carries a scoped API key in the `X-API-Key` header (format `chirp_<key>`) and your home's context in `X-Organization-Id`. You create and manage keys in **Settings → API Keys**; the essentials are in [Authentication & API keys](authentication-and-api-keys.md), and the full walkthrough is in [API Keys](../settings/api-keys.md).

## In this section

- [REST API](public-rest-api.md) — the normal way to connect scripts and tools.
- [gRPC API](grpc-api.md) — only for advanced typed-client or service integrations.
- [MCP Server](mcp-server.md) — connect your own AI app to your home.
- [Authentication & API keys](authentication-and-api-keys.md) — how requests are signed.
- [Examples](examples.md) — a first authenticated request.
