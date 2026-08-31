---
description: Add Chirp dashboard widgets for live sensor data, charts, controls, maps, images, text, and embedded pages.
---

# Adding Widgets

A dashboard comes alive when you add widgets. Some show what your sensors are doing now or how a reading changed; others control a device, plot a location, display an image, or add a note without any sensor connection. For sensor widgets, context matters: the same temperature reading in a bedroom can mean comfort, while in a fridge it can mean whether food is safe.

This is what widgets are designed for. You choose what each one shows, set the ranges and colors that match the context, and give it a name that makes sense for where it lives. Two widgets can read from the same sensor and look completely different because you've configured them for different purposes.

## How to add a widget to a dashboard

Before you can add widgets, you need a dashboard. If you haven't created one yet, see [Building a Dashboard](../building-a-dashboard.md).

**Opening edit mode:**

Open the dashboard, tap the **actions menu** (three dots) in the top right, and select **Edit dashboard**. The dashboard enters edit mode — you'll see a **Cancel** button and a **Save** button appear in the header, replacing the Live Data indicator.

**If the dashboard is empty:**

An empty dashboard shows **"You have no widgets here"** with an **Add widget** button in the center. Tap it to open the widget picker.

**If the dashboard already has widgets:**

In edit mode, a **plus (+) button** appears — use it to add more widgets. You can also tap the **three-dot menu** on any existing widget to edit, move, resize, or delete it.

**Reusing a widget you've already set up:**

Once a widget is configured just the way you like it, you don't have to build the next one from scratch.

- **Duplicate** a widget from its three-dot menu to get a copy on the same dashboard — you'll see **"Widget successfully duplicated"**. This is the quick way to cover several identical sensors: set up the first radiator's temperature widget with the ranges and colors you want, duplicate it once per radiator, and just point each copy at its own sensor. If the copy doesn't appear, you'll see **"Could not duplicate widget"** — try again.
- **Move to dashboard** sends a widget to a different dashboard entirely. Handy when the garden soil probe you added to "Kitchen" really belongs on "Garden". If the move doesn't go through, you'll see **"Could not move widget"**.

**Saving your changes:**

After configuring a widget, tap **Save** in the widget settings to add it to the dashboard. When you're done arranging, tap **Save** in the dashboard header to exit edit mode and keep your layout.

## Choose the right widget

| Widget | Use it when | What it shows |
|--------|------------|---------------|
| [Last Data](last-data-widget.md) | You need to know what something is doing right now | The latest value received from one or more sensors |
| [Chart](chart-widget.md) | You need to see how a value changed over time | A historical graph plus the live current reading |
| [Text](text-widget.md) | You want a heading, reminder, or note on the dashboard | Text you write yourself, with no sensor connection |
| [Image](image-widget.md) | You want to see sensor data pinned onto an image — a floor plan, a room photo, a diagram | Your own uploaded image with live numeric readings pinned to their locations |
| [Map](map-widget.md) | You want to see where a GPS-reporting device is right now | Current position on a real outdoor interactive map, plus one sensor reading on the marker |
| [Control](control-widget.md) | You want to send a command to a switch, light, thermostat, or other controllable device | A switch, button, input, or slider for the device's available command |
| [iFrame](iframe-widget.md) | You want a web page you check often — weather, traffic, a calendar — right on your dashboard | A live web page from a supported service, embedded in the tile next to your sensors |
| [Digital Building Twin](digital-building-twin/README.md) | You want a 3D model of your home with sensors mapped to real rooms and objects | A 3D editor that turns your home into a live picture, colored by what your sensors say |

## What comes next

- [Last Data Widget](last-data-widget.md) — Latest sensor values, gauges, and per-sensor conditions
- [Chart Widget](chart-widget.md) — Choose a Line or Bar chart for history, current readings, and threshold bands
- [Text Widget](text-widget.md) — Label dashboard areas or leave a household note
- [Image Widget](image-widget.md) — Any image with draggable live-data pins
- [Map Widget](map-widget.md) — GPS tracker location with route history
- [Control Widget](control-widget.md) — Send commands with a switch, button, input, or slider
- [iFrame Widget](iframe-widget.md) — Pin a live web page — weather, traffic, calendar — next to your sensors
- [Digital Building Twin](digital-building-twin/README.md) — A 3D model of your home that lights up with live sensor readings
- [Conditions](conditions.md) — Color rules that turn readings into meaning
- [Organizing Your Views](../organizing-your-views.md) — Group dashboards into folders
