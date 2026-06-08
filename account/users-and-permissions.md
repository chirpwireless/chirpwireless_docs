---
description: Set per-section access for every household member so each person sees only what matters to them.
---

# Household Members

Your Chirp home works best when the people who live there can see what matters to them. You choose what each person can view and change, section by section — Dashboards, Devices, Rules, and everything else can be configured individually for every household member.

## The Members Page

Click your avatar or name in the bottom-left corner to open the user menu, then select **Users**.

The page shows everyone who belongs to your home, plus any invitations that have not been accepted yet.

- **Search** — Use the "Search users..." bar at the top to find a specific person by name or email.
- **Owner badge** — The home owner is marked with an "Owner" label. The owner always has full access and cannot be removed from this page. Ownership transfer happens in [Home Settings](organization-settings.md).
- **Pending invitations** — Invitations that have not been accepted yet appear with an info tooltip: "Awaiting invitation confirmation."
- **Edit access / View access columns** — Show a summary label for each member's permissions (see "Permission Labels" below).
- **Edit and Remove buttons** — Available for every member except the owner.

## How Permissions Work

Every section of Chirp can be set to one of three levels for each person:

| Level | What it means |
|---|---|
| **Edit** | Full access — can view and make changes |
| **View** | Can see the section but cannot modify anything |
| **No access** | The section is completely hidden |

When you invite someone or change their permissions, you set each section individually. There is no "pick a role" step — you work directly with the per-section settings.

### What You Can Configure

| Section | Allowed levels | Default for new invites | Notes |
|---|---|---|---|
| Overview | Edit / View / No access | Edit | |
| Dashboards | Edit / View / No access | Edit | |
| Devices | Edit / View / No access | Edit | |
| Cameras | Edit / View / No access | Edit | |
| SIM Cards | Edit / View / No access | Edit | |
| Notifications | Edit / View / No access | Edit | |
| Rules | Edit / View / No access | Edit | |
| Subscription | Edit / View / No access | Edit | |
| Manage Users | Edit / View / No access | No access | With View, a person can see the members list. With Edit, they can also invite people, change permissions, and remove members. |
| Connectors | Edit / View / No access | Edit | |
| Activity Log | View / No access | No access | Read-only for everyone — there is no Edit option. |
| API Keys | Edit / No access | Edit | There is no View option — access is all-or-nothing. |

### Defaults When Inviting

When you add someone new, the dialog starts with Edit on most sections. **Manage Users** and **Activity Log** are set to No access by default. You can adjust everything before sending the invitation.

### Permission Labels in the Members List

The members list shows labels like "Admin," "Editor," or "Viewer" next to each person. These are not assigned roles — they are computed automatically. Chirp compares each person's actual permission set against three known patterns:

- **Admin** — Edit on all sections, including Subscription and Manage Users. Activity Log is always View. API Keys is always Edit.
- **Editor** — Edit on most sections, but no access to Subscription or Manage Users. Activity Log is View. API Keys is Edit.
- **Viewer** — View on most sections, with the same exclusions as Editor. Activity Log is View. API Keys is Edit (self-service exception).

If a person's permissions match one of these patterns, the matching label is shown. If their permissions are customized and do not match any pattern, the individual section names are displayed instead. The owner always shows "Owner."

These labels are a convenience for scanning the members list at a glance. The real model is always per-section.

## In This Section

| Page | What it covers |
|---|---|
| [Inviting Members](inviting-members.md) | How to send an invitation, assign per-section permissions, and manage pending invites. |
| [Accepting Invitations](accepting-invitations.md) | What happens when someone clicks a membership or ownership transfer link. |
| [Managing Access](managing-access.md) | Updating permissions, revoking pending invitations, and removing household members. |
