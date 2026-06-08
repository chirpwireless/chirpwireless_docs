# API

Chirp gives you programmatic access to your home's data — for personal scripts, local dashboards, spreadsheets, and trusted integrations with other home-automation tools.

Use the **[API reference](https://api.chirpwireless.io/)** for the complete list of calls, request fields, responses, and required scopes. This section covers what the API is for, how requests are signed, and where to get a key.

> To control a device — turn it on or off, dim a light, change its settings — use [Device Commands](../devices/commands/) in the app. The API is for reading your data and wiring up integrations.

## REST is the way in

For home scripts and integrations, the **REST API** is the practical starting point: plain HTTPS and JSON that works from any language, tool, or no-code automation. Almost anything you'd want at home — read a sensor's latest value, pull history into a spreadsheet, bridge readings into another smart-home platform — is a REST call. See [REST API](public-rest-api.md).

A **gRPC API** also exists — the advanced / on-premise path. It is not the normal homeowner path: for home scripts and tools use REST, and reach for gRPC only if you specifically need it for an on-premise or typed service-to-service integration. See [gRPC API](grpc-api.md).

## Signing requests

Each request carries a scoped API key in the `X-API-Key` header (format `chirp_<key>`) and your home's context in `X-Organization-Id`. You create and manage keys in **Settings → API Keys**; the essentials are in [Authentication & API keys](authentication-and-api-keys.md), and the full walkthrough is in [API Keys](../settings/api-keys.md).

## In this section

- [REST API](public-rest-api.md) — the normal way to connect scripts and tools.
- [gRPC API](grpc-api.md) — only for advanced typed-client or service integrations.
- [Authentication & API keys](authentication-and-api-keys.md) — how requests are signed.
- [Examples](examples.md) — a first authenticated request.
