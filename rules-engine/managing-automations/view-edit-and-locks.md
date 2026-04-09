# View, Edit, and Locks

Your automations are shared resources — especially if more than one person in your household uses Chirp. The platform handles this with two distinct modes and a simple locking system that prevents accidental overwrites.

## View Mode

When you click an automation's name in the Rules list, it opens in **View mode**. This is a read-only view where you can:

- See the full visual diagram
- Click any node to inspect its properties
- Browse the History tab to review versions
- Check which artifact is deployed

You cannot change anything in View mode — no dragging nodes, no editing expressions, no saving. This is the safe way to look at an automation without risking accidental changes.

## Edit Mode

To make changes, switch to **Edit mode**. You can do this by:

- Clicking the **Edit** button when viewing an automation
- Using the **mode selector** in the editor header to switch from Viewing to Editing

When you enter Edit mode, two things happen:

1. The canvas becomes interactive — you can drag nodes, draw connections, and modify properties.
2. A **lock** is placed on this automation, tied to your account.

## How Locks Work

Locks prevent two people from editing the same automation at the same time. While you hold the lock:

- Only you can make changes to this automation
- Other household members see a lock icon next to the automation in the Rules list
- The lock tooltip shows who is editing and when the lock expires
- The Edit, Clone, and Delete actions are disabled for everyone else

The lock has an expiry time, which is shown in the UI. Chirp extends the lock automatically while you are actively working — you do not need to do anything to keep it alive.

### What If Someone Else Is Editing?

If you try to edit an automation that another household member is already working on, a dialog appears:

> **"The rule is in edit mode"**
> "[Name] started editing the rule at [time]. The rule is closed during another user's editing."

Click **Go to rules** to return to the list. The lock will be released when the other person finishes editing.

### Force-Unlock (Organization Owners)

If an automation is locked but the person who locked it is unavailable — maybe they left the editor open and stepped away — **organization owners** can force-unlock it.

1. Find the locked automation in the Rules list (look for the lock icon).
2. Click the lock icon (only clickable for organization owners).
3. Confirm the unlock in the dialog that appears.

Force-unlocking releases the lock immediately. Any unsaved changes the previous editor had are lost. The person who was editing will see a notification explaining that the owner unlocked the automation.

Use this sparingly — check with the other person first if possible.

## Autosave

While you are in Edit mode, Chirp automatically saves your work at regular intervals. You can see the current state in the editor header:

| Indicator | What it means |
|---|---|
| **Saving...** | A save is in progress right now |
| **Saved** | Your latest changes have been persisted |
| **Autosave Failed** | Something went wrong — a dialog appears offering to **Retry** or go **Back to rule** |

Each autosave creates a version in the history, so even if you forget to save manually, your recent work is captured.

## Inactivity Timeout

If you leave the editor open but stop interacting with it for a while, Chirp shows a dialog:

> **"The rule will be closed in 5 minutes"**
> "Continue editing to reset the timer."

You have two choices:

- **Continue** — Resets the timer and keeps your editing session going.
- **Save and exit** — Saves your current work, releases the lock, and returns you to the Rules list.

If you do not respond, Chirp saves your work automatically (recorded as a "session_timeout" version), releases the lock, and closes the editor. Your work is safe — you just need to re-enter Edit mode to continue.

## Leaving the Editor

When you navigate away from the editor while in Edit mode — clicking the back arrow, switching to View mode, or closing the browser tab — and you have unsaved changes, a prompt appears:

> **"Are you sure you want to unlock the rule?"**
> "Unsaved changes will be lost."

- **Cancel** — Stay in the editor and keep working.
- **Unlock** — Release the lock and leave. Changes made since the last save are lost.

If your browser crashes or you lose your internet connection unexpectedly, the lock is released automatically and the latest saved state is preserved as a version (with save type "disconnect"). You will not lose everything — just any changes made after the last autosave.

## Tips

- **Use View mode when you just want to check on things.** It is quicker and does not lock the automation.
- **Save manually before stepping away.** Autosave catches most situations, but a deliberate save gives you a clean version with save type "manual" that is easy to identify later.
- **Keep editing sessions focused.** The lock means nobody else can work on that automation while you have it open. Make your changes, save, and exit so the automation is available to others.
- **Name important versions.** After a significant change, save manually and then rename the version in the History tab so you can find it easily if you need to restore later.
