# Choosing Widgets

Widgets are the individual pieces of information on your dashboard. Each widget connects to one of your sensors and shows its data in a way you choose — a simple number, a colorful doughnut chart, a time-series graph, or a floor plan with sensor readings pinned in place.

The key idea is that widgets are not fixed cards. You control how each one looks and what the numbers mean. A temperature widget for your living room might show a comfortable green range of 18–24°C, while the exact same sensor type in a fridge widget turns red above 5°C. Same data, different context — and the widget makes that context visible.

## Getting into edit mode

You can only add or change widgets when your dashboard is in **edit mode**.

1. Open a dashboard from the sidebar.
2. Tap the **actions menu** (three dots) in the header and select **Edit dashboard**.

Once in edit mode:

- A **plus button** appears in the header — tap it to add a widget.
- **Cancel** and **Save** buttons appear on the right.
- Each existing widget gets a small **three-dot menu** in its top-right corner for editing or deleting.

Remember to tap **Save** when you're done. **Cancel** discards everything you changed.

## What widget types are available

Tap the **plus button** (or the **Add widget** button if your dashboard is empty) to see the widget picker. The available types depend on your plan — you may see all four or just some.

### Device data

**What it shows:** A single reading from one sensor — temperature, humidity, battery level, door status, or any metric your sensor reports.

**When to use it:** When you want a quick, focused view of one specific measurement. Perfect for a "kitchen temperature" or "front door status" card.

**How to add it:**
1. Select **Device data** from the picker.
2. A dialog titled **"Choose a device"** opens. Find your sensor and tap **Choose** (or **Close** to go back).
3. The next dialog (**"2 / Choose one or multiply widgets"**) shows the sensor's available metrics with a live preview. Metrics already on this dashboard are marked **"Already added"**.
4. Pick a metric from the **"Choose widget or widgets"** dropdown and tap **Choose** — or **Back** to pick a different sensor.

### Last data *(plan-dependent)*

**What it shows:** The latest value from one or more sensors, displayed as a number, doughnut chart, or pie chart.

**When to use it:** When you want to see current readings from several sensors at once — for example, temperature, humidity, and CO2 in the same widget.

**What you can customize:**
- **Widget type** — Choose between **Number** (plain reading), **Doughnut** (ring gauge), or **Pie** (filled gauge).
- **Value ranges** *(Doughnut and Pie only)* — Set a **Min value** and **Max value** for each sensor. This defines the scale: for a doughnut showing room temperature, you might set 10–35°C; for a fridge sensor, 0–10°C. The max is where the gauge reads "full."
- **Display data legend** — Toggle on to show a legend identifying each data source.
- **Conditions** — Set color rules per metric. For a room sensor: green for 18–24°C, yellow for 15–18°C, red below 15°C. For a fridge sensor: green for 2–5°C, red above 5°C. See [Conditions](#conditions) below.
- **Multiple data sources** — Add readings from more than one sensor. Tap **"Add datasource"** in the Datasource tab, then tap **"Choose device"** to select a device. Once selected, its available metrics appear. Tap **"Add metric"** to include additional readings from the same device.

### Chart *(plan-dependent)*

**What it shows:** Sensor values over time, plotted as a line or bar chart.

**When to use it:** When you want to see trends — was the bedroom getting warmer last night? Did the garden moisture drop over the week?

**Setting up the data source:** Tap **"Add datasource"**, then **"Choose device"** to pick a sensor. Once selected, tap **"Add metric"** to create the metric row. The Chart widget uses one metric at a time — to change it later, use the **Device metric** dropdown on the existing row. Each metric row also includes a **Data type** dropdown, a **Color** picker for the line or bar color, and a **Delete** button.

**What you can customize:**
- **Widget type** — **Line** chart (smooth trend) or **Bar** chart (discrete intervals).
- **Timeframe** — Choose how far back to look: **Last hour**, **Last day**, **Last week**, or **Last month**.
- **Value range** — Set the Y-axis scale with **From** and **To** values so the chart focuses on the range that matters (e.g., 15–30°C for room temperature instead of 0–100°C).
- **Thresholds** — Add colored bands that highlight important ranges on the chart. Each threshold has:
  - **From** and **To** values (the range it covers)
  - **Label** (e.g., "Comfortable", "Too warm")
  - **Color** (picker)
  - **Show fill** — Shade the area between the threshold lines
  - **Show line** — Draw the threshold boundary lines
  
  For example, on a living room temperature chart: a green band from 18–24°C labeled "Comfortable", and a red band above 28°C labeled "Too warm".

- **Toggles:**
  - **Show average value** — Display the average across the time range.
  - **Show vertical axis lines** / **Show horizontal axis lines** — Grid line visibility.
  - **Display data legend** — Show which color belongs to which sensor.
- **Per-metric color** — Each metric has a **Color** picker to set its line or bar color. Chart widgets do not use the full conditions system — use thresholds (above) to define labeled value bands instead.

### Image map *(plan-dependent)*

**What it shows:** A floor plan or room image with sensor readings pinned to specific spots.

**When to use it:** When you want a visual layout of where each sensor is and what it's reading — a house floor plan with temperature shown at each room's sensor location.

**What you can customize:**
- **Widget name and description** — Give it a clear label (placeholder: "Type widget name here").
- **Layers** — Each layer represents a floor, section, or view of your space. The first layer is created automatically and cannot be deleted.
  - **Add new layer** — Tap to create additional layers.
  - **Layer name** — Editable text field for each layer.
  - **Upload image** — Each layer needs an image. Accepted formats: **PNG or JPG**. After uploading, you see a thumbnail preview with options to **Upload new** (replace) or **Delete** the image.
- **Per-layer data sources** — In the Datasource tab, each layer shows its name and lets you add devices:
  - Tap **"Add datasource"** to add a device to the layer.
  - Choose a device, then select which metrics to display.
  - Add multiple devices per layer — each pinned to the image.
  - Tap **"Add metric"** to include additional sensor readings from the same device.

### Map *(plan-dependent)*

**What it shows:** Your GPS tracker device's location on an interactive map, together with a selected reading from that tracker — any metric it transmits, whatever the device sends.

**When to use it:** When you want to see where a tracker is and check on it at a glance from your home dashboard, without going to the device page. Useful for a family GPS tracker, a pet collar, or a vehicle with a tracker.

The Map widget is specifically for tracker-type devices. If you want to see where a stationary sensor is placed on a map, that's handled through the sensor's detail page — see [Maps and Device Placement](maps-and-device-placement.md).

**Setting up the data source:**

1. Select **Map** from the widget picker.
2. The Datasource tab opens with the title **"Map configuration"** and subtitle **"Configure last data and data sources."**
3. Choose a tracker device from the device selector. Only devices with latitude and longitude readings show up here — these are detected automatically when sensor names match expected location field names.
4. Once a device is selected, pick an **additional metric** to display on the map marker. This is any field your tracker transmits — whatever the device sends and has been mapped as a sensor.

**What you can customize:**
- **Widget name** *(required)* — Give it a clear label so you recognize it on the dashboard.
- **Description** — An optional subtitle under the widget name.
- **Theme** — Choose **Light** or **Dark** for the map tile appearance.
- **Display data legend** — Toggle on to show a legend identifying the displayed metric.

**Using the map after it's on your dashboard:**

The Map widget has a few controls once placed on a dashboard:

- **History** — Tap this to switch to a date range view and browse past location data.
- **Date range button** — When active, shows the selected period as **DD.MM.YYYY - DD.MM.YYYY**.
- **Clear data range** — Resets the view back to the current position.

When a date range is selected, the widget draws your tracker's recorded route as a dashed line connecting all the positions it logged during that period (up to 500 points).

**What to expect:**

After you add the Map widget, the marker shows the tracker's last known location with the value you selected visible on it. The marker color reflects any conditions you've set for that metric — green if everything is normal, red if it crosses a threshold. As the tracker reports new positions, the map updates automatically.

**Troubleshooting:**

- *No device shows up in the device list* — Your tracker may not be transmitting latitude and longitude fields. Check the device detail page to confirm it's reporting location data.
- *Route is empty for a date range* — The tracker wasn't active or didn't report location during that period. Try a wider date range or check that the tracker was powered on.
- *Metric not showing on the marker* — Confirm the tracker is transmitting that specific field. Open the device page to see recent readings.

**Home examples:**

- **Family GPS tracker** — Add a Map widget to your home dashboard so you can see where your partner is on the way home from work, with their speed showing on the marker.
- **Pet GPS collar** — Keep a Map widget on your phone dashboard. When your dog is in the garden, tap History to see where they roamed during the afternoon.
- **Garden sensor on wheels** — If you have a mobile outdoor sensor, the Map widget shows its current position alongside battery level.

## Conditions

Conditions are per-metric color rules that make readings meaningful at a glance. They work the same way across **Last data** and **Image map** widgets. Chart widgets use a simpler per-metric color picker and appearance-level thresholds instead of the full conditions system.

To set up conditions on a metric:

1. In the widget's Datasource tab, find the metric row.
2. Tap the **Conditions** button (it shows the current count, like "Conditions: 2").
3. The conditions dialog opens with the title **"Conditions"** and the note **"The conditions set first will be considered as a priority"**.

For each condition, you set:

- **Condition name** — A label like "Normal", "Warning", or "Critical".
- **Data type** — **Number** (set a From/To range), **String** (match a text value), or **Boolean** (True/False).
- **Color** — A color picker for this condition.

You can also set:
- **Unit** — Override the display unit for this metric.
- **Icon** — Choose a display icon.
- **Default color** — The color when no condition matches.

Tap **"Add condition"** to create additional rules. The first condition in the list has the highest priority.

**Example — room vs. fridge:** A temperature sensor in your living room might have conditions: green for 18–24°C ("Comfortable"), yellow for 15–18°C ("Cool"), red below 15°C ("Cold alert"). The exact same sensor type in your fridge gets different conditions: green for 2–5°C ("Normal"), red above 5°C ("Check fridge"). Same sensor, different meaning — configured through conditions.

## Editing a widget

To change a widget that's already on your dashboard:

1. Enter edit mode.
2. Tap the **three-dot menu** in the widget's top-right corner.
3. Choose **Edit** to reopen its settings, or **Delete** to mark it for removal. The deletion only takes effect when you tap **Save**. If you tap **Cancel**, the widget comes back.

The three-dot menu only appears in edit mode.

## The empty dashboard

If your dashboard has no widgets yet, the center shows:

- **"You have no widgets here"**
- **"Add your first widget to build your dashboard"**
- An **Add widget** button

Tap the button to open the widget picker.

## What's next

- [Building a Dashboard](building-a-dashboard.md) — Create the dashboard first if you haven't yet.
- [Organizing Your Views](organizing-your-views.md) — Arrange dashboards into folders.
- [Live Home Data](live-home-data.md) — Understand how fresh readings reach your widgets.
