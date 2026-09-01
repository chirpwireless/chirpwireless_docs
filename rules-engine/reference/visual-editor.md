---
description: Find your way around the automation editor — the header bar, canvas, node palette, and properties sidebar.
---

# Visual Editor

The visual editor is where you design your automation logic. It opens when you create a new automation or click **Edit** on an existing one. The editor has four main areas: the header bar, the canvas, the node palette, and the properties sidebar.

---

## Header bar

The header bar runs across the top of the editor and contains the main controls:

- **Automation name** — Click the name to rename your automation directly in the header.
- **Actions menu** — A dropdown with additional options:
  - **Rename** — Change the automation name.
  - **Edit description** — Add or update a text description for the automation.
  - **Duplicate rule** — Create a copy of this automation.
- **Mode selector** — A dropdown that switches between **Editing** (you can make changes) and **Viewing** (read-only, no accidental edits).
- **Autosave indicator** — Visible in Editing mode. This shows whether the page-level autosave has saved your latest canvas state. Autosave runs periodically in the background so you do not lose work if your browser closes unexpectedly.
- **Tabs** — Switch between **Editor** (the canvas) and **History** (version history for this automation).
- **Save** button — Explicitly saves the current state. The button is disabled if there are no unsaved changes or if the automation has no name.
- **Build** button — Compiles the automation into a deployable artifact. Only available in Editing mode. A build validates all your nodes and expressions before producing the artifact — see [Fixing Builds and Runtime Stops](fixing-builds-and-runtime-stops.md) if the build fails.

---

## Canvas

The canvas is the main workspace where your automation takes shape. A Start Event is placed automatically when you create a new automation.

- **Add nodes** by dragging them from the palette onto the canvas.
- **Pan** by clicking and dragging empty space on the canvas.
- **Zoom** using the editor controls or the scroll wheel.
- **Select a node** by clicking it — this opens the properties sidebar on the right.

### Connections

To connect two nodes, click the output port on one node and drag to the input port on another. This creates a flow — the path your automation follows at runtime.

Exclusive Gateway nodes can have multiple outgoing connections, each with its own condition. The order of these connections matters because the gateway checks them top to bottom. See the [Automation Node Guide](automation-node-guide.md) for details on how each node type behaves.

---

## Node palette

The palette sits alongside the canvas and lists the node types you can drag onto your automation:

| Node | What it does |
|---|---|
| **Start Event** | The entry point — starts from one device sensor or a saved trigger condition. One is placed on the canvas automatically when you create a new automation. |
| **End Event** | Marks the end of a path. Every branch of your automation must end here. |
| **Script Task** | Runs a CEL expression to compute new values. |
| **Exclusive Gateway** | A decision point that checks conditions and picks one path to follow. |
| **Set Alarm** | Fires an alarm notification when the automation reaches this point. |
| **Execute Command** | Sends a command to a device when the automation fires — acts on your home, not just alerts. |
| **Enrichment** | Fetches the latest reading from a different sensor. |
| **Boundary Error Event** | Catches errors from a parent node and routes to a fallback path. |

For detailed descriptions of each node's fields and runtime behavior, see the [Automation Node Guide](automation-node-guide.md).

---

## Properties sidebar

When you click a node on the canvas, a properties sidebar slides in from the right. It shows the configuration fields for that node — things like the node name, sensor selection, CEL expressions, and input/output definitions.

Each node type has its own set of fields. The sidebar always has **Save** and **Cancel** buttons at the bottom:

- **Save** — Applies your changes to the node. Until you click Save, nothing is committed.
- **Cancel** — Discards your changes and closes the sidebar.

**Node property changes are not automatic.** You must click Save after editing a node's fields. This is separate from the page-level autosave in the header, which periodically saves the overall canvas layout in the background.

---

## Lock behavior

Chirp prevents two household members from editing the same automation at the same time.

- If someone else is already editing, a dialog appears: *"The rule is in edit mode"* — with the editor's name and the time they started (if available). You can view the automation in read-only mode but cannot make changes until the lock is released.
- If you are editing and stay inactive for several minutes, a warning dialog appears: *"The rule will be closed in 5 minutes — Continue editing to reset the timer."* Click **Continue** to keep your session, or **Save and exit** to save and release the lock.
- Organization owners can force-unlock a rule that someone else has locked.
