# Image Map Widget

Upload any 2D image and pin live sensor readings directly onto it. The image can be a floor plan, a room photo, a garden layout, a machine diagram — anything where you want to see sensor data in a spatial context. Each pin shows the sensor's current value and an icon. The pin color changes automatically as conditions trigger — so a cold room shows blue, a comfortable room shows green, and a room that needs attention shows red, all on the same image.

You see the reading where the sensor is. Instead of reading a list of device names and matching them to locations, you look at the actual space and see what each part is doing right now.

You can add multiple layers to a single widget — one per floor, one per room, or however you want to organize the space. A floor switcher appears on the widget when you have more than one layer.

**Note:** Image Map only works with numeric sensor readings — INTEGER and FLOAT types. Temperature, humidity, battery percentage, soil moisture, CO2 levels, fill levels, and similar numeric values can be pinned. Sensors that report text or binary values are not available in the metric selector.

## Setting up an Image Map widget

### Step 1 — Choose Image Map from the widget picker

Open dashboard edit mode and tap **Image Map** in the widget picker. (See [Adding Widgets](README.md) for how to open edit mode.) The settings panel opens. Unlike other widgets, **the Appearance tab opens first** — you need to upload your image before you can place pins.

### Step 2 — Appearance tab: upload your image and configure layers

The Appearance tab is titled **"Add image map images and layers"** with the subtitle **"Upload images for each layer..."**

**Widget name** *(required)* — The title shown on the widget. The placeholder reads **"Type widget name here"**.

**Description** — An optional subtitle.

**Layers:**

Every Image Map has at least one layer. The first layer is created automatically and cannot be deleted.

For each layer:
- **Layer name** *(required)* — Give the layer a clear name ("Ground floor", "Garden", "Living room"). If the name is empty, the field shows a red border.
- **Upload image** — Tap to upload a floor plan or photo. Accepted formats: **PNG or JPG**. A hint reads **"PNG or JPG format"**. After uploading, a thumbnail preview appears.
- **Upload new** — Replace the current image.
- **Delete image** — Remove the image from this layer.
- **Expand/collapse arrow** — Minimize a layer's settings to keep the panel tidy.

Tap **Add new layer** to add additional floors or rooms. Each layer has its own image and its own set of sensor pins.

**Zoom controls** — In the bottom right of the image preview, plus (+) and minus (−) buttons let you zoom in and out between 0.5× and 3× in 0.1× steps. These controls are **only visible in edit mode** and are for positioning pins accurately — use them to zoom in before dragging a pin to its exact location. They don't affect how the widget appears on the dashboard.

### Step 3 — Datasource tab: add sensors and place pins

The Datasource tab is titled **"Image map configuration"** with the subtitle **"Configure image layers and data sources."**

For each layer, you can add one or more devices:

1. Tap **Add datasource** under a layer. A device selector appears.
2. Choose a device whose numeric sensors you want to show on that layer.
3. After selecting a device, metric rows appear. Each row shows:
   - **Data type** — set to Telemetry
   - **Device metric** — choose which numeric sensor to pin (only INTEGER and FLOAT sensors are offered)
   - **Icon** — pick an icon for the pin
   - **Conditions button** — labeled **"Conditions: N"** where N is the current condition count. Tap to define what color the pin shows at different values. See [Conditions](conditions.md) for details.
   - **Delete** — remove this metric from the layer
4. Tap **Add metric** to include more sensors from the same device. The button grays out once all of the device's numeric sensors have been added.

**Placing pins on the image:**

After you add a metric, its pin appears on the layer image. **Drag the pin to the exact location** of that sensor — the corner of the room where the temperature sensor sits, the window where you placed the humidity probe, the plant pot for the soil moisture sensor. The pin position is saved when you save the widget.

Use the zoom controls in the Appearance tab to zoom into the image and place pins precisely.

### Step 4 — Save

Tap **Save** to add the widget to the dashboard.

## What the widget shows

On the dashboard, each layer shows its image with colored circular pins at the positions you set. Each pin shows:
- The sensor's icon
- The current live value and unit

**Pin color is driven entirely by conditions.** The first matching condition wins. If no condition matches, the pin shows the default color you set in the Conditions modal. If no default is set, the platform applies a default color.

**Floor switcher** — When your widget has two or more layers, a floor switcher appears in the bottom left of the widget. It is hidden by default and appears when you hover over the widget (and stays visible in edit mode). Tap a layer name in the switcher to see that floor.

Pin values update in real time as sensors report new data.

**Empty states:**
- **"No saved plan"** — Layer has no image uploaded yet
- **"No widget data"** — Widget has no sensors configured

## Home examples

**House floor plan with temperature sensors:**
Upload a floor plan. Add a temperature sensor pin for each room. Conditions: green 18–24°C "Comfortable", yellow 14–18°C "Cool", red below 14°C "Cold". You see instantly which rooms need attention — colored pins on the actual floor plan, no list to read.

**Apartment with humidity monitoring:**
Upload the floor plan, place a humidity pin at each room's air sensor. Conditions: green 40–60% "Good", yellow 60–75% "Elevated", red above 75% "High humidity". The image tells you which rooms need ventilation at a glance.

**Indoor plants — current soil moisture:**
Upload a room photo. Place soil moisture pins on each plant pot. Conditions per plant: green "Well watered", yellow "Water soon", red "Dry". You see which plant needs water without checking each one individually.

**Home workshop or garage — any equipment layout:**
Upload a photo or diagram of your workspace. Pin temperature or air quality sensors to the areas they monitor. The image doesn't have to be a floor plan — any photo where you want to see readings in spatial context works.

## See also

- [Conditions](conditions.md) — Define color rules for each metric so pin colors reflect what readings mean in context
- [Maps and Device Placement](../maps-and-device-placement.md) — Place stationary sensors on an outdoor or street map (a different feature)
- [Adding Widgets](README.md) — How to open edit mode and use the widget picker
