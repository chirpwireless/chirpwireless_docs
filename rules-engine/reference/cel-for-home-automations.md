---
description: A friendly CEL guide for home rules — sensor variables, comparisons, math, text, and building clear alarm messages.
---

# CEL for Home Automations

Chirp uses [CEL (Common Expression Language)](https://cel.dev) to power the expressions inside your automations — gateway conditions, script computations, alarm messages, and input/output definitions. CEL was originally designed by Google for evaluating conditions safely, and that safety carries over to your home automations: expressions cannot access your network, your files, or anything outside the automation's own data. They simply take in sensor values and produce results.

You do not need to be a programmer to use CEL. Most home automations use only a handful of short expressions. This page covers everything you need.

---

## Your sensor data

Every expression has access to a `vars` object that holds the current automation data. When your sensor sends a reading and the automation starts, three values are available right away:

| Variable | What it contains |
|---|---|
| `vars.value` | The sensor reading — a number (like soil moisture `42.5`), a string (like door status `"open"`), or a boolean (like motion `true`) |
| `vars.sensor_id` | The unique identifier of the sensor that triggered the automation |
| `vars.timestamp` | The time the reading was recorded |

### Accessing fields

Use **dot notation** for simple names or **bracket notation** when names contain special characters:

```cel
vars.value              // dot notation — the sensor reading
vars["sensor_id"]       // bracket notation — works for any name
vars["garden-sensor"]   // bracket notation required — hyphen in name
```

### Data added by nodes

As your automation runs, more data becomes available:

- **Script Tasks** that return a map add their keys to `vars`. For example, a script returning `{"comfort": "good"}` makes `vars.comfort` available downstream.
- **Enrichment nodes** store fetched sensor data as nested objects. If the output variable is `outdoor`, you can access `vars.outdoor.value`, `vars.outdoor.sensor_id`, and `vars.outdoor.timestamp_ms`.
- **Outputs** defined on any node publish named values into `vars` for downstream use.

---

## Types

Every value in CEL has a type. Here are the ones you will encounter:

| Type | What it is | Example |
|---|---|---|
| `bool` | True or false | `true`, `vars.value > 30` |
| `int` | Whole number | `42`, `-5` |
| `double` | Decimal number | `22.5`, `0.7` |
| `string` | Text | `"open"`, `"Basement alert"` |
| `list` | Ordered collection | `[1, 2, 3]`, `["kitchen", "bedroom"]` |
| `map` | Key-value pairs | `{"level": "high", "zone": "garden"}` |
| `null` | No value | `null` |
| `timestamp` | A point in time | `vars.timestamp` |
| `duration` | A span of time | `duration("30m")` |

### Converting between types

| Function | What it does | Example |
|---|---|---|
| `string()` | Converts to text | `string(vars.value)` → `"22.5"` |
| `int()` | Converts to whole number | `int("42")` → `42` |
| `double()` | Converts to decimal | `double("3.14")` → `3.14` |

Type conversion is important when building alarm messages — CEL does not automatically turn numbers into text for concatenation.

---

## Comparing values

| Operator | Meaning | Example |
|---|---|---|
| `==` | Equal to | `vars.value == "open"` (door sensor) |
| `!=` | Not equal to | `vars.value != "closed"` |
| `>` | Greater than | `vars.value > 70.0` (humidity too high) |
| `>=` | Greater than or equal | `vars.value >= 30` (moisture threshold) |
| `<` | Less than | `vars.value < 15.0` (soil too dry) |
| `<=` | Less than or equal | `vars.value <= 5` (battery low) |

---

## Combining conditions

| Operator | Meaning | Example |
|---|---|---|
| `&&` | Both must be true | `vars.value > 20.0 && vars.value < 26.0` (comfort zone) |
| `\|\|` | Either can be true | `vars.value < 5 \|\| vars.value > 95` (extreme readings) |
| `!` | Opposite | `!has(vars.outdoor)` (enrichment data missing) |

---

## Doing math

| Operator | Meaning | Example |
|---|---|---|
| `+` | Addition | `vars.value + 5` |
| `-` | Subtraction | `vars.value - vars.outdoor.value` (indoor/outdoor difference) |
| `*` | Multiplication | `(vars.value - 32.0) * 5.0 / 9.0` (Fahrenheit to Celsius) |
| `/` | Division | `vars.value / 100.0` (percentage to decimal) |
| `%` | Remainder | `vars.value % 10` |

---

## Choosing between values

The ternary operator picks one of two values based on a condition:

```cel
vars.value > 30 ? "too warm" : "comfortable"
```

Nest them for multiple levels:

```cel
vars.value < 15 ? "too dry" : vars.value < 40 ? "ideal" : "too wet"
```

This is useful in Script Tasks for classifying readings:

```cel
{"status": vars.value == "open" ? "unlocked" : "secured"}
```

---

## Working with text

| Operation | Syntax | Example |
|---|---|---|
| Join text | `+` | `"Moisture is " + string(vars.value) + "%"` |
| Length | `size()` | `vars.name.size() > 0` |
| Contains | `contains()` | `vars.zone.contains("garden")` |
| Starts with | `startsWith()` | `vars.sensor_id.startsWith("door-")` |
| Ends with | `endsWith()` | `vars.sensor_id.endsWith("-outdoor")` |
| Regex match | `matches()` | `vars.sensor_id.matches("^room-[0-9]+$")` |

Remember: use `string()` to convert numbers before joining them with text. `"Value: " + vars.value` will fail if `vars.value` is a number.

---

## Checking if data exists

The `has()` function checks whether a field is present before you try to use it:

```cel
has(vars.outdoor) && vars.outdoor.value > 35.0
```

This matters after an Enrichment node with a Boundary Error Event. If the enrichment fails and the error path runs, `vars.outdoor` will not exist. Using `has()` prevents your downstream expressions from crashing on missing data.

```cel
has(vars.garden_moisture) ? vars.garden_moisture.value : -1
```

---

## Collections

| Function | What it does | Example |
|---|---|---|
| `x in list` | Checks if a value is in a list | `vars.zone in ["kitchen", "bathroom", "laundry"]` |
| `key in map` | Checks if a key exists | `"humidity" in vars` |
| `list.exists(x, expr)` | True if any element matches | `["door", "window"].exists(s, vars.sensor_id.contains(s))` |
| `list.all(x, expr)` | True if all elements match | `[20.0, 22.0, 25.0].all(t, t > 15.0)` |
| `list.filter(x, expr)` | Returns matching elements | `[10, 25, 40].filter(t, t > 20)` → `[25, 40]` |
| `list.map(x, expr)` | Transforms each element | `[1, 2, 3].map(x, x * 10)` → `[10, 20, 30]` |

---

## Inputs and Outputs scope

When you add Inputs and Outputs to a node in the properties sidebar, they behave differently:

- **Inputs** are **local** to that node. They create helper variables that only exist during that node's execution. Downstream nodes cannot see them.
- **Outputs** write values into the **shared** `vars` context. They persist and are accessible to all downstream nodes.

If you compute a value in an Input and want to use it later, move it to an Output instead.

---

## Platform functions

Chirp adds two functions on top of standard CEL:

### error(message)

Forces the node to fail with a specific error message. The engine then looks for an attached Boundary Error Event to route to. If none exists, the automation stops.

Use it when certain data conditions should trigger the error path deliberately:

```cel
vars.value < 0 ? error("negative reading — sensor may be faulty") : {"status": "ok"}
```

### random()

Returns a random decimal number between 0.0 and 1.0. Useful for sampling or adding variation:

```cel
random() < 0.05 ? "spot-check" : "skip"
```

---

## Building alarm messages

The Motivation Message field in a Set Alarm node must produce a text string. Use `string()` to convert numbers:

```cel
"Basement humidity is " + string(vars.value) + "% — above the safe limit"
```

```cel
"Front door has been " + vars.value + " since " + string(vars.timestamp)
```

Include context so the notification makes sense on its own:

```cel
"Garden soil moisture dropped to " + string(vars.value) + "%. Watering may be needed."
```

---

## Tips

- **Keep expressions short.** If you need to do several things — classify, compute, and format — spread the work across multiple Script Task nodes. Simpler expressions are easier to debug.
- **Use `has()` before optional data.** Any variable from an Enrichment node might not exist if the sensor was offline.
- **Convert types explicitly.** CEL will not turn a number into text for you. Use `string()` for alarm messages and `double()` or `int()` when mixing numeric types in arithmetic.
- **Test with edge cases in mind.** What happens when the sensor reports zero? A negative value? A very large number? Make sure your gateway conditions handle the full range.
- **Name variables clearly.** When defining Output names or Enrichment variable names, use descriptive names like `outdoor_temp`, `soil_moisture`, or `door_status` — not `x` or `tmp`.
