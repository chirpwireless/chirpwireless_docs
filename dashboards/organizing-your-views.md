# Organizing Your Views

When you have just one or two dashboards, finding them in the sidebar is easy. But as your smart home grows — a dashboard for each room, one for security, one for the garden — the list gets longer. Folders help you group related dashboards together, and drag-and-drop reordering lets you put the ones you use most right at the top.

## Opening the dashboard settings

Tap the **gear icon** (tooltip: **"Dashboard settings"**) next to the Dashboards section in the sidebar. A dialog opens with the title **"Dashboard settings"** and the description **"Create folders and rearrange dashboards and folders with a drag-and-drop gesture"**.

If you haven't created any dashboards yet, you'll see **"No dashboards yet"** in the center of the dialog.

## Creating a folder

At the top of the dialog, you'll find a text input for creating folders:

1. Type a folder name. The placeholder reads **"My folder"** — but something like "Upstairs", "Garden", or "Security" is more helpful.
2. Tap **Create folder**.

If you try to create a folder without entering a name, you'll see **"Folder name is required"**.

Once created, the folder appears in your sidebar as a collapsible group. Tap it to see the dashboards inside.

### How deep can folders go?

Folders are **one level only**. You can put dashboards inside a folder, but you can't put a folder inside another folder. This keeps things simple:

```
Dashboards
├── Upstairs             (folder)
│   ├── Bedroom
│   └── Nursery
├── Downstairs           (folder)
│   ├── Kitchen
│   └── Living Room
├── Garden               (folder)
│   └── Soil & Weather
└── Security             (top-level dashboard)
```

## Rearranging with drag-and-drop

The dialog shows all your dashboards and folders in a list. You can drag items to:

- **Change the order** — Move a dashboard or folder up or down in the list.
- **Move a dashboard into a folder** — Drag it onto the folder name.
- **Move a dashboard out of a folder** — Drag it back to the top level.

Your sidebar updates immediately to reflect the new arrangement.

## Deleting a folder

Tap the **trash icon** next to a folder name. A confirmation asks:

**"Are you sure you want to delete {folder name} folder?"**

with the warning:

**"All dashboards inside this folder will also be deleted. Once deleted, this action cannot be undone."**

Tap **Yes, delete** to confirm. The folder and every dashboard inside it are permanently removed.

## Deleting a dashboard from settings

You can also delete individual dashboards from this dialog. The confirmation reads:

**"Are you sure you want to delete {dashboard name} dashboard?"**

**"Once deleted, this action cannot be undone."**

Tap **Yes, delete** to confirm.

## Closing the settings

Tap **Ok** to close the dialog. All changes are already saved.

## Ideas for organizing a home

- **By floor** — "Upstairs", "Downstairs", "Basement". Simple and intuitive.
- **By purpose** — "Comfort" (temperature, humidity), "Security" (doors, windows, motion), "Garden" (moisture, weather).
- **By person** — If family members have their own rooms with sensors, a folder per person keeps things personal.

Start simple. You can always reorganize later by dragging dashboards between folders.

## What's next

- [Building a Dashboard](building-a-dashboard.md) — Create dashboards to fill your folders.
- [Choosing Widgets](choosing-widgets.md) — Add sensor data to each dashboard.
