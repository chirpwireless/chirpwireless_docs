---
description: Pin a sensor's exact value into your 3D home, colored by its status, and show or hide every pin at once.
---

# Pins and Live Readings

Color tells you *that* something is up — the nursery's gone amber, the basement's gone blue. Sometimes you also want the actual **number**: not just "the nursery is warm" but "the nursery is 26.3 °C." A pin puts that exact reading right into the model, at the spot it belongs to.

A pin is a marker placed at a particular point in your model. It shows the reading's name and current value with its units, and the pin itself takes the same color as the reading — so it's a label and a status light at the same time.

## Pinning a reading

Pins are added from the Sensors panel, on a metric you've already set up (see [Connecting sensors and colors](binding-sensors-and-colors.md)).

1. On the bottom toolbar, click **Sensors** and find the metric you want to pin.
2. On that metric, click **Pin to scene**.
3. The editor switches into pick mode with the prompt **Click on the scene to pin this metric**.
4. Click the spot in your model where the pin should sit — over the nursery, by the back door, on the driveway.
5. The pin appears there, showing the reading's name and current value.

Once a metric is pinned, you get two more buttons: **Re-pin** to move the marker somewhere else, and **Unpin** to take it off.

## What a pin shows

Each pin is a little teardrop marker with a label hovering above it. The label has the reading's name and its current value with units — `Nursery / Temperature  26.3 °C`. The marker and label are colored by your rules, the same way your objects are: a reading in the "warm" band makes the pin amber, one in the "just right" band makes it green.

So a pin does two things at once — it shows you the exact number, and its color tells you the status without you even having to read it.

## Pins and floors

A pin belongs to the floor it was placed on. In a multi-floor home, a pin you put upstairs shows when you're viewing upstairs and stays out of the way when you're looking at the ground floor — so a tall house doesn't end up with every floor's pins piled on top of each other. See [Floors and levels](floors-and-levels.md).

## Showing and hiding pins

The Sensors panel has a **Show sensor pins** switch. It appears once you've pinned at least one reading, and turns every pin in the model on or off together.

Turn pins **off** for a clean, color-only look — nice for a dashboard you glance at from across the room. Turn them **on** when you want the exact numbers. However the switch is set when you save the widget is how the dashboard tile shows it.

## When to use a pin

For a lot of things, color alone is enough — the garage door doesn't need a number, "open" or "closed" is the whole story. Reach for a pin when the number itself matters:

* The nursery or bedroom, where the exact temperature is what you care about.
* A water tank, where the fill percentage tells you when to top it up.
* Anywhere "how much" matters as much as "is there a problem."

Pin the few readings you genuinely want as numbers, and let color handle the rest. A model covered in pins is as hard to read as a spreadsheet; a few well-placed ones draw your eye exactly where it should go.

## See also

* [Connecting sensors and colors](binding-sensors-and-colors.md) — Set up the metric a pin is based on
* [Floors and levels](floors-and-levels.md) — How pins behave across floors
* [GPS anchoring](gps-anchoring.md) — Place your home on the real-world map
