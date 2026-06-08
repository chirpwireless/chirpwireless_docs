---
description: Browse every saved version of an automation, name your milestones, and roll back to a known-good version anytime.
---

# History, Restore, and Recovery

Every time your automation is saved — whether you click Save yourself, Chirp autosaves in the background, or the system saves during a session event — a new version is recorded. This gives you a complete timeline of how your automation has changed, and the ability to go back to any earlier version if something goes wrong.

## Why This Matters

Automations evolve. You tweak a threshold, add a branch, or restructure the flow. Most of the time those changes improve things — but sometimes you change something and the automation stops working the way you expect. Maybe you accidentally deleted a node, or a new condition is too broad and triggers false alerts.

Version history means you are never stuck. You can see exactly what your automation looked like before the change, restore it, and move on. Your saved work is always recoverable through version history.

## Finding the History Tab

1. Open any automation (in either View or Edit mode).
2. Click the **History** tab below the header bar.

The History tab shows a table of all saved versions, with the newest version at the top.

## What the History Table Shows

| Column | What it tells you |
|---|---|
| **Version name** | A label for the version. Defaults to an auto-generated name, but you can rename it. |
| **Date & Time** | When this version was saved |
| **Save type** | How the version was created (see below) |
| **User** | Who was editing when this version was saved |

### Save Types

Each version records the reason it was saved. This helps you understand the context around each entry:

| Save type | What happened |
|---|---|
| **manual** | Someone clicked the Save button deliberately |
| **auto** | Chirp autosaved during an active editing session |
| **editor_close** | Saved automatically when the editor was closed or the user navigated away |
| **disconnect** | Saved when the browser closed or the connection dropped unexpectedly |
| **session_timeout** | Saved after the inactivity timeout expired |
| **lock_cleanup** | Saved by the system when it detected an expired lock and released it |
| **restored** | This version was created by restoring a previous version |

A "manual" save is usually the most reliable restore point — it means someone deliberately saved at that moment. "auto" and "disconnect" versions may represent work-in-progress.

## Naming Versions

By default, versions have auto-generated names. Renaming them makes it much easier to find the right version later, especially if you have many.

To rename a version:

1. Click the **pencil icon** next to the version name in the history table.
2. Type a new name (up to 100 characters).
3. Press Enter or click away to confirm.

Good version names describe what changed or what the automation looked like at that point:

- "Before adding the outdoor sensor"
- "Working humidity alert"
- "Adjusted threshold to 75%"

A few naming rules:
- Maximum 100 characters
- Cannot duplicate the name of another version in the same automation
- The characters `<`, `>`, and `/` are not allowed

## Viewing a Previous Version

To see what your automation looked like at a specific point in time:

1. Find the version in the history table.
2. Click the **eye icon** (View) on that row.
3. The editor opens a read-only view of the diagram as it existed in that version.

In this view, you can see the full diagram and inspect node properties, but you cannot change anything. Two buttons are available:

- **Restore this version** — Makes this version the current one (see below)
- **Exit view mode** — Returns you to the History tab

## Restoring a Version

If a recent change broke your automation, restoring a previous version is the safest way to fix it.

### How to Restore

1. View the version you want to restore (click the eye icon in the History tab).
2. Click **Restore this version**.
3. A confirmation dialog explains what will happen.
4. Click **Restore** to confirm.

### What Happens

- The restored version becomes the new current version of your automation.
- A new entry appears at the top of the history table with save type **restored**.
- The version that was active before the restore is **preserved in the history** — it is not deleted or overwritten. Your saved work remains recoverable through version history.
- The restored version is a design-time change only. It does not affect any currently running artifact. If you want the restored version to go live, you need to build and deploy it.

Think of it this way: restoring does not "rewind" your automation. It creates a new version that happens to contain the same diagram as an older one. Your entire history — including the version you are moving away from — remains intact.

## Tips

- **Name versions after significant milestones.** "Added garden moisture branch" is much more useful than "Version 7" when you need to find a restore point.
- **Prefer restoring from a "manual" save.** Auto and disconnect versions may contain incomplete work.
- **Restore before you start over.** If an automation is behaving strangely after edits, restore a known-good version rather than trying to fix the broken one under pressure. You can always study the broken version later.
- **Remember to redeploy.** Restoring a version updates the design but does not change what is running. Build and deploy the restored version to make it live.
