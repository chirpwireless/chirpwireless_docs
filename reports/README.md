---
description: Track who has access to your Chirp home, and keep your sensors' join codes safe in an encrypted vault.
---

# Records & Reports

Two things worth keeping a proper record of: who has access to your household, and the codes your sensors need to get onto your network.

- [Activity Log](audit-trail.md) — A record of all membership events: invitations, joins, permission changes, and removals. Filter by person, event type, or date range.
- [Key Vault](key-vault.md) — An encrypted home for your sensors' DevEUI and AppKey pairs.

The activity log is found in the sidebar under **Reports > Audit Trail**. Only household members with the Audit Trail permission can view it.

**Key Vault** sits alongside it in the sidebar under **Records & Reports**. Every LoRaWAN sensor ships with a DevEUI and an AppKey — usually on a sticker that stops being easy to reach the moment the sensor goes on the wall. Save the pair to the vault and you can get it back whenever a sensor needs re-adding after a reset, a move, or a swap. It's encrypted, it belongs to your home rather than to one person, and it has its own permission, so you decide who can open it. See [Key Vault](key-vault.md).
