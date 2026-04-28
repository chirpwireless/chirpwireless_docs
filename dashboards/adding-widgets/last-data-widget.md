# Last Data Widget

The Last Data widget shows the **last value received from a sensor**. When the device is actively reporting, that is also the current value. When the device goes offline after its last transmission, the widget continues showing that last value — it does not clear the display or flag that the device is silent. You see what the sensor last said, which is current if the device is still transmitting and may be stale if it is not.

Is the bedroom light on or off? Is the front door open or closed? What is the living room temperature? These are Last Data questions. The widget shows the last transmitted value for each — no chart, no history, no trend. If you want to see how a value changed over time, that is the [Chart widget](chart-widget.md).

You can display a plain number, a ring gauge (Doughnut), or a filled gauge (Pie). One widget can hold multiple sensors — bedroom temperature, humidity, and CO2 level side by side, each styled independently. Conditions turn the raw number into visible meaning: green means everything is fine, red means look at this now.

## Setting up a Last Data widget

### Step 1 — Choose Last Data from the widget picker

Open dashboard edit mode and tap **Last Data** in the widget picker. (See [Adding Widgets](README.md) for how to open edit mode.) The settings panel opens with two tabs: **Datasource** and **Appearance**.

### Step 2 — Datasource tab: connect your sensors

The Datasource tab is titled **"Last Data configuration"** with the subtitle **"Configure last data and data sources."**

**Adding a data source:**

1. Tap **Add datasource**. A device selector appears.
2. Choose the device whose sensor you want to display.
3. After choosing a device, its available metrics appear as rows. Each metric row shows:
   - **Data type** — set to Telemetry
   - **Device metric** — choose which sensor reading to display (only numeric sensors — INTEGER and FLOAT types — are offered)
   - **Icon** — pick an icon to represent this metric on the widget
   - **Conditions button** — labeled **"Conditions: N"** where N is the number of conditions currently set. Tap it to open the Conditions modal and define what color this reading shows at different values. This is also where you set the **default color** for the metric. See [Conditions](conditions.md) for details.
   - **Delete** — remove this metric from the widget

There is no color picker directly in the metric row. The reading color is controlled entirely through the Conditions modal.

**Adding multiple sensors:**

Tap **Add datasource** again to add a second device. You can add as many devices as you like. Duplicate devices are not allowed — once a device is added, it won't appear in the picker again.

Each device can expose multiple metrics. After adding a device, tap **Add metric** on its row to include additional sensor readings from the same device. The Add metric button grays out once all of that device's available metrics have been added.

**Default value range for gauges:**

When you add a metric, a default value range of 0–100 is created for it automatically. This range is used by the Doughnut and Pie display types to set the scale. You can change it in the Appearance tab.

### Step 3 — Appearance tab: choose how it looks

**Widget name** *(required)* — The title shown on the widget. The placeholder reads **"Enter widget name"**.

**Description** — An optional subtitle below the name.

**Widget type** — Choose how readings are displayed:

- **Number** — A plain numeric value with its unit. Clean and direct.
- **Doughnut** — A ring gauge. The ring fills proportionally between the Min and Max values you set. Useful for anything with a meaningful scale — water level, battery percentage, a fill ratio.
- **Pie** — A filled circle gauge. The circle fills completely when the reading reaches its Max. Same scale concept as Doughnut, different visual shape.

**Value range** *(Doughnut and Pie only)* — Appears per sensor once you choose Doughnut or Pie. Set the **Min** and **Max** values that define the gauge scale. The tooltip reads: **"Set min and max to define the chart scale. Max is the value where the indicator is fully filled (for a pie, the whole circle)."**

Validation: Min must be strictly less than Max. If they are equal or reversed, the widget won't save.

**Display data legend** — A toggle that adds a legend listing your sensor metrics below the reading. Works for all three display types: Number, Doughnut, and Pie.

### Step 4 — Save

Tap **Save** to add the widget to the dashboard.

## What to expect

Once placed, the widget immediately shows the last known value from each sensor. As sensors report new data, the display updates live.

The value shown is the last one received. If a device has been offline or silent, the widget continues showing the last reading it got — it does not clear the display. Check the sensor's last-reported time on the device page before acting on a reading if the device might be offline.

If a sensor hasn't reported yet, the widget shows **"Waiting for live data"** in the reading area. If no metrics have been configured, it shows **"Add a metric to start visualizing data"** or **"Choose data source and add metric"**.

## Home examples

**Is the bedroom light on or off right now?**
A light sensor reports 1 when on and 0 when off (an INTEGER). Number widget with two conditions: "On" — Number, From 1, To 1 — yellow; "Off" — Number, From 0, To 0 — grey. You see yellow when the light is on, grey when it is off — no number needed.

**Front door — open or closed right now?**
A contact sensor reports 1 (open) or 0 (closed). Conditions: "Open" — red; "Closed" — green. The widget turns red the moment someone opens the door and returns to green when it closes.

**Leak sensor — is anything happening?**
A moisture sensor reports 1 when wet, 0 when clear. Conditions: "Leak detected" — red; "Clear" — green. You see the current status at a glance without reading a number.

**Living room temperature — what is it right now?**
A Number widget with conditions: green 18–24°C "Comfortable", yellow 15–18°C "Cool", red below 15°C "Cold". You're not asking what the temperature was yesterday — just what it is right now.

**Water storage tank — how full is it right now?**
A Doughnut widget for a tank sensor reporting liters. Min: 0, Max: 500. The ring shows the current fill level at a glance. Conditions: green above 300L "Plenty", yellow 100–300L "Getting low", red below 100L "Refill soon".

**Garden soil moisture — does it need water today?**
A Pie widget for a soil sensor reporting 0–100%. Min: 0, Max: 100. Conditions: green 40–80% "Good", yellow 20–40% "Water soon", red below 20% "Dry". The filled circle makes the current moisture level immediately readable.

## See also

- [Conditions](conditions.md) — Define color rules for each metric: what green, yellow, and red mean for that specific sensor in that specific place
- [Adding Widgets](README.md) — How to open edit mode and use the widget picker
