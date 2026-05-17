# gRPC API

Chirp also offers a gRPC interface. For almost everyone at home you won't need it — **REST is the practical choice for home scripts and integrations** (see [REST API](public-rest-api.md)). **gRPC is the advanced / on-premise path: use it only if you specifically need it for an on-premise or typed service-to-service integration.**

## When it's worth it

Reach for gRPC only if you specifically want a typed, generated client and a fixed contract inside your own software, or direct service-to-service calls in a more involved or self-hosted setup. Otherwise REST covers what a typical home script or integration needs, with far less setup.

## How it works

gRPC uses the same key-based sign-in as REST — `X-API-Key` plus your home context (see [Authentication & API keys](authentication-and-api-keys.md)). The [API reference](https://api.chirpwireless.io/) lists the available gRPC services and methods. For native gRPC client definitions, use the materials provided with your on-premise or integration package.

## See also

- [REST API](public-rest-api.md) — start here.
- [Authentication & API keys](authentication-and-api-keys.md)
