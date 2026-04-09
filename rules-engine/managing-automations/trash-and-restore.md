# Trash and Restore

When you delete an automation, it does not disappear forever. It moves to the **Trash** — a holding area where deleted automations wait before being permanently removed. If you change your mind, you can bring it back.

## Deleting an Automation

From the Rules list on the main Rules Engine page:

1. Find the automation you want to delete.
2. Click the **Delete** action (available from the row's action menu).
3. Confirm the deletion in the dialog that appears.

The automation is moved to the Trash tab. It no longer appears in the active Rules list, and any deployed artifact for that automation is stopped.

## Browsing the Trash

On the main Rules Engine page at `/rules`, click the **Trash** tab. This shows all deleted automations with their names, deletion dates, and who deleted them.

## Restoring from Trash

If you deleted an automation by mistake — or you realize you still need it after all:

1. Open the **Trash** tab.
2. Find the automation you want to restore.
3. Click the **Restore** action.

The automation reappears in the active Rules list, ready for you to view, edit, or deploy again.

Restored automations come back **unlocked** — no editing lock is held, so anyone with edit permissions can immediately start working on them.

Note that restoring an automation from trash does not automatically redeploy it. If it was running before deletion, you will need to build and deploy a new artifact to make it live again.

## Retention Window

Deleted automations are kept in the Trash for a limited time. The retention window is shown in the Trash tab. After that window passes, the automation is permanently removed and cannot be recovered.

If you think you might need an automation again, restore it sooner rather than later.

## Tips

- **Delete with confidence.** Trash gives you a safety net — you are not making an irreversible decision.
- **Check the Trash tab periodically.** If something has been sitting there for a while and you know you do not need it, you can let it expire naturally. If you realize you do need it, restore before the retention window closes.
- **Restored automations are clean slates operationally.** They come back with their full version history intact, but without a running artifact. Treat the restore as a starting point — review the automation, rebuild if needed, and deploy when ready.
