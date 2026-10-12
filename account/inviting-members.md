---
description: Invite people to your Chirp home and pick which sensors, dashboards, and automations they can use.
---

# How do I invite members to my Chirp home?
Adding someone to your Chirp home takes just a few steps. Once they accept, they can see and interact with the sensors, dashboards, and automations you choose to share with them.

## What do I need before I invite someone?
- **Manage Users** permission with Edit access. If the **Add user** button is greyed out, you do not have this permission — ask your home owner or another member who manages access.
- The person you want to invite must already have a Chirp account. The invitation system does not create new accounts. If they have not signed up yet, they need to register first.

## Where do I find the invitation form?
Click your name or avatar in the bottom-left corner to open the user menu, then select **Users**. The members page shows everyone who belongs to your home, plus any invitations that have not been accepted yet. Click the **Add user** button at the top of the page.

## How do I send an invitation?
1. Click **Add user**. The **"Invite user to organization"** dialog opens.

2. **Enter the email address.** Type the email associated with the person's Chirp account. Click **Continue**.

3. **Set permissions.** The **Page access** section appears, listing each section of Chirp. For every section, choose one of three access levels:

   - **Edit** — they can view and make changes
   - **View** — they can see the section but not change anything
   - **No access** — the section is completely hidden from them

   The dialog starts with sensible defaults: Edit on most sections, with **Manage Users** and **Activity Log** set to No access. You can adjust any section before sending.

   Two sections have restricted options:
   - **Activity Log** (under **Reports** > **Audit Trail**) — only View or No access. There is no Edit option because the Activity Log is read-only for everyone.
   - **API Keys** — only Edit or No access. There is no View option — API key management is all-or-nothing.

4. Click **Send invite**. Chirp sends an email with a link to join your home. The invitation is valid for **7 days**.

5. The pending invitation appears in the members list. The row shows the invited email with an **"Awaiting invitation confirmation"** tooltip, and a **Remove** button in case you need to revoke it.

## Are there limits on invitations?
- **Existing accounts only.** If the email does not match an existing Chirp user, the invitation is rejected.
- **No self-invitations.** You cannot invite yourself.
- **No duplicate invitations.** If an active invitation already exists for the same email in your home, a new one cannot be sent.
- **No duplicate members.** If the person is already a member of your home, the invitation is rejected.
- **No Owner invitations.** You cannot invite someone as Owner. Ownership transfer is a separate process in [Home Settings](organization-settings.md).

## What happens after I send an invitation?
Once the invitation is sent, the person receives an email with a one-click link. See [Accepting Invitations](accepting-invitations.md) for what happens on their end. Need to withdraw an invitation that has not been accepted yet, or look after members once they have joined? [Managing Access](managing-access.md) covers both.
