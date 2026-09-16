---
description: Make an authenticated Chirp REST request with curl, an API key, and its home identifier to list accessible devices.
---

# Examples

This example shows an **authenticated REST request**: a web request carrying an API key so Chirp can check which home and operations the caller may access. It lists devices without changing them, making it a useful first check for a new integration.

Create a key with Devices **Read** access and have its matching home identifier ready. Store them in the environment variables shown below, then run the request with curl. For other operations and required scopes, use the [API reference](https://api.chirpwireless.io/).

## An authenticated REST request {#a-signed-rest-request}

Swap in your own key and home ID:

```bash
curl -sS https://api.chirpwireless.io/api/v2/devices \
  -H "X-API-Key: $CHIRP_API_KEY" \
  -H "X-Organization-Id: $CHIRP_HOME_ID"
```

`GET /api/v2/devices` lists the sensors the key can see (it needs a Devices **Read** scope). Use the same two headers for other calls; check the API reference for the path and the scope each one needs.

## gRPC

Only relevant for advanced or on-premise typed-client setups. It uses the same headers. For native gRPC client definitions, use your on-premise or integration package.

## Keep it safe

- Keep the key in an environment variable or password manager — never in the script itself or a shared file.
- One key per tool, with only the scopes it needs.
- More in [Authentication & API keys](authentication-and-api-keys.md).
