---
description: Every automation node — Gateway, Script Task, Set Alarm, Execute Command, Enrichment — its fields and runtime behavior.
---

# Automation Node Guide

Every automation is built from nodes connected by flows on the visual canvas. This page describes each node type: what it does, what fields appear in its properties sidebar, and how it behaves when the automation runs.

All properties panels have **Save** and **Cancel** buttons at the bottom. Changes are not applied until you click Save.

---

## Start Event

The entry point of your automation. Every automation has exactly one Start Event, placed automatically when you create it. It can start from one sensor's readings or from a trigger that watches a condition across one or more sensors.

### Properties panel

| Field | Description |
|---|---|
| **Name** | A label for this node. Placeholder: *e.g., Fire Alarm*. |
| **Start source** | What sets the automation off: **Sensor reading** (one sensor's readings, the usual choice) or **Trigger condition** (a [trigger](../going-deeper/triggers.md), for "only if it's still happening" and for covering several sensors at once). One or the other, never both. |
| **Event filter — Device** | Shown for **Sensor reading**. Dropdown to select the device. Placeholder: *Select device*. |
| **Event filter — Sensor** | Shown for **Sensor reading**. Dropdown to select the sensor on that device. Enabled after you choose a device. Placeholder: *Select sensor*. |
| **Trigger condition** | Shown for **Trigger condition** instead of the Event filter. Dropdown listing your triggers. Placeholder: *Select trigger*. Only the first page loads, and it says so when there are more. |
| **Enable Schedule** | Toggle (Off by default). When turned On, the automation only runs during the specified time window. |
| **Time Range** | Appears when Schedule is On. Tap **Change schedule**, choose the days of the week, and enter the **From** and **To** times. Outside this window, incoming data is ignored. |
| **Time Zone** | Appears when Schedule is On. Select the time zone used for the schedule. |
| **Inputs** | Optional input parameters. Each has a name and a CEL expression. Click **+ Add input** to add entries. |
| **Outputs** | Optional output parameters. Same structure as Inputs. Click **+ Add output**. |

### What happens at runtime

What you get depends on the **Start source**.

**Started by a sensor reading** — when the selected sensor reports, the automation creates three variables that all downstream nodes can access:

| Variable | Contains |
|---|---|
| `vars.value` | The sensor reading (number, string, or boolean depending on sensor type) |
| `vars.sensor_id` | The unique identifier of the sensor that triggered the automation |
| `vars.timestamp` | The time the reading was recorded |

**Started by a trigger condition** — you get a different three:

| Variable | Contains |
|---|---|
| `vars.device_name` | The name of the sensor that set it off — how a grouped automation tells you *which* window or door it was |
| `vars.sensor_id` | The identifier of the sensor behind it |
| `vars.timestamp` | When the situation was met |

There is **no `vars.value`** on a trigger-started automation: a trigger reports that something *held for a while*, not what the reading was. An expression using `vars.value` will fail every time it runs.

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

The default flow covers "none of these matched". It does not cover a condition that can't be worked out at all — if one mentions a variable the automation hasn't got, or comes back as something other than true or false, the gateway stops there and nothing further along that path runs. In a debug session you'll see a red ring on the gateway; see [Debugging Automations](debugging-automations.md#what-the-rings-and-dots-mean).

A gateway also has to do one job or the other: two or more paths leading out of it (a decision), or two or more coming in (paths joining back up). One in and one out doesn't decide anything, and the build turns it down — join those two nodes directly instead.

### Do you need Inputs and Outputs?

No — and most gateways don't use them. Conditions can read your values directly, so you can leave both empty and put `vars.value > 25` straight on the branch.

They're there for when a condition would otherwise be long, or when you'd be writing the same sum on several branches. An **Input** works something out just before the gateway decides and gives it a short name that the gateway's own conditions can use — set an input called `feelsLike` to `vars.temperature + vars.humidity / 10`, then write your branches as `vars.feelsLike > 30`. An input belongs to that gateway alone; nodes further along can't see it.

An **Output** goes the other way: it's worked out after the branch is picked and added to your automation's values, so a later node — an alarm message, say — can use it.

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

## Execute Command

Sends a command to a device when the automation reaches this node — the step that lets an automation *act* on your home, not just warn you. It runs one of a device's existing [commands](../../devices/commands/) (turn on, set brightness, change temperature) all by itself.

For the full walkthrough and examples, see [When an Automation Runs a Command](automation-runs-a-command.md). This entry covers the fields.

### Properties panel

| Field | Description |
|---|---|
| **Name** | A label for this step. Leave it blank and pick a command, and it fills in with the command's name. Placeholder behaves like the other nodes. |
| **Device** | A search box to pick the device to control. |
| **Command** | A dropdown of that device's commands. Enabled once you pick a device. |
| **Parameters** | One row per thing the command needs (brightness, target temperature, on/off). Each is either a fixed **Value** (checked against the allowed range) or an **Expression** — a CEL formula worked out at runtime, with the triggering reading available as `vars.value`. |
| **Inputs** | Optional input parameters. Click **+ Add input**. |
| **Outputs** | Optional output parameters. Click **+ Add output**. |

The device must be controllable (Zigbee/MQTT, or a Class C LoRaWAN device) and must already have a command set up — see [Setting up a command](../../devices/commands/creating-commands.md).

### What happens at runtime

1. Each setting is worked out — fixed values as-is, expressions calculated from the current reading.
2. The command is sent to the device, over Zigbee/MQTT or LoRaWAN, just as if you'd pressed it yourself.
3. It's recorded in the device's history with how it went, and any "check it worked" set on the command applies here too.

Attach a Boundary Error Event if you want to be alerted when a command doesn't go through.

### Home example

Your basement humidity sensor triggers the automation. A gateway routes any reading above 70% to an Execute Command node that sends "turn on" to the dehumidifier's smart plug — so the damp is dealt with before you'd even have seen the alert.

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
