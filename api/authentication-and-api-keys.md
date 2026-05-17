# Authentication & API Keys

Every API request — REST or gRPC — is signed with a **scoped API key**. This page explains the idea; creating, scoping, rotating, and revoking keys is covered step-by-step in [Settings → API Keys](../settings/api-keys.md) and isn't repeated here.

## What a request carries

- **`X-API-Key`** — your key, on every request.
- **`X-Organization-Id`** — your home; it has to match the home the key was made in. Some calls also accept it as an `organizationId` query value (the [reference](https://api.chirpwireless.io/) shows which).

Requests always go over a secure connection.

## Scopes keep keys narrow

A key only does what you let it. Each scope has a **Read** side and a **Write** side, and you choose them when you create the key. Give a key the least it needs — a spreadsheet export only needs Read. The full list and what each scope means is with the key-creation steps in [API Keys](../settings/api-keys.md).

## Keeping keys safe

- The full key shows **once** when you create it; after that only a short prefix is visible. Copy it into a password manager straight away.
- Use a **different key for each tool**, so you can switch one off without breaking the rest.
- If a key might have leaked, **revoke or rotate** it right away — a lost key can't be recovered, only replaced.
- Never paste a key into a public script, a shared sheet, or version control.

## Where to manage keys

Create and manage keys in [Settings → API Keys](../settings/api-keys.md). That page is about the keys themselves; this section is about using them to call the API.
