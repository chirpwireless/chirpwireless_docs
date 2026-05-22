# Adding Widgets

A dashboard comes alive when you add widgets — the individual display panels that show what your sensors are doing right now. But the same temperature sensor in the bedroom and the same temperature sensor watching a fridge are not the same thing. One widget shows comfort. The other shows whether your groceries are safe. The value is identical in type; the meaning is entirely different.

This is what widgets are designed for. You choose what each one shows, set the ranges and colors that match the context, and give it a name that makes sense for where it lives. Two widgets can read from the same sensor and look completely different because you've configured them for different purposes.

## How to add a widget to a dashboard

Before you can add widgets, you need a dashboard. If you haven't created one yet, see [Building a Dashboard](../building-a-dashboard.md).

**Opening edit mode:**

Open the dashboard, tap the **actions menu** (three dots) in the top right, and select **Edit dashboard**. The dashboard enters edit mode — you'll see a **Cancel** button and a **Save** button appear in the header, replacing the Live Data indicator.

**If the dashboard is empty:**

An empty dashboard shows **"You have no widgets here"** with an **Add widget** button in the center. Tap it to open the widget picker.

**If the dashboard already has widgets:**

In edit mode, a **plus (+) button** appears — use it to add more widgets. You can also tap the **three-dot menu** on any existing widget to edit, move, resize, or delete it.

**Saving your changes:**

After configuring a widget, tap **Save** in the widget settings to add it to the dashboard. When you're done arranging, tap **Save** in the dashboard header to exit edit mode and keep your layout.

## Choose the right widget

| Widget | Use it when | What it shows |
|--------|------------|---------------|
| [Last Data](last-data-widget.md) | You need to know what something is doing right now | The latest value received from one or more sensors |
| [Chart](chart-widget.md) | You need to see how a value changed over time | A historical graph plus the live current reading |
| [Image Map](image-map-widget.md) | You want to see sensor data pinned to a floor plan, room photo, or diagram | Your own uploaded image with live numeric readings pinned to their locations |
| [Map](map-widget.md) | You want to see where a GPS-reporting device is right now | Current position on a real outdoor interactive map, plus one sensor reading on the marker |
| [Digital Building Twin](digital-building-twin/README.md) | You want a 3D model of your home with sensors mapped to real rooms and objects | A 3D editor that turns your home into a live picture, colored by what your sensors say |

## What comes next

- [Last Data Widget](last-data-widget.md) — Latest sensor values, gauges, and per-sensor conditions
- [Chart Widget](chart-widget.md) — Time-series graphs with live current reading and threshold bands
- [Image Map Widget](image-map-widget.md) — Floor plans with draggable live-data pins
- [Map Widget](map-widget.md) — GPS tracker location with route history
- [Digital Building Twin](digital-building-twin/README.md) — A 3D model of your home that lights up with live sensor readings
- [Conditions](conditions.md) — Color rules that turn readings into meaning
- [Organizing Your Views](../organizing-your-views.md) — Group dashboards into folders
