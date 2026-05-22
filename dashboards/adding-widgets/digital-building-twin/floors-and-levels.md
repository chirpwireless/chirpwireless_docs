# Floors and Levels

Most homes have more than one level — an upstairs and a downstairs, maybe a basement, maybe a loft. A Digital Building Twin handles all of them in a single widget. Each floor is its own layer of the same model, with its own rooms, its own furniture, and its own sensors.

This page covers adding floors, moving between them, and the two ways to look at a multi-floor home.

## The floor buttons

A small floating stack of buttons sits to one side of the editor. It's mission control for floors:

* Each floor is a button — **L0**, **L1**, **L2**, and so on. The top floor sits at the top of the stack, the bottom floor at the bottom, just like the real house.
* The floor you're currently working on is highlighted.
* Click any floor button to switch to that floor. Whatever you draw, place, or connect goes onto the floor you're on.

## Adding a floor

* Click the **+** at the **top** of the stack to add a floor **above** the highest one — an attic or loft.
* Click the **+** at the **bottom** of the stack to add a floor **below** the lowest one — a basement or cellar.

When you add a floor, the editor gives it a floor plate shaped like the floor next to it, so a new level starts with a footprint instead of nothing. From there you draw its walls, add its furniture, and connect its sensors on their own.

A tidy way to do a whole house: add all the floors first, then work through them one at a time.

## Removing a floor

Select the floor on the stack, then click the **delete** icon on its button. A model always keeps at least one floor, so the delete button only shows up when there's more than one.

## Two ways to view a multi-floor home

Below the floor buttons are two view switches.

### 3D / 2D

Switches between the **3D view** (spin the model around) and the **2D view** (a flat, top-down plan). It's the same switch covered in the [Editor tour](editor-tour.md). Lay rooms out in 2D, check them in 3D.

### Stack / Solo

This switch decides how the floors are shown, and only appears once your home has more than one floor:

* **Stack** — every floor is shown in its real place, one on top of another. You see the whole house at once. Best for a final look and for setting up the dashboard view.
* **Solo** — only the floor you're on is shown; the others are hidden. Best while you're working — just the one floor, with nothing from above or below getting in the way.

Most people work in **Solo** so each floor is clear while they build it, then flip to **Stack** to see the whole house before saving.

## What the dashboard shows

The dashboard tile shows your home from the angle and view you leave the editor in. For a multi-floor house, framing it in **Stack** with a gentle 3D tilt gives a nice whole-house view on the dashboard. If one floor matters most — the floor with the nursery, the basement with the leak sensor — you can frame that one instead and save.

## Tips

* Give your floors real names in the **Scene** panel — "Upstairs," "Ground Floor," "Basement" — rather than leaving them as L0, L1, L2.
* Build one floor at a time. Switching to **Solo** keeps the floor you're on free of clutter.
* Sensors stay attached to their objects, so a sensor upstairs and a sensor downstairs both stay in the right place no matter which floor you're viewing.

## See also

* [Editor tour](editor-tour.md) — The 3D/2D switch and getting around
* [Drawing your home](drawing-your-building.md) — Build each floor
* [Connecting sensors and colors](binding-sensors-and-colors.md) — Wire up sensors on every floor
