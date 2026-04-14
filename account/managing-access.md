# Managing Access

As your household changes, you can update what each person sees and does — or remove someone entirely. You need **Manage Users** permission with Edit access to make changes.

## Where to Find It

Click your name or avatar in the bottom-left corner to open the user menu, then select **Users**. The members page shows all current members and pending invitations for your home.

Use the **"Search users..."** bar at the top to find a specific person by name or email.

## Changing Someone's Permissions

1. Find the person in the members list and click the **Edit** button next to their name.
2. The **Page access** panel opens, showing their current permission for each section of Chirp.
3. Adjust any section: **Edit**, **View**, or **No access**.
4. Click **Save changes**.

The update replaces all existing permissions with the new set. Changes take effect the next time that person loads Chirp.

The Activity Log (under **Reports** > **Audit Trail**) records a **"Permissions changed"** event with the before-and-after details.

## Revoking a Pending Invitation

If someone has not accepted their invitation yet:

1. Find the pending invitation in the members list — it shows the invited email with an **"Awaiting invitation confirmation"** tooltip.
2. Click the **Remove** button.
3. A confirmation dialog asks: *"Are you sure you want to delete the invitation for {email}?"*
4. Confirm the action.

The invitation link is immediately invalidated and the row disappears from the list. Invitation revocations are not recorded in the Activity Log.

## Removing a Member

1. Find the person in the members list and click the **Remove** button.
2. A confirmation dialog asks: *"Are you sure you want to remove {name} from {home name}?"*
3. Confirm the removal.

### What Happens When Someone Is Removed

- All their access to your home is deleted — sensors, dashboards, automations, and alerts become invisible to them.
- Their Chirp account is not affected. They can still access other homes they belong to.
- A **"User removed"** event is recorded in the Activity Log.

## What You Cannot Do

- **You cannot remove the owner.** There is no Remove button on the owner's row. If ownership needs to change, the current owner must transfer it in [Home Settings](organization-settings.md).
- **You cannot edit the owner's permissions.** There is no Edit button on the owner's row. The owner has automatic access to everything.
