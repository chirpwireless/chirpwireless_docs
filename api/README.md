# API

Chirp gives you programmatic access to your home's data and controls — for personal scripts, local dashboards, spreadsheets, and trusted integrations with other home-automation tools.

The full, interactive API reference is at **[api.chirpwireless.io](https://api.chirpwireless.io/)**. That portal lists exactly what you can call; this section explains what the API is, how requests are signed, and where to get a key. It does not copy the reference.

## REST is the way in

For home scripts and integrations, the **REST API** is the practical starting point: plain HTTPS and JSON that works from any language, tool, or no-code automation. Almost anything you'd want at home — read a sensor's latest value, pull history into a spreadsheet, bridge readings into another smart-home platform — is a REST call. See [REST API](public-rest-api.md).

A **gRPC API** also exists, for advanced setups that use generated, strongly typed clients or wire services together directly. It is not the normal homeowner path — if you're writing a script or connecting a tool, use REST. See [gRPC API](grpc-api.md) only if you specifically need it.

The reference portal is the source of truth for which operations exist, and under which protocol — don't assume something offered over REST is also offered over gRPC.

## Signing requests

Each request carries a scoped API key in the `X-API-Key` header and your home's context in `X-Organization-Id`. You create and manage keys in **Settings → API Keys**; the essentials are in [Authentication & API keys](authentication-and-api-keys.md), and the full walkthrough is in [API Keys](../settings/api-keys.md).

## In this section

- [REST API](public-rest-api.md) — the normal way to connect scripts and tools.
- [gRPC API](grpc-api.md) — only for advanced typed-client or service integrations.
- [Authentication & API keys](authentication-and-api-keys.md) — how requests are signed.
- [Examples](examples.md) — a first authenticated request.
