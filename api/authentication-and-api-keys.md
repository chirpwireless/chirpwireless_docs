---
description: Authenticate Chirp API requests with an API key, its allowed scopes, and the required matching X-Organization-Id header.
---

# Authentication & API Keys

An **API key** is a secret credential that identifies a script or integration when it calls Chirp. Its **scopes** limit what it can do, such as read device information. Each key belongs to one home's workspace, called an **organization** in the API.

Create the key in [Settings → API Keys](../settings/api-keys.md), then send it with that home's identifier on each authenticated request. Chirp checks the key, its allowed scopes, and whether the organization matches. This is API-key authentication; you do not create a separate cryptographic signature for the request.

## What a request carries

- **`X-API-Key`** — your key (format `chirp_<key>`), on every request.
- **`X-Organization-Id`** — your home; it has to match the home the key was made in. The authentication gateway requires this header. An `organizationId` query value required by a particular call is additional; it cannot replace the header.

Requests always go over a secure connection.

## Scopes keep keys narrow

A key only does what you let it. Most scopes come in a **Read** and a **Write** form; a few — like telemetry and subscription data — are read-only. You choose them when you create the key, so give a key only what it needs — a spreadsheet export only needs Read. Each call in the [API reference](https://api.chirpwireless.io/) lists the scope it requires.

## Keeping keys safe

- The full key shows **once** when you create it; after that only a short prefix is visible. Copy it into a password manager straight away.
- Use a **different key for each tool**, so you can switch one off without breaking the rest.
- If a key might have leaked, **revoke or rotate** it right away — a lost key can't be recovered, only replaced.
- Never paste a key into a public script, a shared sheet, or version control.