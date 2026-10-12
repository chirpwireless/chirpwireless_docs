---
description: Turn a DXF floor plan into walls for your 3D home — set the source unit and preview before importing.
---

# Importing a Floor Plan

If you already have a floor plan of your home — from when you bought the place, from a renovation, from an estate-agent listing — you don't have to draw your home from scratch. The editor can read a **DXF** file, the standard format that design and drawing programs export, and turn it straight into walls.

Heads up: this import is still in **beta**, and the window says so — *DXF import is in beta and may not work perfectly. Check the result after import.* The preview is your safety net, and a plan exported straight from a design app usually reads better than one that was scanned or converted.

It's the quickest route to an accurate model: the layout comes in already shaped and to scale, and you get to spend your time on the fun part — furnishing rooms and connecting sensors.

## What you need

* A `.dxf` file of your floor plan. Architects, builders, and home-design apps can all export DXF.
* A plain-text (ASCII) DXF. Binary DXF and DWG files can't be read, so if your plan is a DWG, save a copy as DXF in the program you opened it with.
* The file is read right in your browser and is not uploaded. Nothing leaves your computer until you save the widget.

## Bringing in a file

1. On the bottom toolbar, click **Build**. In the row of building tools, click **Import from file** (it sits beside **Trace from map**).
2. A full-screen window titled **Import from file**, with a **Beta** badge, opens on an **Import a floor plan** screen. Click **Choose file**, or drag a `.dxf` file anywhere onto the window.
3. The window reads the file ("Reading file…") and draws it. A sidebar on the right gives you the controls below, and the **Import** button at the top is enabled once there is something to import. **Cancel** closes the window without changing your model.
4. Follow the four numbered steps at the top of the sidebar, which tick off as you go: drag a rectangle around one floor plan, check the walls, doors and windows and add it as a level, repeat for the other floors, then import all levels at once.
5. Click **Import** (it reads **Import levels: 2** once two levels are lined up). The plan arrives as walls, doors, and windows on the levels you chose.

If the file has no usable lines, the window says **No supported geometry in this file** ("The file has no lines, polylines, arcs or circles to turn into walls."). If it can't be read at all, it asks you to make sure it is a text DXF. **Choose another file** takes you back to the picker.

## How do I import several floors from one drawing?

Many plans put the ground floor, the upper floor and sometimes the roof side by side on one sheet. Each of them can become its own level:

1. Drag a rectangle around one floor plan on the preview. The area you selected is outlined, and a card with a dashed border appears under **Levels to import**.
2. In the card, open the **Level** list and pick where the plan should go. Each choice is labeled **(new)** for a level that doesn't exist yet, **(empty)** for an existing level with nothing on it, or **(replace)** for a level that already has objects. Levels already taken by another floor in this import are greyed out.
3. The line under the list tells you what was recognized, for example "12 walls · 3 doors · 4 windows", or "Recognising walls…" while it works, or "Walls could not be recognised in this area." If stairs were found, the card adds "Stairs were recognised and left out."
4. Click **Add as** followed by the level's name to put the plan in the list, or **Clear selection** to start over. The same plan can't go to two levels: if you pick a taken level you'll see "Another floor already goes to this level."
5. Repeat with a new rectangle for each other floor. Every added floor appears in **Levels to import** with its own **Level** list and a **Remove level** button.

If you don't draw a rectangle at all, the sidebar says "Nothing selected yet. Without a selection the whole drawing is imported as one level." and offers a single **Level** list for it.

A very large selection is refused with "Too many walls to import (N). Select one floor plan or fewer layers." Draw a tighter rectangle or turn off some layers.

When an import would write over a level that already has objects, a **Replace** question appears first ("Replace Ground floor?") and tells you how many walls, doors and windows, and other objects will be deleted and that devices bound to them will be unbound. Choose **Replace** to continue or **Cancel** to keep your level.

## What are the sidebar settings?

* **Drawing** shows the file name, how many elements were skipped ("Text, dimensions, hatches and blocks are not imported"), and any warnings. **Drawing units** is the unit the plan was drawn in: **Millimeters (mm)**, **Centimeters (cm)**, **Meters (m)**, **Inches (in)**, **Feet (ft)**, or **Unitless**. A note under it says **Detected from the file** when the editor found the unit, "The file does not declare its units. Check the scale in the preview." when it didn't, or **Differs from the units declared in the file** when you changed it. This is the setting that decides whether your home comes in at the right size: if the preview looks far too big or far too small, the unit is almost always why. **Choose another file** swaps the drawing, and **Reset file** clears it.
* **Recognition** has two switches and a list. **Detect doors and windows** turns gaps and symbols in the walls into door and window objects. **Import single lines as walls** also turns lone lines into walls, which helps with plans drawn as simple outlines. **Curve smoothness** is **Low (8)**, **Medium (16)**, or **High (32)**: arcs and circles become straight wall pieces, and more segments look smoother but add walls. Medium is fine for most homes.
* **Layers** lists every layer in the file with a checkbox and the number of lines on it. Untick layers that hold furniture, hatching, or notes so only the structure is read.

The preview legend explains the colors: **Walls**, **Doors**, **Windows**, **Passages**, **Drawing lines**, **Current selection**, and **Level to import**. Everything updates as you change a setting, so you can get the size and detail right just by looking.

Warnings can include "the drawing has no dimensions or blocks (converted from PDF or exploded) — walls may be recognised inaccurately", which means the plan was flattened on its way to you. If you can get the original drawing, use that. A few skipped items is completely normal: a plan file carries lots of things that aren't walls.

## After importing

The imported walls work exactly like walls you draw yourself. Click any of them to set the height, thickness, and material, add doors and windows, and keep building. If something's not right, **Undo** (Ctrl+Z) takes the import back out so you can change the settings and try again.

A nice workflow: import the shell from the plan file, switch to the flat **2D view** to check the rooms, then draw any inside walls the plan didn't have, and you're ready to furnish.

## Tips

* If your home imports at the wrong size, fix **Drawing units** and import again.
* Importing a multi-floor home? Pick a level for each floor plan in the import window (see [Floors and levels](floors-and-levels.md) for how levels work) and import them together.
* The tidier the plan file, the cleaner the import. If a plan is crowded with extra layers, exporting just the walls from the design app gives the best result.

## See also

* [Drawing your home](drawing-your-building.md) — Draw or adjust walls by hand
* [Tracing from the map](tracing-from-the-map.md) — Build from a satellite map instead
* [Floors and levels](floors-and-levels.md) — Import each floor onto its own level
