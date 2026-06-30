---
description: Connect your scripts and tools to Chirp over HTTPS with a scoped API key — manage sensors, dashboards, and automations.
---

# REST API

The REST API is how you connect your own scripts and tools to Chirp over normal HTTPS. If you can make an authenticated web request — from Python, a shell, a spreadsheet add-on, or another home-automation platform — you can use it.

Use the [API reference](https://api.chirpwireless.io/) for the full list of calls, their parameters, responses, and required scopes.

## What every request needs

- `X-API-Key` — a key you create in [Settings → API Keys](../settings/api-keys.md).
- `X-Organization-Id` — your home's ID; it has to match the home the key belongs to. A few calls also accept it as an `organizationId` query value instead of the header.

Everything goes over a secure (TLS) connection. Look after the key like a password — see [Authentication & API keys](authentication-and-api-keys.md).

## What the API can do

REST is the broad, everyday way in. Depending on the scopes you give the key, a script can work across your home's data — for example: read your account; list your sensors and manage their setup, including how each one is wired to a connection and which readings it maps to; pull **history and latest readings** (great for spreadsheets and charts); read and change connections; read and build dashboards and widgets; read your home and subscription details; read and manage your automations, including their saved versions; and set up and send **device commands** to control your gear.

For typed service-to-service or on-premise setups, see [gRPC API](grpc-api.md).

## Getting started

1. Make a scoped key in [Settings → API Keys](../settings/api-keys.md) and save it somewhere safe.
2. Find the call you want in the API reference.
3. Send it with the two headers above.
4. Read the JSON that comes back.

There's a copy-paste starter in [Examples](examples.md).

## See also

- [gRPC API](grpc-api.md) — only if you specifically need typed clients.
- [Authentication & API keys](authentication-and-api-keys.md)
- [API Keys](../settings/api-keys.md)
