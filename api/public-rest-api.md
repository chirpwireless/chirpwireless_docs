# REST API

The REST API is how you connect your own scripts and tools to Chirp over normal HTTPS. If you can make an authenticated web request — from Python, a shell, a spreadsheet add-on, or another home-automation platform — you can use it.

This page is the plain-English overview. The exact calls live in the interactive reference at [api.chirpwireless.io](https://api.chirpwireless.io/); it's always the source of truth and isn't copied here.

## What every request needs

- `X-API-Key` — a key you create in [Settings → API Keys](../settings/api-keys.md).
- `X-Organization-Id` — your home's ID; it has to match the home the key belongs to. A few calls also accept it as an `organizationId` query value — the reference shows which.

Everything goes over a secure (TLS) connection. Look after the key like a password — see [Authentication & API keys](authentication-and-api-keys.md).

## What the API can do

The API has two protocols — REST and gRPC — and they don't cover the same calls. Depending on the scopes you give the key, the API as a whole can, for example:

- read your account and list your sensors;
- read sensor history and latest readings;
- read dashboards, automations, alarms, and notifications;
- change settings or create things where you've granted a Write scope.

Today the **REST** side is focused on your account, listing sensors, and automations; the rest of that list is gRPC (see [gRPC API](grpc-api.md)). There's no remote-command or downlink call in the public API.

Always check the [reference](https://api.chirpwireless.io/) for the exact call and whether it's REST or gRPC — don't assume a call is in both.

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
