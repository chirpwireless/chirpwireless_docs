# REST API

The REST API is how you connect your own scripts and tools to Chirp over normal HTTPS. If you can make an authenticated web request — from Python, a shell, a spreadsheet add-on, or another home-automation platform — you can use it.

This page is the plain-English overview. The exact calls live in the interactive reference at [api.chirpwireless.io](https://api.chirpwireless.io/); it's always the source of truth and isn't copied here.

## What every request needs

- `X-API-Key` — a key you create in [Settings → API Keys](../settings/api-keys.md).
- `X-Organization-Id` — your home's ID; it has to match the home the key belongs to. A few calls also accept it as an `organizationId` query value — the reference shows which.

Everything goes over a secure (TLS) connection. Look after the key like a password — see [Authentication & API keys](authentication-and-api-keys.md).

## What the API can do

REST is the broad, everyday way in. Depending on the scopes you give the key, a script can work across your home's data — for example: read your account; list your sensors and manage their setup; pull **history and latest readings** (great for spreadsheets and charts); read and change connections; read and build dashboards and widgets; read your home and subscription details; and read and manage your automations.

The exact calls, their parameters, and the scope each one needs are in the [reference](https://api.chirpwireless.io/) — that's the source of truth and isn't copied here. There's no remote-command or downlink call in the public API. Some of these are also available over gRPC (the [advanced / on-premise path](grpc-api.md)); don't assume a call exists in both — the reference shows which.

## Getting started

1. Make a scoped key in [Settings → API Keys](../settings/api-keys.md) and save it somewhere safe.
2. Find the call you want in the [reference](https://api.chirpwireless.io/).
3. Send it with the two headers above.
4. Read the JSON that comes back.

There's a copy-paste starter in [Examples](examples.md).

## See also

- [gRPC API](grpc-api.md) — only if you specifically need typed clients.
- [Authentication & API keys](authentication-and-api-keys.md)
- [API Keys](../settings/api-keys.md)
