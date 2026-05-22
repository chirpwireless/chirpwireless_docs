# Drawing Your Home

The walls, doors, and windows you draw are what make the model recognizably *your* place — not a generic box, but your home, with the kitchen where the kitchen is and the back door where the back door is. A few minutes of drawing is all it takes. This page shows you how.

Prefer not to draw it all by hand? You can import a floor plan or trace your home from a map instead — see [Importing a floor plan](importing-a-dxf-plan.md) and [Tracing from the map](tracing-from-the-map.md). And you can mix the approaches: trace the outside, then draw the inside walls yourself.

## Drawing in 2D or 3D

The editor shows your model in two ways, and you can draw in either:

* **2D view** looks straight down, like a paper floor plan. It doesn't rotate, so it's the easy view for getting room shapes right.
* **3D view** shows the walls standing up, so you can see how it really looks.

Flip between them with the **3D / 2D** switch on the floor buttons. Most people sketch the layout in 2D and then pop into 3D to admire it.

## Drawing a wall

1. On the bottom toolbar, click **Build**. The building tools appear.
2. Click **Wall**.
3. Click once in the view to drop the **start** of the wall.
4. Move the mouse — a preview wall stretches out, with its length shown in meters as you go.
5. Click again to drop the **end**. The wall appears.
6. The tool stays on, so you can carry straight on to the next wall. Each wall is its own two-click action.

Walls snap to a grid as you draw, which keeps your corners square and your rooms tidy without any careful aiming. If a new wall crosses one that's already there, the older wall splits at the crossing — handy later, because you can color each piece on its own.

Done drawing? Press **Escape**, right-click, or click **Build** again.

## Adding doors and windows

Doors and windows go *into* a wall, so draw your walls first.

1. Click **Build**, then click **Door** or **Window**.
2. Click on a wall where you want the opening.
3. It's cut into the wall.

Switch to **Select** and click a door or window to tidy it up in the settings panel:

* **Doors** — Width, Height, where it sits along the wall, which side it's **hinged**, and which way it **swings** (inward or outward).
* **Windows** — Width, Height, where it sits along the wall, how high off the floor, and the sill depth.

## Drawing a fence

A fence draws just like a wall — click **Build**, click **Fence**, then click a start point and an end point. Fences are great for the parts of your property that aren't house: the garden boundary, the edge of the driveway, a yard.

## Tweaking walls afterwards

Switch to **Select** and click a wall to open its settings:

* **Length** — shown so you can check it.
* **Height** — how tall the wall is.
* **Thickness** — how thick it is.
* **Material** — a row of looks to choose from (white, brick, concrete, wood, glass, metal, plaster, tile, marble) plus a **custom** color. It's purely for appearance — it doesn't change anything about sensors — but a brick exterior and white interior walls make the model feel like home.

To remove a wall, select it and press **Delete**, or use the Delete button in its settings.

## Naming things as you go

As your home takes shape, open the **Scene** panel and give your walls and rooms real names — double-click to rename. "Living room wall" beats "Wall 12," and good names make connecting sensors much quicker later on.

## Tips

* Draw the outside walls first, then the inside ones. The grid snap keeps it all lined up.
* Lay it out in 2D, then switch to 3D to check the heights and the doorways look right.
* Undo (Ctrl+Z) walks back through everything you've drawn, so don't be afraid to experiment.
* It doesn't have to be a perfect architect's drawing — it just has to look enough like your home that you know which room is which at a glance.

## See also

* [Importing a floor plan](importing-a-dxf-plan.md) — Start from a plan file
* [Tracing from the map](tracing-from-the-map.md) — Trace your home from a satellite map
* [Floors and levels](floors-and-levels.md) — Add upstairs, downstairs, the basement
* [Placing objects](placing-objects.md) — Furnish the rooms
