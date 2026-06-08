---
description: Show a Chirp reading on a round dial with the Radial Gauge — a needle, a sweep angle you choose, and colored zones for the level.
---

# Radial Gauge Display

<!-- IMAGE: last-data-radial-gauge.jpg — alt: Last Data widget using the Radial Gauge display -->

The Radial Gauge shows a reading on a **round dial**, with a needle pointing to the value — just like the dials on a car dashboard or an old thermostat. Your color conditions wrap around it as arcs, and you can choose how far the dial sweeps, from a near-full circle to a small arc.

It is one of the [Last Data widget](../last-data-widget.md) display types, joining Number, Doughnut, Pie, Tube, and the flat [Gauge](gauge.md).

## Radial Gauge or the flat Gauge?

Both show a reading against a scale with colored zones — they just look different:

* The **[Gauge](gauge.md)** is a flat, sideways bar. It's tidy and lines up nicely when you have several in a row.
* The **Radial Gauge** is a round dial. It has more presence and feels like a real instrument, which makes it lovely for one or two headline readings on a dashboard.

Pick whichever you like the look of — they work the same way underneath.

## Nice for

* A standout reading you want front and center — the water tank level, the home battery charge, the greenhouse humidity.
* Anything with a clear "full" point, so the dial sweeps from empty to full in a way that feels natural.
* Any reading where colored zones make the meaning obvious at a glance.

## Setting one up

It starts like any [Last Data widget](../last-data-widget.md) — add a device, pick a number reading, and set up your [Conditions](../conditions.md). The dial settings appear on the **Appearance** tab once you choose the type.

1. In dashboard edit mode, tap **Last data** in the widget picker.
2. On the **Datasource** tab, **Add datasource**, choose your device, **Add metric**, set **Data type** to **Telemetry**, and pick the reading.
3. Tap **Conditions: N** to set a default color and your colored zones (each with a range and a color), then save.
4. Tap **Next**, give the widget a **name**, and choose **Radial gauge** under **Widget type**. The dial settings appear:
   * **Min value** and **Max value** — the bottom and top of the dial. Min has to be below Max.
   * **Tick marks** — how many little marks ring the dial.
   * **Sweep angle** — how far around the dial goes, from 0 to 360 degrees. The default of 300 leaves a gap at the bottom like a classic dial; turn it up for a full circle or down for a smaller arc.
   * **Radial Gauge name** — a short label for the dial (filled in for you, but you can change it).
5. Toggle the legend on if you'd like, then tap **Save**.

## Home example

**Rainwater tank.** A level sensor in a rainwater tank gets a Radial Gauge set **Min** 0 and **Max** 100 (percent full), with three zones: "Plenty" 60–100 green, "Getting low" 25–60 yellow, "Top it up" 0–25 red. The needle sits high and green after a downpour and swings toward the red as the garden drinks it down over a dry week — a glance from the kitchen tells you where things stand. Want a nudge on your phone when it hits red? Add an [alert](../../../alarm/) for that reading.

## See also

* [Last Data Widget](../last-data-widget.md) — the full setup and the other display types
* [Gauge Display](gauge.md) — the flat version
* [Conditions](../conditions.md) — set what the colors mean
* More displays: [Number](number.md) · [Doughnut](doughnut.md) · [Pie](pie.md) · [Tube](tube.md)
