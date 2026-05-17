# Authentication & API Keys

Every API request — REST or gRPC — is signed with a **scoped API key**. Create, scope, rotate, and revoke keys in [Settings → API Keys](../settings/api-keys.md); this page covers how requests are signed.

## What a request carries

- **`X-API-Key`** — your key (format `chirp_<key>`), on every request.
- **`X-Organization-Id`** — your home; it has to match the home the key was made in. Some calls also accept it as an `organizationId` query value instead of the header.

Requests always go over a secure connection.

## Scopes keep keys narrow

A key only does what you let it. Scopes have a **Read** side and a **Write** side, and you choose them when you create the key. Give a key only the scopes it needs — a spreadsheet export only needs Read. Each call in the [API reference](https://api.chirpwireless.io/) lists the scope it requires.

## Keeping keys safe

- The full key shows **once** when you create it; after that only a short prefix is visible. Copy it into a password manager straight away.
- Use a **different key for each tool**, so you can switch one off without breaking the rest.
- If a key might have leaked, **revoke or rotate** it right away — a lost key can't be recovered, only replaced.
- Never paste a key into a public script, a shared sheet, or version control.