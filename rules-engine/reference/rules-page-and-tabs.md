---
description: A tour of the Rules page — Rules, Triggers, Artifacts, and Trash, plus the actions on each automation row.
---

# Rules Page and Tabs

The Rules page is where you manage automations and the saved trigger conditions that can start them. Open it from the sidebar by clicking **Rules engine**. The page has four tabs: **Rules**, **Triggers**, **Artifacts**, and **Trash**.

---

## Rules tab

This is the main list of your automations. Each row shows:

| Column | What it shows |
|---|---|
| **Name** | The automation name and its description (if you added one) |
| **Last Modified** | How long ago the automation was last changed — for example, "2 hours ago" |

### Actions

Each automation has three actions on the right side of its row:

- **Edit** — Opens the automation in the visual editor so you can change its logic.
- **Clone** — Creates a copy of the automation. Useful when you want a second automation based on the same pattern — say, a "Bedroom Humidity Alert" cloned from your existing "Basement Humidity Alert."
- **Delete** — Moves the automation to the Trash tab (it is not permanently removed right away).

### Lock indicator

If another household member is currently editing an automation, a lock icon appears next to its name. Hovering over the icon shows a tooltip: *"The rule is in edit mode. The rule cannot be changed while it is being worked on by another employee of the organization."* along with the time the lock expires.

While an automation is locked, Edit, Clone, and Delete are disabled for everyone else. The lock releases automatically after the editor saves and exits, or after a period of inactivity.

### Adding a new automation

Click the **Add Rule** button to create a new automation. This opens a blank canvas in the visual editor with a Start Event already placed.

---

## Triggers tab

This tab contains saved conditions such as “freezer door open for 10 minutes” or “any leak sensor is wet.” Select **Add trigger** to choose the reading, comparison, timing, and devices.

Creating a trigger does not create an automation or add anything to the canvas. After saving it, return to the **Rules** tab, add or edit an automation, and select the trigger in that automation's **Start Event**. It is a Start Event source, not a node in the palette. See [From a trigger to a running automation](../going-deeper/triggers.md#from-a-trigger-to-a-running-automation) for every step.

---

## Artifacts tab

The Artifacts tab shows every automation that has been **built** — compiled into a deployable artifact. This is where you deploy, stop, and manage the running versions of your automations.

### Search

A search input at the top lets you filter the artifacts list by name. This is helpful when you have many automations and need to find one quickly.

### Layout

Artifacts are grouped by automation name. Each group shows the **Rule name** and **Description** as columns. Click the expand arrow on a row to see all builds for that automation.

### Expanded artifact details

Each build shows:

- **Build timestamp** — When this artifact was compiled.
- **Status** — One of:
  - **Running** (green) — The artifact is live and waiting for its selected sensor or trigger source.
  - **Stopped** (orange) — The artifact was deliberately stopped by you or a household member.
  - **Force Stopped** (red) — The system detected repeated errors and automatically stopped the artifact. See [Fixing Builds and Runtime Stops](fixing-builds-and-runtime-stops.md) for recovery steps.
- **Comment** — A text note attached to the build. Comments are inline editable — click a comment to update it without rebuilding. Add notes like "initial version" or "replaced by v3 due to false alarms."
- **Artifact Source** — A link that opens the automation's current state in a read-only editor view.
- **Deploy** / **Stop** / **Delete** — Actions to control the artifact lifecycle.

---

## Trash tab

Automations you delete from the Rules tab appear here. Each row shows:

| Column | What it shows |
|---|---|
| **Name** | The automation name |
| **Description** | The automation description |
| **Deleted time** | The date and time it was deleted |

The only action available is **Restore rule**, which moves the automation back to the Rules tab. Restored automations come back unlocked.
