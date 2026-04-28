# Chart Widget

Last Data tells you where a reading is now. Chart tells you where it has been — and whether the trend should concern you.

Your bedroom temperature is 23°C right now. But was it always 23°C? Yesterday evening it was 19°C. Chart shows you that journey: the **large current reading** at the top tells you what it is now, and the **historical graph** below shows how it got there — the trace over the last hour, day, week, or month. You see the value right now and the pattern over time — rising, falling, stable, or spiking — without switching between views.

Threshold bands sit on the graph itself. Color the normal range green, the warning range yellow, and the danger range red. The bands make context visible at a glance — and the large reading at the top changes color automatically when the current value falls inside a threshold range.

## Setting up a Chart widget

### Step 1 — Choose Chart from the widget picker

Open dashboard edit mode and tap **Chart** in the widget picker. (See [Adding Widgets](README.md) for how to open edit mode.) The settings panel opens with two tabs: **Datasource** and **Appearance**.

### Step 2 — Datasource tab: connect one sensor

The Datasource tab is titled **"Chart configuration"** with the subtitle **"Configure chart and data sources."**

**The Chart widget tracks one sensor at a time.** Tap **Add datasource** to open the device selector and choose a device. Once a data source is added, the Add datasource button disappears entirely — it doesn't gray out, it leaves the panel. To switch to a different sensor, change the metric on the existing row.

The metric row shows:
- **Data type** — set to Telemetry
- **Device metric** — choose which sensor reading to graph (numeric sensors only: INTEGER and FLOAT types)
- **Color** — a color picker that sets both the line or bar color on the graph and the base color for the large current reading at the top
- **Delete** — remove this data source

Chart metrics do not have an Icon picker or a Conditions button. Color is set directly on the metric row.

### Step 3 — Appearance tab: configure the chart

**Widget name** *(required)* — Shown as the widget header.

**Description** — Optional subtitle.

**Widget type:**
- **Line** — A smooth continuous curve. Best for readings that change gradually over time, like temperature or humidity.
- **Bar** — Discrete vertical bars for each interval. Useful for readings where you want to see each report as a distinct event.

**Timeframe** — The period shown in the graph:
- Last hour
- Last day
- Last week
- Last month

**Value range** — Set the Y-axis scale:
- **From** *(required)* — The bottom of the axis
- **To** *(required)* — The top of the axis

**Thresholds** — Colored bands drawn across the graph to mark meaningful ranges. Tap **Add threshold** to create one. Each threshold has:
- **From** — Lower bound of the band
- **To** — Upper bound of the band
- **Label** — A name for the band (shown in the legend)
- **Color** — The color of the band
- **Show fill** — Toggle to display a colored fill across the band
- **Show line** — Toggle to display a boundary line at each edge
- **Delete** — Remove this threshold

Threshold bands render on the graph in **both Line and Bar modes**. Add as many thresholds as you need to describe the full range of meaning.

**Toggles:**
- **Show average value** — Adds a dashed horizontal line showing the average for the selected timeframe, with "Average" in the legend
- **Show vertical axis lines** — Grid lines along the time axis
- **Show horizontal axis lines** — Grid lines along the value axis
- **Display data legend** — Shows threshold labels and the average label in a scrollable legend below the chart

### Step 4 — Save

Tap **Save** to add the widget to the dashboard.

## How the current reading color works

The large value shown at the top of the widget defaults to the metric color you set in the Datasource tab. If the current value falls within one of your threshold ranges, the reading color switches to that threshold's color instead. This means the number at the top turns red, yellow, or green automatically — you don't have to set up separate conditions for the current reading separately.

For example: if you define a threshold from 5–10°C colored red, and your sensor reads 7°C, the large reading at the top displays in red. When the temperature drops back below 5°C and falls outside the threshold, the reading returns to the metric's base color.

## Thresholds vs conditions

Chart uses threshold bands — colored regions drawn on the graph — to add context to the time-series data. Last data and Image map widgets use the conditions system instead: named rules with priority order and per-metric color defaults. See [Conditions](conditions.md) for details on what the conditions system supports and the current metric-type caveat.

## Home examples

**Bedroom temperature — then and now:**
Your bedroom temperature is 23°C right now. Yesterday evening it was 19°C. Line chart, Last week — you can see the gradual warming trend and spot exactly when temperatures started climbing. Use Last Data if you only need to know the current value; use Chart when you want to understand the direction it is moving.

**Fridge staying cold this week?**
Not just "is it 4°C now" (use Last Data for that) — but "was it always 4°C this week?" Line chart, Last week, value range 0 to 10. Threshold: green 0–5°C "Normal", red 5–10°C "Check fridge". The graph shows whether the fridge held temperature consistently or had a spike yesterday afternoon when the door was left open.

**Energy use over the week:**
A smart meter. Line chart, Last week. Threshold bands mark the normal consumption range. Deviations — higher-than-usual overnight consumption, weekend peaks — are immediately visible as the line moves outside the green band.

## See also

- [Conditions](conditions.md) — Color rules for Last Data and Image Map widgets
- [Adding Widgets](README.md) — How to open edit mode and use the widget picker
