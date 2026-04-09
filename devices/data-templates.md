# Data Templates

Data templates tell Chirp what your sensors are measuring and how to display it. They're the reason a temperature reading shows up as "22.5 °C" instead of a mysterious number — and why a humidity sensor from one manufacturer shows the same kind of data as a humidity sensor from a completely different brand.

Many common sensor types come pre-configured, so you might never need to touch data templates at all. But if you're using a less common sensor or want to customize how measurements are labeled, this is where you do it.

## How to get there

There are two ways to reach data templates:

- **From a sensor list** — When viewing your sensors in a connection's **Connected Devices** tab, click the **Metrics Templates** button in the top-right area.
- **Direct URL** — Navigate to `/metrics` in your browser.

## The three tabs

Data templates are organized into three tabs, each handling a different layer:

### Units

Units define the measurement units available in Chirp — things like °C, °F, %, lux, mV, and so on.

**What you see:** A table with **Name** and **Symbol** columns, plus edit and delete buttons.

**To add a unit:**
1. Click **Add Unit**.
2. Enter a **Name** (e.g., "Celsius") and **Symbol** (e.g., "°C").
3. Click **Save**.

Some units come built in and can't be edited — these cover the most common measurements.

### Normalized Keys

Normalized keys are standard names for what a measurement represents. Instead of every sensor using its own name for temperature (one might call it `temp`, another `temperature`, another `t_celsius`), you create one normalized key called `temperature` and map all of them to it.

**What you see:** A table with **Normalized Key** and **Type** columns, plus edit and delete buttons.

**To add a key:**
1. Click **Add Normalized Key**.
2. Enter a name — use something descriptive and lowercase, like `temperature`, `humidity`, `soil_moisture`, or `battery_level`.
3. Click **Save**.

Built-in keys cover common measurements and can't be edited.

### Metrics

Metrics (also called sensor templates) combine a normalized key, a unit, a value type, and a data type into a complete measurement definition. When you add a sensor, this is what gets attached to map the sensor's raw output into something meaningful.

**What you see:** A table with columns for **Normalized key**, **Unit of measurement**, **Type**, **Data type**, and action buttons.

**To add a metric:**
1. A new row appears at the top of the table.
2. **Normalized key** — Select an existing key or create a new one right from the dropdown.
3. **Unit of measurement** — Pick from your units list (e.g., °C, %, lux).
4. **Type** — Choose the value format:
   - **Integer** — Whole numbers (e.g., battery percentage: 85)
   - **Float** — Decimal numbers (e.g., temperature: 22.5)
   - **String** — Text values (e.g., status: "open")
   - **Boolean** — True/false (e.g., motion detected: true)
5. **Data type** — Choose what kind of data this is:
   - **Telemetry** — Regular sensor readings (temperature, humidity, etc.)
   - **Device Metadata** — Information the sensor reports about itself
   - **User Metadata** — Notes or tags you add manually
6. Click save on the row.

**Filtering:** Use the dropdown filters above the table to narrow the list by type or data type.

## Do I need to set this up?

For most common LoRaWAN sensors, Chirp comes with built-in templates that cover standard measurements. When you register a sensor using a device profile template, the right data templates are often assigned automatically.

You'll want to create custom data templates if:
- Your sensor measures something unusual (e.g., a specific industrial gas)
- You want different display units (e.g., Fahrenheit instead of Celsius)
- You're using a sensor brand that isn't in the template library

For how data templates connect to individual sensors, see [Adding Sensors](adding-sensors.md) and [Sensor Details](sensor-details.md).
