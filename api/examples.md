# Examples

This shows how to sign a request. It doesn't list the calls themselves — pick the one you want from the reference at [api.chirpwireless.io](https://api.chirpwireless.io/), which is the source of truth.

## A signed REST request

Swap in your own key and home ID:

```bash
curl -sS https://api.chirpwireless.io/api/v2/devs \
  -H "X-API-Key: $CHIRP_API_KEY" \
  -H "X-Organization-Id: $CHIRP_HOME_ID"
```

`GET /api/v2/devs` lists the sensors the key can see (it needs a Devices **Read** scope). For anything else — a latest reading, history for a chart, changing a setting — look up the exact call in the [reference](https://api.chirpwireless.io/) and send it with the same two headers. Don't guess a path; the reference lists exactly what's available, and which calls are REST and which are gRPC.

## gRPC

Only relevant for advanced typed-client setups. It uses the same key and home headers. The [reference](https://api.chirpwireless.io/) lists the available gRPC services and methods so you know what to call; the client and protocol definitions aren't downloadable from there — get them from your integration package or support.

## Keep it safe

- Keep the key in an environment variable or password manager — never in the script itself or a shared file.
- One key per tool, with only the scopes it needs.
- More in [Authentication & API keys](authentication-and-api-keys.md).
