---
description: Set per-metric color rules so a reading turns green, yellow, or red — green for comfortable, red for check it now.
---

# Conditions

Conditions are per-metric color rules that turn a raw sensor reading into visible meaning. Instead of looking at a number and deciding whether it's good or bad, the widget does that for you — a green pin means comfortable, a red pin means check it now, a yellow marker means getting close to the limit. You define what those colors mean for each sensor in each place it's used.

A temperature sensor in the living room should be green at 18–24°C. The same type of sensor watching a fridge should be green at 2–5°C. Different place, different meaning, completely different conditions — even though the data looks the same.

## Which widgets use conditions

Conditions are available for **Last Data** and **Image** widgets. Each metric in these widgets has its own set of conditions, configured independently.

The **Chart** widget uses a different approach — per-metric color picker and threshold bands on the graph. See [Chart Widget](chart-widget.md) if you're working with a Chart.

**Note on metric types:** Both the Image and Last Data metric selectors surface numeric sensors only (INTEGER and FLOAT types). Number conditions are the practical path for both widgets. The conditions modal also exposes String and Boolean data type options — these are described below — but they require a widget that can select a sensor of those types, which is not currently the case for Last Data or the Image widget.

## How to open the Conditions modal

1. Open the widget's settings and go to the **Datasource** tab.
2. Find the metric row for the sensor you want to configure.
3. Tap the **Conditions button** — it's labeled **"Conditions: N"** where N is the number of conditions currently set.
4. The Conditions modal opens.

## What the Conditions modal contains

**Title:** "Conditions" / **Subtitle:** "The conditions set first will be considered as a priority"

**Header (applies to the whole metric):**
- **Device metric** — Read-only. Shows which sensor this modal is for.
- **Unit** — Override the display unit shown on the widget. Leave blank to use the sensor's default unit.
- **Icon** — Pick or change the icon for this metric.
- **Default color** — The color used when no condition matches. This is the only place to set the metric's base color.

**Conditions list:**
Each condition has:
- **Condition name** *(required)* — A label like "Comfortable", "Warning", or "Critical". Must not be empty.
- **Data type** — Number, String, or Boolean (see below)
- **Value fields** — Depend on the data type
- **Color** — The color to show when this condition matches
- **Delete** — Remove this condition

**Add condition** — Tap to add a new condition. New conditions default to: name "Condition N", type Number, From 0, To 100, primary color.

There's no limit on the number of conditions you can add.

**Save** (disabled while any validation error exists) / **Cancel**

## Priority: first match wins

Conditions are evaluated top to bottom. The **first condition in the list that matches the current reading** determines the color. Order matters.

If your sensor reads 7°C and you have:
1. "Normal" — Number, From 2, To 8 — green
2. "Warning" — Number, From 8, To 12 — yellow

The reading 7°C matches condition 1, so green is shown. Condition 2 is not evaluated.

To change priority, reorder the conditions in the list.

## Value fields by data type

### Number

**From** and **To** fields — both are optional. Either can be left empty to create an open-ended range:

- **Empty From** — matches any value below To (no lower limit)
- **Empty To** — matches any value above From (no upper limit)
- **Both filled** — From must be ≤ To

Examples:
- From: 18, To: 24 → matches readings between 18 and 24
- From: 30 (no To) → matches any reading 30 and above
- (no From), To: 5 → matches any reading 5 and below

### Number conditions — on/off and open/closed states

Many sensors report binary state as a number: 1 when something is active or open, 0 when it is off or closed. Number conditions map these values to meaningful labels and colors:

- Condition "On" — Number, From 1, To 1 — yellow (or your chosen color)
- Condition "Off" — Number, From 0, To 0 — grey

Examples using this pattern:
- Light sensor: 1 = "On" (yellow), 0 = "Off" (grey)
- Contact sensor (door): 1 = "Open" (red), 0 = "Closed" (green)
- Leak sensor: 1 = "Leak detected" (red), 0 = "Clear" (green)

The same Number condition type handles all of these. The difference is only in the labels and colors you assign.

### String

A single **Value** text field. Matches the reading exactly, case-sensitive. Available in the conditions modal but requires a widget that surfaces a String-type sensor — Last Data and Image widget selectors do not surface String sensors.

### Boolean

A **True / False** dropdown. Matches the reading exactly. Available in the conditions modal but requires a widget that surfaces a Boolean-type sensor — Last Data and Image widget selectors do not surface Boolean sensors.

## Color fallback hierarchy

1. **Matched condition color** — The color of the first matching condition
2. **Default color** — The color set in the modal header (applies when no condition matches)
3. **Platform default** — Applied when no default color is set in the modal

## Examples

### Number conditions — temperature in two contexts

**Living room sensor:**
- "Comfortable" — From 18, To 24 — green
- "A bit cool" — From 15, To 18 — yellow
- "Cold alert" — (no From), To 15 — red

**Fridge sensor (same sensor type, completely different meaning):**
- "Normal" — From 2, To 5 — green
- "Check fridge" — From 5 (no upper limit) — red

The readings look the same — both are temperatures in °C. The conditions are completely different because "2°C in a fridge" is fine, while "2°C in the living room" is an emergency.

### Number conditions — open-ended bounds for a tank level

A water tank sensor reports fill percentage (0–100%):
- "Critical" — (no From), To 20 — red
- "Low" — From 20, To 50 — yellow
- "Good" — From 50 (no upper limit) — green

The first condition catches everything below 20%. The last catches everything above 50%. There's no need to specify exact upper/lower limits for every range.

### Number conditions — any numeric reading

The system doesn't care what the number represents. The same pattern works for:
- Battery level (%, 0–100)
- Soil moisture (%, 0–100)
- CO₂ level (ppm)
- Tank volume (liters or gallons)
- Any sensor that reports numbers

The meaning and the thresholds are yours to define.

### String conditions — device status sensor

A sensor that reports text values like "OK", "WARNING", or "FAULT":
- "OK" — String, Value: OK — green
- "Warning" — String, Value: WARNING — yellow
- "Fault" — String, Value: FAULT — red

No math involved. The widget reads the string, matches it exactly, and shows the right color.

### Boolean conditions — binary state sensors

**Motion sensor:**
- "Motion detected" — Boolean, True — orange
- "Clear" — Boolean, False — green

**Leak detector:**
- "Leak detected" — Boolean, True — red
- "Clear" — Boolean, False — green

**Pump running:**
- "Running" — Boolean, True — blue
- "Idle" — Boolean, False — grey

Any binary sensor works the same way: pick a color for each state and a label that makes sense in context.

## See also

- [Last Data Widget](last-data-widget.md) — Use conditions to color sensor readings and gauges
- [Image Widget](image-widget.md) — Use conditions to color the pins on your image
