# Home Settings

Home Settings is where you rename your Chirp home and, if needed, hand ownership to someone else. Only the home owner sees this option.

## Getting There

Click your avatar or name in the bottom-left corner to open the user menu. If you are the owner, **Organization settings** appears in the menu. Click it to open the settings dialog.

If you do not see this option, you are not the current owner.

The dialog contains two fields — your home's name and the current owner — along with **Save changes** and **Close** buttons.

## Renaming Your Home

Edit the **Organizations name** field in the dialog and click **Save changes**. The new name appears everywhere — in the user menu, member lists, and the Activity Log (under **Reports** > **Audit Trail**).

## Transferring Ownership

Ownership transfer is a two-step process: you initiate it, and the new owner must accept.

### Starting the Transfer

1. Open the settings dialog.
2. Click the **Organizations owner** dropdown, which lists every current member of your home.
3. Select the person you want to make the new owner. The helper text reads: *"Only one user can be Organization owner."*
4. Click **Save changes**.

Chirp sends an ownership transfer invitation to the selected person. The invitation is valid for **24 hours**. A success screen confirms with two messages and a **Got it** button to dismiss:

> *"We sent an invitation letter to the specified email."*
>
> *"Your access will be updated to Editor once the new owner logs into the platform."*

Until the new owner accepts, you remain the owner with full control.

### What Happens After Acceptance

Despite the "Editor" message shown in the dialog, your actual access is broader than the Editor label suggests. Once the new owner accepts:

- **You keep full editing access** to every section of Chirp — Dashboards, Devices, Rules, Connectors, Subscription, member management, and everything else.
- **The Activity Log** (under **Reports** > **Audit Trail**) becomes view-only for you. This is the only section where your access changes.
- **The Organization settings menu item** moves to the new owner. You will no longer see it in your user menu.
- **The new owner** gets automatic access across the home, with the Activity Log limited to view-only.

The previous owner remains a member of the home and is not removed.

### Constraints

- **Only the current owner can initiate a transfer.** No one else sees the settings dialog.
- **The target must already be a member of your home.** You cannot transfer ownership to someone who has not joined yet.
- **One active transfer at a time.** If a transfer invitation is already pending, you cannot start another until it expires or is accepted.
- **24-hour expiration.** If the new owner does not accept within 24 hours, the invitation expires and you remain the owner.
- **Always exactly one owner.** There is no co-ownership.
