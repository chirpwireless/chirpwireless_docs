# API Keys

API keys let you connect Chirp to your own scripts, home automation setups, and integrations — securely and without sharing your account password. You might use one to pull temperature history into a spreadsheet, connect another smart home platform to your sensor data, or give a developer trusted read access to your home readings.

Each key has exactly the permissions you choose. If you need to cut off access to one tool, you revoke or rotate just that key — everything else keeps working.

> **Want to know how to actually call the API?** The [API](../api/README.md) section covers the protocols, signing requests, and examples. This page is just about making and managing the keys.

## Getting there

Navigate to **Settings → API Keys** in the sidebar.

---

## Creating a key

1. Click **Create API Key**.
2. Fill in a **Name** for the key. This is required. Use something that reminds you what the key is for — for example, "Temperature Export Script" or "Home Platform Bridge". You'll see this name in the table later.
3. Optionally pick an **Expires** date. The calendar won't let you choose a date in the past. If you leave this blank, the key stays active until you revoke it. For experiments or short-term setups, setting an expiry date is a good reminder to clean up access you no longer need — check the **Status** column to confirm a key's current state.
4. Choose **Scopes** — you must select at least one. Scopes control what the key is allowed to do. See [What the scopes mean](#what-the-scopes-mean) below.
5. Confirm to create the key.

### Save the key right away

The moment the key is created, it appears once with a copy button and the message:

> **"Copy this key now. You will not be able to see it again."**

Copy it and keep it somewhere safe — in a password manager, a secure notes app, or wherever you store credentials. Once you close the dialog, the full key is gone. Only a short prefix remains visible in the table. If you lose it, you'll need to create a new one.

---

## What the scopes mean

Scopes are the permissions you assign to a key. Pick only what the integration actually needs.

Available scopes may depend on your home's plan. Pulling **history** or **latest readings** uses a separate telemetry scope, not *Devices: Read* — check the [API reference](../api/README.md) for the scope each call needs.

| Scope | Read lets the key... | Write lets the key... |
|-------|---------------------|----------------------|
| **Connections** | View your connection setup | Change connection settings |
| **Dashboards** | View dashboards and widget data | Create and edit dashboards and widgets |
| **Devices** | View your sensors and their setup | Register sensors, change sensor settings |
| **Events** | Read sensor event history | — |
| **Logs** | View activity logs | Export logs |
| **Organizations** | View your home organization details | Change organization settings |
| **Rules** | View automation rules | Create, edit, and manage automations |
| **Sensors** | View sensor templates and metrics | Create and edit sensor templates |
| **Users** | View household member accounts | Invite and manage household members |

Grant only what the tool uses — a script that just reads your sensor list needs only **Devices: Read**, with no write access or anything to do with rules or users. Start minimal and add scopes only if the integration actually needs them.

---

## Your keys table

The API Keys page shows all the keys you've created. Each row tells you:

| Column | What it shows |
|--------|--------------|
| **Name** | The label you gave the key |
| **Key Prefix** | A short snippet of the key — enough to recognize it, not enough to use it |
| **Scopes** | The permissions this key carries, shown as labels |
| **Status** | **Active** (green), **Rotated** (yellow), or **Revoked** (red) |
| **Created** | When you first created this key |
| **Expires** | The expiry date you set, or "Never" |
| **Last Used** | When this key last made a successful API call |

Keys are sorted newest first. A rotation icon and a trash icon appear only on Active keys — use the rotation icon to rotate a key and the trash icon to revoke it.

---

## Rotating a key

Rotation swaps the key for a fresh one. The old key stops working the moment you confirm. Use this if a key has been accidentally shared, exposed, or you just want to refresh credentials periodically.

1. Click the rotation icon on the key row.
2. A dialog asks you to confirm:
   > **"Rotate API Key — This will generate a new key and mark the current key '[name]' as rotated. The old key will stop working."**
3. Confirm.
4. The new key is shown once — copy it immediately.
5. Update any scripts or integrations using the old key before they try to connect again.

The old key stays in the table with **Rotated** status so you have a record of it.

---

## Revoking a key

Revoking cuts off access permanently. You'd do this when you no longer need the key at all — for example, when a project is finished or you're removing a tool from your setup.

1. Click the trash icon on the key row.
2. A dialog confirms what's about to happen:
   > **"Revoke API Key — This will permanently revoke the API key '[name]'. This action cannot be undone."**
3. Confirm.

The key shows as **Revoked** in the table. It stays visible for your records, but it will never work again.

---

## If you lose a key

There's no way to recover a key once the dialog is closed. The only option is to rotate it — use the rotation icon on the key row, copy the new key, and update your scripts with the new value.

---

## A few good habits

- **One key per integration.** If one tool needs to be disconnected, you revoke just that key. Other integrations keep working without any changes.
- **Set expiry dates for experiments.** If you're testing something or sharing temporary access, put an end date on the key. You won't need to remember to clean it up later.
- **Never paste a key into a chat, email, or code commit.** Store credentials in a password manager or secure notes, and inject them into scripts at runtime rather than hardcoding them.
- **Rotate regularly for stable integrations.** Even for long-running scripts, a fresh key every few months is good practice.
