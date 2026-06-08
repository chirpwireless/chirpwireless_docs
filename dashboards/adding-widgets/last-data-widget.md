---
description: Show the latest value from one or more sensors as a number, gauge, or ring — is the door open, how warm is the room?
---

# Last Data Widget

The Last Data widget shows the **last value received from a sensor**. When the device is actively reporting, that is also the current value. When the device goes offline after its last transmission, the widget continues showing that last value — it does not clear the display or flag that the device is silent. You see what the sensor last said, which is current if the device is still transmitting and may be stale if it is not.

Is the bedroom light on or off? Is the front door open or closed? What is the living room temperature? These are Last Data questions. The widget shows the last transmitted value for each — no chart, no history, no trend. If you want to see how a value changed over time, that is the [Chart widget](chart-widget.md).

You can display the latest value as-is — a number, text, or an on/off (`true`/`false`) reading — or as a ring gauge (Doughnut), a filled gauge (Pie), a Tube that fills up like a tank, a Gauge that slides a marker along a colored track, or a Radial Gauge that shows the reading on a round dial. One widget can hold multiple sensors — bedroom temperature, humidity, and CO2 level side by side, each styled independently. Conditions turn the raw number into visible meaning: green means everything is fine, red means look at this now.

## Setting up a Last Data widget

### Step 1 — Choose Last Data from the widget picker

Open dashboard edit mode and tap **Last data** in the widget picker. (See [Adding Widgets](README.md) for how to open edit mode.) The settings panel opens with two tabs: **Datasource** and **Appearance**.

### Step 2 — Datasource tab: connect your sensors

The Datasource tab is titled **"Last Data configuration"** with the subtitle **"Configure last data and data sources."**

**Adding a data source:**

1. Tap **Add datasource**. A **Datasource 1** block appears.
2. In the block, tap **Choose device** and select the device whose sensor you want to display.
3. Tap **Add metric**. A metric row appears. Each metric row shows:
   - **Data type** — set to Telemetry
   - **Device metric** — choose which sensor reading to display (any reading — number, text, or on/off)
   - **Icon** — pick an icon to represent this metric on the widget
   - **Conditions button** — labeled **"Conditions: N"** where N is the number of conditions currently set. Tap it to open the Conditions modal and define what color this reading shows at different values. This is also where you set the **default color** for the metric. See [Conditions](conditions.md) for details.
   - **Delete** — remove this metric from the widget

There is no color picker directly in the metric row. The reading color is controlled entirely through the Conditions modal.

> **About reading types.** The **Device metric** list shows every reading, whatever its type. The **Value** display shows it as-is — a number, text, or an on/off value (`true`/`false`) — so no conversion is needed. The gauge-style displays (Doughnut, Pie, Tube, Gauge, Radial gauge) need a number to fill a scale: a numeric text reading is read as that number, and anything non-numeric shows as 0. To change a reading's type, open [Data Templates](../../devices/data-templates.md) and set its **Type** on the **Metrics** tab.

**Adding multiple sensors:**

Tap **Add datasource** to add a second device. You can add as many devices as you like. Duplicate devices are not allowed — once a device is added, it won't appear in the picker again.

Each device can expose multiple metrics. After adding a device, tap **Add metric** on its row to include additional sensor readings from the same device. The Add metric button grays out once all of that device's available metrics have been added.

**Default value range for gauges:**

When you add a metric, a default value range of 0–100 is created for it automatically. This range is used by the Doughnut, Pie, Tube, and Gauge display types to set the scale. You can change it in the Appearance tab.

When your sensors are set, tap **Next** to continue to the Appearance tab.

### Step 3 — Appearance tab: choose how it looks

**Widget name** *(required)* — The title shown on the widget. The placeholder reads **"Enter widget name"**.

**Description** — An optional subtitle below the name.

**Widget type** — Choose how readings are displayed. Each display type has its own page with a screenshot and the full detail:

- **Value** — The latest reading shown as-is — a number with its unit, text, or an on/off (`true`/`false`) value. Clean and direct. [→ Value Display](last-data-widget/number.md)
- **Doughnut** — A ring gauge that fills proportionally between the Min and Max you set. [→ Doughnut Display](last-data-widget/doughnut.md)
- **Pie** — A filled circle gauge — the same idea as Doughnut, with a bolder look. [→ Pie Display](last-data-widget/pie.md)
- **Tube** — A tall cylinder that fills from the bottom like a tank. [→ Tube Display](last-data-widget/tube.md)
- **Gauge** — A horizontal track with a sliding marker and your color conditions shown as bands. [→ Gauge Display](last-data-widget/gauge.md)
- **Radial gauge** — A round dial with a needle, a sweep angle you choose, and your conditions as colored arcs. [→ Radial Gauge Display](last-data-widget/radial-gauge.md)

**Value range** *(Doughnut, Pie, Tube, Gauge, and Radial gauge)* — Appears per sensor once you choose one of these display types. Set the **Min** and **Max** values that define the scale the widget fills or marks against. The tooltip reads: **"Set min and max to define the chart scale. Max is the value where the indicator is fully filled (for a pie, the whole circle)."**

Validation: Min must be strictly less than Max. If they are equal or reversed, the widget won't save.

**Tick marks** *(Tube, Gauge, and Radial gauge)* — Choose how many tick marks divide the scale. On a Gauge they run along the track, on a Tube they run down the side and pick up the color of whatever condition band they land in, and on a Radial gauge they ring the dial.

**Sweep angle** and **Radial Gauge name** *(Radial gauge only)* — Set how far around the dial sweeps (0 to 360 degrees; 300 by default) and the label shown with it. See [Radial Gauge Display](last-data-widget/radial-gauge.md).

**Tube and Gauge don't have a built-in "good" end.** The fill or marker just shows where the reading sits — your conditions decide what's fine and what isn't. Put the red band at the low end to be warned when something is running out, or at the high end when something is rising too far. The [Tube](last-data-widget/tube.md) and [Gauge](last-data-widget/gauge.md) pages walk through both.

**Display data legend** — A toggle that adds a legend listing your sensor metrics below the reading. Works for every display type.

### Step 4 — Save

Tap **Save** to add the widget to the dashboard.

## What to expect

Once placed, the widget immediately shows the last known value from each sensor. As sensors report new data, the display updates live.

The value shown is the last one received. If a device has been offline or silent, the widget continues showing the last reading it got — it does not clear the display. Check the sensor's last-reported time on the device page before acting on a reading if the device might be offline.

If a sensor hasn't reported yet, the widget shows **"Waiting for live data"** in the reading area. If no metrics have been configured, it shows **"Add a metric to start visualizing data"** or **"Choose data source and add metric"**.

## Common patterns

Almost every Last Data tile is one of a few simple ideas. Each display type has its own page with the full step-by-step and home examples — here is where to start.

- **Is it on or off?** — a door, a light, a leak sensor. A plain [Value display](last-data-widget/number.md) with one color per state is all you need.
- **What is the reading right now?** — a room temperature, an air-quality figure. A [Value display](last-data-widget/number.md) shows the value; a [Gauge display](last-data-widget/gauge.md) also shows whether it is in a comfortable range.
- **How full is it?** — a water tank, a battery, a rain barrel. Show it as a [Doughnut](last-data-widget/doughnut.md) or [Pie](last-data-widget/pie.md) ring, or as a filling [Tube](last-data-widget/tube.md) that looks like the tank itself.
- **Is something heading for trouble?** — a level creeping too high or a supply running too low. A [Gauge display](last-data-widget/gauge.md) turns your colors into bands so you can spot the moment it crosses the line.

## See also

- [Conditions](conditions.md) — Define color rules for each metric: what green, yellow, and red mean for that specific sensor in that specific place
- [Adding Widgets](README.md) — How to open edit mode and use the widget picker
