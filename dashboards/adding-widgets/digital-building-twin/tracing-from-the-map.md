---
description: Click your home's outline on a satellite map to turn it into walls and save its real-world location.
---

# Tracing from the Map

No floor plan? No problem. You can build the shell of your home straight from a satellite map. Open the map, find your house, click around its outline, and the editor turns that shape into walls — and remembers where on Earth your home actually is.

This is the easiest way to start when you can see your home from above but don't have any drawings of it. It works just as well for the parts of your property beyond the house — the garden, the driveway, the garage, a shed. It's also how your home gets its **map location**: the trace saves your home's real coordinates, which is what the features in [GPS anchoring](gps-anchoring.md) build on.

## Opening the map

1. On the bottom toolbar, click **Build**.
2. In the building-tools row, click **Trace from map**.
3. A full-screen map opens.

Move and zoom the map until your home is nicely in view — drag to move, scroll to zoom, or use the controls in the corner.

## Tracing your home

1. Click **Trace building** to start. The cursor turns into a crosshair and a hint appears: *Click on the map to add building corners*.
2. Click each **corner** of your home, one after another. Each click drops a point, and the points join up into the outline you're drawing.
3. Go all the way around the edge of the house. The toolbar keeps a running count of your points.
4. Put a point in the wrong spot? Click **Undo** to take the last one back. **Reset** clears everything and starts fresh. **Pause** lets you stop adding points for a moment without losing the ones you have.
5. When you've gone all the way around — three points or more — click **Import**.

The outline becomes walls, one for each side, placed on the floor you're currently on. The map closes and you're back in the editor with the shell of your home in place.

## What gets saved

Importing a traced home does two things:

* **Creates the walls** — one for each edge of the outline you drew, on the active floor.
* **Saves your home's location** — because you drew on a real map, the editor remembers your home's real-world coordinates. That location travels with the model, and it's what the map-based features build on later. See [GPS anchoring](gps-anchoring.md).

## After tracing

The traced walls are just ordinary walls — click any of them to set height, thickness, and material, add doors and windows, draw the inside rooms, and furnish away. Tracing gives you a correctly-shaped, correctly-placed outline; everything inside it you build like normal.

## Tips

* Zoom in close on the map before you start — the bigger your house looks on screen, the more accurately you can click each corner.
* Go around the outline in order, all the way around once. Don't hop from one side of the house to the other.
* For an L-shaped house, click a point at every corner — including the inside corners where the L bends.
* Use **Pause** if you need to move the map partway through, then carry on clicking.

## See also

* [GPS anchoring](gps-anchoring.md) — What your home's saved location is for
* [Drawing your home](drawing-your-building.md) — Add the inside rooms after tracing
* [Importing a floor plan](importing-a-dxf-plan.md) — Build from a plan file instead
