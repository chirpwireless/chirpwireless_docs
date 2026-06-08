---
description: Turn a DXF floor plan into walls for your 3D home — set the source unit and preview before importing.
---

# Importing a Floor Plan

If you already have a floor plan of your home — from when you bought the place, from a renovation, from an estate-agent listing — you don't have to draw your home from scratch. The editor can read a **DXF** file, the standard format that design and drawing programs export, and turn it straight into walls.

It's the quickest route to an accurate model: the layout comes in already shaped and to scale, and you get to spend your time on the fun part — furnishing rooms and connecting sensors.

## What you need

* A `.dxf` file of your floor plan. Architects, builders, and home-design apps can all export DXF.
* The file is read right in your browser. Nothing is sent anywhere until you save the widget.

## Bringing in a file

1. On the bottom toolbar, click **Build**, then click **Trace from map** — the import window is reached from the same building-tools row.
2. In the import window, click **Choose file** and pick your `.dxf` file.
3. The window reads the file and shows you a **preview** of the walls it found, so you can check it looks right before anything is added.
4. Have a look at the **Options** and the count of what was found (below).
5. Click **Import**. The plan's lines become walls, placed on the floor you're currently working on.

If the file can't be read, the window will tell you. If it reads but doesn't contain any walls, it says that too — some plan files only hold labels and measurements, with no actual walls.

## Options

Two settings control how the plan is read:

* **Source unit** — the unit your plan was drawn in: **Millimeters**, **Centimeters**, **Meters**, **Inches**, **Feet**, or **Unitless**. The editor reads the unit from the file when it can and fills this in for you; change it if the file got it wrong. This is the setting that decides whether your home comes in at the right size — if the imported plan looks far too big or far too small, the source unit is almost always why.
* **Arc segments** — how smoothly curved lines are drawn, since walls are made of straight pieces: **Low**, **Medium**, or **High**. Medium is fine for most homes.

The preview updates every time you change a setting, so you can get the size right just by looking.

## What was found

The window shows a count of what the import did — how many **Walls** it created, how many curved shapes it approximated, and how many **Skipped entities** it left out. **Warnings** explain anything that was dropped. A few skipped items is completely normal: a plan file carries lots of things that aren't walls — text, dimension lines, furniture symbols — and only the walls belong in your model.

## After importing

The imported walls work exactly like walls you draw yourself. Click any of them to set the height, thickness, and material, add doors and windows, and keep building. If something's not right, **Undo** (Ctrl+Z) takes the import back out so you can change the source unit and try again.

A nice workflow: import the shell from the plan file, switch to the flat **2D view** to check the rooms, then draw any inside walls the plan didn't have — and you're ready to furnish.

## Tips

* If your home imports at the wrong size, fix the **Source unit** and import again.
* Importing a multi-floor home? Add the floor first (see [Floors and levels](floors-and-levels.md)), switch to it, then import that floor's plan.
* The tidier the plan file, the cleaner the import. If a plan is crowded with extra layers, exporting just the walls from the design app gives the best result.

## See also

* [Drawing your home](drawing-your-building.md) — Draw or adjust walls by hand
* [Tracing from the map](tracing-from-the-map.md) — Build from a satellite map instead
* [Floors and levels](floors-and-levels.md) — Import each floor onto its own level
