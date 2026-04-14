# Fixing Builds and Runtime Stops

When you click **Build**, Chirp validates your entire automation before creating a deployable artifact. If something is wrong, the build fails and shows error messages. This page explains what those errors mean and how to fix them, along with how deployment works and what to do when the system force-stops an automation.

---

## Common build errors

Build errors appear after you click Build. Each error describes the problem the validator found. Fix the issues and build again.

### Missing or incomplete Start Event

**What it looks like:** `expected exactly 1 message startEvent, got 0`

**What it means:** Every automation needs exactly one Start Event with a device and sensor selected. The build found either no Start Event or a Start Event without a sensor configured.

**How to fix:** Click the Start Event on your canvas. In the properties sidebar, select a **Device** and then a **Sensor** under Event filter. Save the node and build again.

### No End Event

**What it looks like:** `expected at least 1 endEvent`

**What it means:** Your automation has no End Event. Every path must eventually reach an End Event so the automation knows when a run is finished.

**How to fix:** Drag an End Event from the palette onto the canvas. Connect the last node in each path to an End Event.

### Dead-end node

**What it looks like:** `node "Task_1" has 0 outgoing flows` or a build error pointing to a node with no connections leading away from it.

**What it means:** A node other than an End Event has no outgoing connection. The automation would get stuck at this point.

**How to fix:** Draw a connection from the dead-end node to the next step in your automation — another task, a gateway, or an End Event.

### Gateway flow without a condition

**What it looks like:** `outgoing flow "Flow_2" of gateway "Gateway_1" must have conditionExpression`

**What it means:** An Exclusive Gateway has an outgoing connection that is not the default flow and does not have a CEL condition. Every non-default flow needs a condition so the gateway knows when to follow it.

**How to fix:** Click the Exclusive Gateway and find the flow without a condition in the properties sidebar. Either add a CEL condition (e.g., `vars.value > 30`) or click **Set as default** if this should be the fallback path. Only one flow can be the default.

### Default flow has a condition

**What it looks like:** `default flow "Flow_3" of gateway "Gateway_1" must not have conditionExpression`

**What it means:** The default flow should not have a condition — it runs when all other conditions are false. A condition on the default flow would be confusing and is not allowed.

**How to fix:** Either remove the condition from the default flow, or change the default to a different flow.

### CEL syntax error

**What it looks like:** `ERROR: <input>:1:15: Syntax error` or a message pointing to a specific position in your expression.

**What it means:** A CEL expression somewhere in your automation has a typo or invalid syntax. Gateway conditions, Script Task scripts, Motivation Messages, and Input/Output expressions are all checked at build time.

**How to fix:** Find the node with the error (the message often includes the node or flow ID). Open its properties and check the CEL expression for typos. Common mistakes: missing quotes around strings, using `=` instead of `==`, or forgetting `string()` when concatenating a number with text. See [CEL for Home Automations](cel-for-home-automations.md) for syntax help.

### Gateway condition does not return true/false

**What it looks like:** A build error referencing a gateway condition that does not evaluate to a boolean.

**What it means:** Gateway conditions must return `true` or `false`. If your expression returns a number, string, or other type, the build rejects it.

**How to fix:** Rewrite the condition as a comparison. For example, change `vars.value` to `vars.value > 30`.

### Duplicate node IDs

**What it looks like:** `duplicate id "Task_1" (scriptTask and scriptTask)`

**What it means:** Two nodes on your canvas have the same internal ID. This is rare and usually caused by copy-paste issues.

**How to fix:** Delete one of the duplicate nodes and re-create it from the palette.

### Invalid Boundary Error Event attachment

**What it looks like:** `boundaryEvent "Boundary_1" attachedToRef "Gateway_1" is not a task`

**What it means:** A Boundary Error Event can only attach to task nodes — Script Task, Set Alarm, or Enrichment. You cannot attach it to a gateway, Start Event, or End Event.

**How to fix:** Detach the Boundary Error Event and reattach it to a valid task node.

### Boundary Error Event flow target

**What it looks like:** `boundaryEvent "Boundary_1" outgoing must target a task or endEvent`

**What it means:** A Boundary Error Event's outgoing connection must lead to a task node (Script Task, Set Alarm, Enrichment) or an End Event. It cannot connect directly to a gateway or Start Event.

**How to fix:** Reconnect the Boundary Error Event's outgoing flow to a valid target — usually a Set Alarm (to notify about the error) or an End Event (to stop gracefully).

---

## Deploy and redeploy

### How deployment works

When you click **Deploy** on an artifact in the Artifacts tab, that build becomes the live version of your automation. It starts evaluating sensor data immediately.

Only one build per automation can be running at a time. If you deploy a new build while another one is already running, the platform automatically stops the old one and starts the new one in a single operation. There is no need to stop the running artifact first — the transition is handled for you.

### Stopping an automation

Click **Stop** on a running artifact to pause it. The sensor continues reporting data, but the automation no longer evaluates those readings.

Stopping is for deliberate pauses — when you want to temporarily disable an automation without deleting it. A stopped artifact can be restarted at any time by clicking **Deploy** again.

### Redeploying after changes

When you edit an automation that already has a running artifact:

1. Make your changes in the editor and save.
2. Build a new artifact — this does not affect the currently running one.
3. Deploy the new artifact — the platform replaces the running one automatically.

---

## Force Stop and recovery

### What Force Stop means

Chirp monitors the health of every running automation. If an automation encounters repeated errors over a sustained period, the system automatically stops it to prevent cascading problems in your home setup. The artifact status changes to **Force Stopped** (red).

This is a safety measure — it protects your home from an automation that might fire incorrect alarms, miss important readings, or produce confusing results due to an underlying problem.

### Common causes

- **Deleted alarm definition** — The automation tries to fire an alarm that no longer exists on the Alarm page.
- **Removed sensor** — The Start Event references a sensor that has been deleted from your device.
- **Enrichment sensor offline** — An Enrichment node tries to fetch data from a sensor that is no longer reporting, and no Boundary Error Event is attached to handle the failure.
- **CEL runtime error** — An expression fails at runtime due to unexpected data shapes (e.g., trying to access a field that does not exist without a `has()` check).

### Recovery steps

1. **Review the automation** — Open the editor and check each node's configuration. Look for references to deleted sensors, devices, or alarm definitions.
2. **Check that your sensors are active** — Make sure the devices referenced in the Start Event and any Enrichment nodes are online and reporting data.
3. **Verify CEL expressions** — Ensure expressions handle edge cases. Use `has()` before accessing variables that might not exist.
4. **Consider adding Boundary Error Events** — Attach them to Enrichment and Script Task nodes so failures route to a fallback path instead of crashing the automation.
5. **Fix the issue, build a new artifact, and deploy** — Once the underlying problem is resolved, build and deploy again.

---

## Build-time CEL validation

CEL expressions are validated at build time — not just checked for syntax, but also analyzed for type correctness:

- **Gateway conditions** must compile to a boolean type. An expression that returns a number or string will fail the build.
- **All expressions** (scripts, conditions, motivation messages, inputs, outputs) must be syntactically valid CEL. Typos and invalid references are caught before you can deploy.
- **Type mismatches** in operators (e.g., comparing a string to a number) may be caught depending on what the compiler can determine statically.

This means that if your build succeeds, the basic structure and syntax of every expression in your automation has been validated. Runtime errors can still occur when actual sensor data arrives with unexpected shapes, but the most common mistakes are caught early.
