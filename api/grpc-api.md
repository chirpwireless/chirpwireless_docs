---
description: Learn when the advanced gRPC interface is worth it over REST for typed, on-premise Chirp integrations.
---

# What is the Chirp gRPC API?
The **gRPC API** is an advanced way for software to call Chirp operations using predefined message types and a generated client library. It is useful when you are developing an integration that already relies on those service definitions, often within an on-premise setup.

You need the service definitions and endpoint from your integration package, plus [authentication credentials](authentication-and-api-keys.md). For a home script or a first integration, the [REST API](public-rest-api.md) is the simpler starting point: you can call it with standard web tools such as curl.

## When should I use the gRPC API?
Reach for gRPC only if you specifically want a typed, generated client and a fixed contract inside your own software, or direct service-to-service calls in a more involved or self-hosted setup. Otherwise REST covers what a typical home script or integration needs, with far less setup.

## How does the gRPC API work?
gRPC uses the same key-based sign-in as REST — `X-API-Key` plus your home context (see [Authentication & API keys](authentication-and-api-keys.md)). The [API reference](https://api.chirpwireless.io/) lists the available gRPC services and methods. If you build a native gRPC client, take the definitions from the materials that come with your on-premise or integration package.

## See also

- [REST API](public-rest-api.md) — start here.
- [Authentication & API keys](authentication-and-api-keys.md)
