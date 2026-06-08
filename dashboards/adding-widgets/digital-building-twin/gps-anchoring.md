---
description: Tie your 3D home model to real latitude and longitude, automatically from a map trace or by hand.
---

# GPS Anchoring

Your Digital Building Twin is a model of a real place — and a real place sits somewhere on the map. GPS anchoring records that: it ties your home, and points inside it, to actual latitude and longitude. It gives your model a real-world location to sit at.

This page covers the two ways your home gets anchored, and how to manage anchors from the Sensors panel.

## Two ways to anchor your home

### Anchored automatically when you trace from the map

If you built the shell of your model by [tracing it from the satellite map](tracing-from-the-map.md), you drew it on real-world coordinates — so it's already anchored. Importing the trace saves your home's location automatically, with no extra step. If you traced your home from the map, you're done.

### Anchored by hand

You can also place anchors yourself, on any model — including one you drew from scratch or imported from a plan file. This is done in the **GPS Anchors** section at the bottom of the Sensors panel.

1. On the bottom toolbar, click **Sensors**, and find the **GPS Anchors** section.
2. Click **Add by click**. The editor switches into pick mode with the prompt **Click on the scene to pick a point**.
3. Click a point in your model — a corner of the house, a spot you know the coordinates of.
4. A small form appears showing the point you picked. Type in its real **Latitude** and **Longitude**.
5. Click **Save**. The anchor joins the list, labelled **A**, **B**, **C**, and so on.

Add as many as you like. A couple of known points — opposite corners of the house, say — are enough to fix your model onto the real map.

## The center point

As you add anchors, the editor works out a **Center** — the average of all your anchor points. It's shown at the top of the anchor list with its latitude and longitude, and it represents where, on a real map, your home sits.

## Managing anchors

The GPS Anchors section lists every anchor with its coordinates, and each one can be removed on its own. There's also a switch to show or hide the anchor markers in the model — handy to keep them visible while you set things up and hidden afterwards for a clean view.

## What anchoring is for

GPS anchoring gives your Digital Building Twin something a plain 3D model doesn't have: a real place in the world. Your home and its anchored points aren't floating in empty space anymore — they have real coordinates.

It puts your home on the map, which is the groundwork for map-aware features down the line. For now, think of it as giving your model its address: it knows where it really is.

## Tips

* Trace your home from the map and anchoring is already done — open the GPS Anchors section and you'll see the anchors the trace created.
* When anchoring by hand, pick points you actually know the coordinates of — a phone's map app can give you the latitude and longitude of a spot if you tap and hold it.
* Spread your anchors out — points at opposite corners of the house fix it more firmly than two points close together.
* Hide the anchor markers once you're set up, so the dashboard view stays focused on your sensors.

## See also

* [Tracing from the map](tracing-from-the-map.md) — Anchoring happens automatically when you trace
* [Pins and live readings](drop-pins-and-live-values.md) — Mark live readings inside the model
* [Editor tour](editor-tour.md) — Finding the Sensors panel
