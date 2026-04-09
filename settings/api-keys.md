# API Keys

If you like to tinker -- connecting Chirp to a home automation script, pulling sensor data into a spreadsheet, or building a custom integration -- API keys give you secure, programmatic access to your home's data.

## Getting There

Go to **Settings** > **API Keys** in the sidebar.

## Creating a Key

1. Click **Create API Key**.
2. Give the key a **Name** that reminds you what it is for (for example, "Garden Dashboard Script" or "Home Assistant Bridge").
3. Set an **Expiry date**. Keys expire automatically after this date. Choose a reasonable window -- you can always create a new one.
4. Choose **Scopes** to control what the key can access. Only grant the permissions the integration actually needs.
5. Click **Create**.

The key is displayed exactly once. Copy it immediately and store it somewhere safe -- Chirp will not show the full key again. If you lose it, you will need to create a new one.

## Managing Your Keys

The API Keys page shows a table of all keys you have created. Each row includes:

- **Name** -- The label you gave it.
- **Key prefix** -- The first few characters of the key, enough to identify it.
- **Scopes** -- Which permissions the key has (shown as chips).
- **Status** -- Active (green), Rotated (yellow), or Revoked (red).
- **Created** -- When the key was created.
- **Expires** -- The expiry date, or "Never" if no expiry was set.
- **Last Used** -- When the key was last used to make an API call, or "-" if it has never been used.

### Rotating a Key

If a key has been in use for a while or you suspect it may have been exposed, click the **Rotate** button on that key's row. A confirmation dialog explains: "This will generate a new key and mark the current key as rotated. The old key will stop working." The new key is shown once — copy it immediately. The old key's status changes to Rotated.

### Revoking a Key

If you no longer need a key or want to cut off access immediately, click the **Revoke** button. A confirmation dialog warns: "This will permanently revoke the API key. This action cannot be undone." Revoked keys remain in the table for reference but stop working instantly.

## Tips

- Give each integration its own key. If you need to revoke access for one tool, the others keep working.
- Set short expiry windows for experiments and longer ones for stable integrations.
- Never paste a key into a message, email, or public repository.
