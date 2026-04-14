# Data Enrichment and Expressions

A single sensor reading tells you what is happening in one spot. But your home is a system of connected spaces — the basement humidity matters more when you also know it has been raining, and the living room temperature means something different when the outdoor reading is 35 degrees versus 15 degrees.

Enrichment nodes and Script Tasks let you build automations that consider multiple data points before making a decision. Together, they turn a simple "is this number too high?" check into a thoughtful, context-aware response.

This is also where the balance becomes clear: Chirp remains a visual automation builder, but CEL lets you express very sophisticated logic when you need it — nested conditions, computed derived values, multi-sensor delta calculations, severity classifications, and dynamic alert messages that include live readings. The range of automations you can build goes well beyond simple thresholds.

## Enrichment: Pulling Data from Another Sensor

An **Enrichment** node fetches the most recent reading from a different sensor — one that is not the trigger sensor for this automation. This lets you bring in context from anywhere in your home.

### How to Add an Enrichment Node

1. Drag an **Enrichment** node from the palette onto the canvas (it has a download icon).
2. Connect it to the flow where you need the additional data — typically right after the Start Event, before any decision-making.
3. Click the Enrichment node to open its properties panel.
4. Configure:

| Field | What to enter |
|---|---|
| **Name** | A descriptive label — for example, "Get outdoor temperature" |
| **Device** | A searchable autocomplete dropdown — start typing and select the device that has the sensor you want to fetch from. |
| **Sensor** | A filtered dropdown that appears after you choose a device — select the specific sensor on that device. |
| **Variable name** | The name you will use to reference this data in later nodes — for example, `outdoor_temp` |

5. Click **Save** in the properties panel.

### Using the Enriched Data

After the Enrichment node runs, the fetched reading is available to every downstream node as `vars.<variable_name>`. For example, if your variable name is `outdoor_temp`, you can reference:

| Variable | What it contains |
|---|---|
| `vars.outdoor_temp.value` | The sensor's most recent reading |
| `vars.outdoor_temp.sensor_id` | The sensor's identifier |
| `vars.outdoor_temp.timestamp_ms` | When the reading was taken (milliseconds) |

You can use these in any CEL expression downstream — in Script Tasks, gateway conditions, or alarm messages.

## Script Tasks: Transforming and Computing

A **Script Task** runs a CEL expression that can transform data, compute new values, or prepare variables for decisions. You already used one in the first tutorial to classify a reading. Here, Script Tasks become even more useful because you can combine data from the trigger sensor and the enriched sensor.

You are still not writing an application from scratch here. The automation remains a visual BPMN flow, and the Script Task is the focused place where you add the exact expression the flow needs.

### Example: Compute a Temperature Difference

After enriching your automation with the outdoor temperature, you might want to know how much warmer or cooler your home is compared to outside:

```cel
{"temp_delta": vars.value - vars.outdoor_temp.value}
```

This creates a new variable, `vars.temp_delta`, that holds the difference. A downstream Exclusive Gateway can then check:

- `vars.temp_delta > 10` — "The house is more than 10 degrees warmer than outside" (possible heating issue in summer)
- `vars.temp_delta < -5` — "The house is more than 5 degrees cooler than outside" (possible heating failure in winter)

### Example: Classify a Wine Cellar Reading

If you monitor both temperature and humidity in your wine cellar (with enrichment for humidity and temperature as the trigger), you could classify the overall condition:

```cel
{"cellar_status": vars.value > 18 ? "too_warm" : vars.value < 10 ? "too_cold" : "ideal"}
```

Then in a second Script Task or the gateway conditions, combine it with humidity:

```cel
{"needs_attention": vars.cellar_status != "ideal" || vars.humidity_reading.value > 75}
```

### More CEL Patterns for Home Use

Here are some expressions that come in handy around the house:

**Percentage calculation:**
```cel
{"moisture_pct": (vars.value / 1023.0) * 100}
```

**Rounding a number to a readable string:**
```cel
{"display_temp": string(int(vars.value * 10) / 10.0)}
```

**Combining text with values for alarm messages:**
```cel
"Indoor: " + string(vars.value) + " / Outdoor: " + string(vars.outdoor_temp.value) + " (delta: " + string(vars.temp_delta) + ")"
```

## Putting It Together: Indoor vs. Outdoor Temperature

Here is a complete automation pattern that compares indoor and outdoor temperature and alerts you if the difference is unusually large:

```
Start Event (Living Room Temp Sensor)
       |
  Enrichment ("Get outdoor temperature")
       |
  Script Task ("Compute delta")
       |
  Exclusive Gateway
      / \
     /   \
  [Large   [Normal - Default]
   delta]       |
    |        End Event
 Set Alarm
 ("Unusual temp difference")
    |
 End Event
```

The Script Task contains:
```cel
{"temp_delta": vars.value - vars.outdoor_temp.value}
```

The gateway condition for the alert path:
```cel
vars.temp_delta > 15 || vars.temp_delta < -10
```

The Set Alarm motivation message:
```cel
"Indoor temperature is " + string(vars.value) + " but outdoor is " + string(vars.outdoor_temp.value) + " — difference of " + string(vars.temp_delta) + " degrees"
```

## Handling Errors: What If a Sensor Is Offline?

The outdoor sensor might be offline, out of battery, or temporarily unreachable. If the Enrichment node cannot fetch a reading, what happens?

Without error handling, that path of your automation simply stops — no alert, no notification, just silence. That is not ideal.

The solution is a **Boundary Error Event** — a small error-catching node that attaches to the Enrichment node and gives you a fallback path.

### How to Add Error Handling

1. Drag a **Boundary Error Event** from the palette and drop it onto your Enrichment node. It snaps to the edge of the node (a small circle with a lightning bolt).
2. Click the Boundary Error Event to open its properties panel. You will see three fields:

| Field | Purpose |
|---|---|
| **Name** | A label for this error catch on the canvas — for example, "Sensor offline" |
| **Error code** | A label you can use to describe the error type for your own reference. This is for documentation purposes only — the boundary event catches all errors from its parent node regardless of the code value. |
| **Message** | A label for the error scenario. Like the error code, this is for your own reference and does not affect which errors are caught. |

3. Draw a single outgoing connection from the Boundary Error Event to a fallback action — this could be a Set Alarm node that tells you the sensor is offline, or an End Event if you simply want to skip the automation when data is missing.

For the fallback alarm, you might use a motivation message like:

```cel
"Could not reach the outdoor temperature sensor — automation skipped this cycle"
```

### The Pattern with Error Handling

```
Start Event (Living Room Temp Sensor)
       |
  Enrichment ("Get outdoor temperature")
       |                \
       |           [Error] Boundary Error Event
       |                         |
  Script Task              Set Alarm ("Sensor offline")
       |                         |
  Exclusive Gateway          End Event
      / \
     /   \
  [Alert] [Normal]
    |       |
    ...    ...
```

This way, you are covered whether the second sensor is working or not. Your automation handles the happy path and the failure path gracefully.

## Tips

- **Name your enrichment variables clearly.** `outdoor_temp` is much easier to work with than `enrichment_1` when you revisit the automation weeks later.
- **Place enrichment early in the flow.** Fetch additional data before you need it — do not place an Enrichment node inside a branch that might not execute.
- **Always add error handling to enrichment nodes.** Sensors go offline. Batteries die. A brief fallback path takes two minutes to set up and saves you from silent failures.
- **Keep Script Task expressions focused.** One transformation per Script Task is easier to understand and debug than cramming everything into a single expression.

For a complete list of CEL operators, functions, and patterns, see the [CEL for Home Automations](../reference/cel-for-home-automations.md) reference. For details on how each node type behaves, see the [Automation Node Guide](../reference/automation-node-guide.md).
