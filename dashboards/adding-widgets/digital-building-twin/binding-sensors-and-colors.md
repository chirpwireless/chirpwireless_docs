# Connecting Sensors and Colors

This is the step that makes the whole thing worthwhile. Up to now your model is a nice 3D drawing of your home. Connecting sensors brings it to life: a sensor says "open" and the garage door turns red; a sensor reads 26 °C and the nursery shifts from green to amber.

A **connection** links one sensor reading to one or more objects in your model, along with the color rules that decide what color those objects show. This page walks through making that link.

## Opening the Sensors panel

On the bottom toolbar, click **Sensors**. The Sensors panel opens. This is where every connection is set up.

## Step 1 — Add a data source

A data source is one of your devices.

1. Click **Add datasource**. A new card appears.
2. Click **Choose device** and pick the device you want to use.
3. The card now shows the device's name. Add as many data sources as you need — one per device.

## Step 2 — Add a metric

Each device has its own individual readings, called **metrics**.

1. On the data-source card, click **Add metric**.
2. In the **Device metric** dropdown, pick the reading you want — temperature, the door's open/closed state, moisture, and so on.
3. Add more metrics if the device has more readings you want to use.

Each metric is one connection. A sensor that reports both temperature and humidity gives you two metrics, and you can connect each one to different things.

## Step 3 — Connect the metric to objects

1. On the metric, click **Configure**. The metric switches into connect mode and its editor opens up.
2. The editor shows the prompt **Click objects on the scene to bind them**.
3. Click any object in your 3D model — the garage door, a room's wall, a bed, the fridge. Each one you click is linked to this metric and shows up in the editor's **Bound** list.
4. Link as many objects as the reading should control. To unlink one, remove it from the Bound list.
5. When you're done, click **Done**.

One metric can drive several objects at once. Connect a single room-temperature sensor to every wall of that room and the whole room changes color together. The metric's **Bound** count tells you how many objects it's currently linked to.

## Step 4 — Choose the colors

The metric's editor is where you set the colors. Two things decide what an object shows:

* **Default color** — the color used when none of your rules match. Set it with the color picker in the editor.
* **Conditions** — the rules that turn readings into colors. Click **Add condition** to make one. Each condition has:
  * a **color**,
  * a **Name** (a label like "Open," "Too warm," "Leak"),
  * a **Data type** — **Number**, **String**, or **Boolean**,
  * and a test that depends on the type:
    * **Number** — a **From** / **To** range. The rule matches when the reading is inside it.
    * **String** — a single **Value**. The rule matches when the reading is exactly that word.
    * **Boolean** — a **True** / **False** setting. The rule matches a true/false reading.

The rules are checked in order, and **the first one that matches wins**. If none match, the object shows the default color. This is the same color-rule system you already use on your other widgets — see [Conditions](../conditions.md) for the full details.

## Step 5 — Try it out

The metric's editor has a **Value** slider. If the sensor isn't sending live data yet, drag the slider and watch your objects change color in real time — it's the quickest way to check your rules before the model goes on a dashboard. Once the device is reporting, the editor shows the real **Current value** and the model follows your live readings.

## A few examples

**Is the garage door open?** Connect a door sensor's open/closed metric to the garage door object. Add two rules: when the value means "open," show red; when it means "closed," show green. One look at the model and you know.

**Is the nursery too warm?** Connect a temperature sensor to the nursery's walls. Add Number rules: 18–22 °C green ("Just right"), 22–25 °C amber ("Warm"), and set the default to red for anything hotter. The room's color tells you the comfort level at a glance.

**Is the basement dry?** Connect a leak sensor to the basement floor. A Boolean rule — wet `true` → blue — turns the basement blue the instant water is detected.

**Is anyone in the home office?** Connect a motion or occupancy sensor to the home-office room. Occupied shows one color, empty another — so you can see if the room is in use before you walk in for a call.

These are just a starting point. Any sensor in your Chirp setup can be wired to any object in the model — however you'd describe what a reading means for a spot in your home, you can make the model show it. Let your own home give you the ideas.

## Tips

* Give your objects clear names in the **Scene** panel before you connect — clicking the right door is much easier when it's labelled "Garage door."
* Connect one metric to several objects when they share a reading; use separate metrics when each thing has its own sensor.
* Use the test slider to check every rule before you save.
* Keep your rules simple — two or three colors (good / warning / problem) usually say more than a long list.

## See also

* [Conditions](../conditions.md) — The full color-rule reference
* [Pins and live readings](drop-pins-and-live-values.md) — Show the actual number in the model
* [Placing objects](placing-objects.md) — Add the objects sensors connect to
