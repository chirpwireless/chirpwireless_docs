# gRPC API

Chirp also offers a gRPC API. For almost everyone at home you won't need it — **REST is the practical choice for home scripts and integrations** (see [REST API](public-rest-api.md)). gRPC is here for advanced setups that use generated, strongly typed clients or wire services together directly.

## When it's worth it

Reach for gRPC only if you specifically want:

- a typed, generated client and a fixed contract inside your own software;
- direct service-to-service calls in a more involved or self-hosted setup.

If that doesn't describe what you're doing, use REST — it covers what a typical home script or integration needs, with far less setup.

## How it works

gRPC uses the same key-based sign-in as REST — `X-API-Key` plus your home context (see [Authentication & API keys](authentication-and-api-keys.md)). The available gRPC services and methods are listed in the reference at [api.chirpwireless.io](https://api.chirpwireless.io/); not everything offered over REST is offered over gRPC, so check there first.

## See also

- [REST API](public-rest-api.md) — start here.
- [Authentication & API keys](authentication-and-api-keys.md)
