---
description: Every automation node explained — Start, Script Task, Gateway, Set Alarm, Enrichment — its fields and runtime behavior.
---

# Automation Node Guide

Every automation is built from nodes connected by flows on the visual canvas. This page describes each node type: what it does, what fields appear in its properties sidebar, and how it behaves when the automation runs.

All properties panels have **Save** and **Cancel** buttons at the bottom. Changes are not applied until you click Save.

---

## Start Event

The entry point of your automation. Every automation has exactly one Start Event, placed automatically when you create it. When the sensor you select reports a new reading, the automation starts running.

### Properties panel

| Field | Description |
|---|---|
| **Name** | A label for this node. Placeholder: *e.g., Fire Alarm*. |
| **Event filter — Device** | Dropdown to select the device. Placeholder: *Select device*. |
| **Event filter — Sensor** | Dropdown to select the sensor on that device. Enabled after you choose a device. Placeholder: *Select sensor*. |
| **Enable Schedule** | Toggle (Off by default). When turned On, the automation only runs during the specified time window. |
| **Time Range** | Appears when Schedule is On. Presets: "0:00 – 24:00", "8:00 – 20:00", "9:00 – 18:00", "6:00 – 22:00". |
| **Time Zone** | Appears when Schedule is On. Select the time zone for the schedule. |
| **Inputs** | Optional input parameters. Each has a name and a CEL expression. Click **+ Add input** to add entries. |
| **Outputs** | Optional output parameters. Same structure as Inputs. Click **+ Add output**. |

### What happens at runtime

When the selected sensor reports a new reading, the automation creates three variables that all downstream nodes can access:

| Variable | Contains |
|---|---|
| `vars.value` | The sensor reading (number, string, or boolean depending on sensor type) |
| `vars.sensor_id` | The unique identifier of the sensor that triggered the automation |
| `vars.timestamp` | The time the reading was recorded |

If you defined Inputs, they are computed as local helper values. If you defined Outputs, they are published into the shared workflow context so downstream nodes can use them.

### Home example

A soil moisture sensor in your garden triggers the automation. `vars.value` contains the moisture percentage (e.g., `28.5`). The automation checks whether the soil is too dry and sends an alert if so.

---

## End Event

Marks the end of an automation path. Every branch of your automation must eventually reach an End Event — if a path has no End Event, the build will fail.

### Properties panel

| Field | Description |
|---|---|
| **Name** | A label for this node. Placeholder: *e.g., Fire Alarm*. |

The End Event panel is minimal — just a name field, plus Save and Cancel.

### What happens at runtime

The automation run finishes for this path.

---

## Script Task

Runs a [CEL expression](cel-for-home-automations.md) to compute new values. Use Script Tasks when you need to classify a reading, calculate a derived value, or prepare data for downstream nodes.

### Properties panel

| Field | Description |
|---|---|
| **Name** | A label for this node. Placeholder: *e.g., Fire Alarm*. |
| **Script** | A CEL expression field (multiline, 6 rows). Placeholder: *Your script*. This is the main computation. |
| **Inputs** | Optional input parameters. Click **+ Add input**. |
| **Outputs** | Optional output parameters. Click **+ Add output**. |

### What happens at runtime

1. If you defined Inputs, they are computed as local variables (not shared downstream).
2. The Script expression is evaluated.
3. If the result is a **map** (e.g., `{"level": "high", "delta": 5.2}`), each key is merged into the shared workflow context. Downstream nodes can access `vars.level` and `vars.delta`.
4. If the result is **not a map**, it is discarded — the Script Task still runs, but nothing is added to the context.
5. If the expression produces an **error**, the engine checks for an attached Boundary Error Event. If one exists, execution routes to the error path. If not, the automation stops.
6. If you defined Outputs, they are published into the shared context after the script runs.

### Home example

A temperature sensor triggers your automation. The Script Task classifies the reading:

```cel
{"comfort": vars.value >= 20.0 && vars.value <= 25.0 ? "perfect" : "adjust"}
```

Downstream, a gateway checks `vars.comfort` to decide whether to send an alert.

---

## Exclusive Gateway

A decision point that checks conditions and picks exactly one path to follow. Think of it as a fork in the road — the automation reads the conditions from top to bottom and takes the first path that matches.

### Properties panel

The gateway panel opens with an info banner: *"Conditions are evaluated sequentially (top to bottom). The first condition met executes its flow, and all remaining conditions are skipped."*

| Field | Description |
|---|---|
| **Name** | A label for this node. Placeholder: *e.g., MSG Smoke*. |

Below the name, each outgoing connection appears as a **Flow** section:

| Flow field | Description |
|---|---|
| **System Name** | The internal name of the flow. |
| **Set as default** | Button to mark this flow as the fallback. Tooltip: *"Choose one of the conditions to act as the fallback path when all other conditions are False."* |
| **Label** | A display label for the flow (non-default flows only). |
| **Color** | A color picker for the flow line (non-default flows only). |
| **Condition (Expression)** | CEL expression that must return `true` or `false` (non-default flows only). Placeholder: *e.g., vars.value > 10*. Required. |

Flows can be **reordered by dragging** — this changes the evaluation order. If no outgoing connections exist yet, the panel shows: *"Draw connections from this gateway on the canvas to add flows."*

| Additional fields | Description |
|---|---|
| **Inputs** | Optional input parameters. Click **+ Add input**. |
| **Outputs** | Optional output parameters. Click **+ Add output**. |

### What happens at runtime

1. The engine evaluates each outgoing flow's condition **from top to bottom**.
2. The **first condition that returns `true`** wins — the automation follows that path and skips all others.
3. If no condition matches, the **default flow** runs. The default flow has no condition — it acts as a catch-all.
4. If no condition matches and there is no default flow, the automation stops with an error.

Always include a default flow so your automation has somewhere to go even when readings are normal.

### Home example

A temperature sensor reports 28 degrees. The gateway has three flows:

1. `vars.value > 35` — "Too hot" path (not matched)
2. `vars.value > 25` — "Warm" path (**matched — automation follows this path**)
3. Default — "Normal" path (skipped because flow 2 already matched)

---

## Set Alarm

Triggers an alarm notification when the automation reaches this node. The alarm itself is defined on the [Alarm page](../../alarm/README.md) — this node selects which alarm to fire and provides the notification message.

### Properties panel

The panel header reads "Set alarm" with a link to the Alarms page where you can create new alarm definitions.

| Field | Description |
|---|---|
| **Choose Alarm** | Autocomplete dropdown to select an existing alarm definition. |
| **Motivation Message** | CEL expression (multiline, 3 rows) that produces the notification text. Subtitle: *"CEL expression that produces the alarm notification text."* Placeholder: `"Temperature is " + string(vars.temp) + " degrees"`. Must return a string. |
| **Inputs** | Optional input parameters. Click **+ Add input**. |
| **Outputs** | Optional output parameters. Click **+ Add output**. |

### What happens at runtime

1. The Motivation Message expression is evaluated — it must produce a string.
2. The selected alarm is triggered with that message.
3. Recipients configured on the alarm definition receive notifications through their chosen channels (email, SMS, push).

### Home example

Your basement water leak sensor triggers the automation. The Set Alarm node fires a "Water Leak Detected" alarm with the message:

```cel
"Water detected by basement sensor at " + string(vars.timestamp)
```

Everyone in the household who subscribed to that alarm receives a notification.

---

## Enrichment

Fetches the latest reading from a **different** sensor and stores it as a variable. This lets your automation compare data from multiple sensors — for example, checking indoor temperature against an outdoor sensor.

### Properties panel

The panel header reads "Data Enrichment" with the subtitle *"Attach relevant metadata to the incoming device data before processing."*

| Field | Description |
|---|---|
| **Name** | A label for this node. Placeholder: *e.g., Attach Room Temperature to Sensor Data*. |
| **Device** | Dropdown to select the device to fetch data from. Placeholder: *Select device*. |
| **Sensor** | Dropdown to select the sensor on that device. Enabled after you choose a device. Placeholder: *Select sensor*. |
| **Output variable** | The variable name where the fetched data will be stored. Placeholder: *User metadata*. |
| **Inputs** | Optional input parameters. Click **+ Add input**. |
| **Outputs** | Optional output parameters. Click **+ Add output**. |

### What happens at runtime

1. The platform fetches the most recent reading from the selected sensor.
2. The result is stored as a nested object under `vars.<output_variable>`:

| Variable | Contains |
|---|---|
| `vars.<output_variable>.value` | The sensor's latest reading |
| `vars.<output_variable>.sensor_id` | The sensor's unique identifier |
| `vars.<output_variable>.type` | The data type of the reading |
| `vars.<output_variable>.timestamp_ms` | Timestamp of the reading in milliseconds |

3. If the sensor is unreachable (offline, battery dead, removed), the node produces an error. Attach a Boundary Error Event to handle this gracefully.

### Home example

Your living room temperature sensor triggers the automation. An Enrichment node fetches the latest reading from the outdoor temperature sensor and stores it in a variable called `outdoor`:

- `vars.outdoor.value` — the outdoor temperature
- A downstream Script Task computes the difference: `{"delta": vars.value - vars.outdoor.value}`
- A gateway checks `vars.delta > 10` to decide whether the temperature gap is worth alerting about.

---

## Boundary Error Event

An error handler that attaches to a task node (Script Task, Set Alarm, or Enrichment). If the parent node fails for any reason, the automation routes through the Boundary Error Event's outgoing flow instead of stopping silently.

### How to add one

Drag a Boundary Error Event from the palette and drop it onto an existing task node. It snaps to the edge of that node. Then draw a single outgoing connection from the Boundary Error Event to the fallback path — typically another Set Alarm, a Script Task, or an End Event.

### Properties panel

| Field | Description |
|---|---|
| **Name** | A label for this node. Placeholder: *e.g., Fire Alarm*. |
| **Error code** | A text field for annotation. Placeholder: *Specify error code here*. |
| **Message** | A multiline text field (3 rows) for annotation. Placeholder: *Type error message here*. |
| **Inputs** | Displayed in the panel but **not processed** by the automation engine (see caveat below). |
| **Outputs** | Displayed in the panel but **not processed** by the automation engine (see caveat below). |

### Important caveats

**Error code and Message are annotations.** They help you label and document the error path in the editor, but the engine does not use them to filter errors. The Boundary Error Event catches **all** errors from its parent node regardless of the code you enter.

**Inputs and Outputs are not processed.** The properties panel shows Input and Output fields, but the automation engine does not evaluate them on this node type. If you need to compute or publish data on the error path, add Inputs and Outputs to the **downstream node** — the task or End Event that the Boundary Error Event's outgoing flow connects to.

### Rules

- A Boundary Error Event must be attached to a task node — it cannot exist as a standalone node.
- It must have exactly **one** outgoing connection.
- It cannot have incoming connections (other than its implicit attachment to the parent).

### What happens at runtime

When the parent task fails — for example, an Enrichment node cannot reach its sensor, or a Script Task expression throws an error — the engine routes execution through the Boundary Error Event's outgoing flow. Without the Boundary Error Event, the failure would silently stop that execution path and you would not know something went wrong.

### Home example

Your automation enriches living room data with a reading from the garden sensor. The Enrichment node has a Boundary Error Event attached. If the garden sensor is offline:

1. The Enrichment node fails.
2. The Boundary Error Event catches the failure.
3. Its outgoing flow leads to a Set Alarm node with a "Sensor Offline" alarm — so you know the garden sensor needs attention.

Without the Boundary Error Event, the automation would quietly stop and you would never know the garden sensor went dark.
