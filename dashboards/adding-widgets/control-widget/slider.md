---
description: Add a Slider Control to a Chirp dashboard to set a value like brightness or volume by sliding across a range.
---

# Slider Control

The **Slider** lets you set a **value** by sliding, instead of a plain on/off. Drag it up or down and it sends that value to the device.

## When to use it

A Slider is great for anything you adjust by amount rather than just switching: **brightness** of a lamp, a dimmer **level**, **volume**, or any setting that moves across a range.

## What you need first

* A device with a command on its **Commands & States** tab whose **input takes a number** (see [Setting up a command](../../../devices/commands/creating-commands.md)).
* A **Device metric** that reports the current value, so the slider shows where it's set.

## How to set it up

1. Open your dashboard in **edit mode** → **Add widget** → **Control**.
2. **Datasource** tab: pick the **Device** and the **Device metric** for the live value. Tap **Next**.
3. **Appearance** tab: type a **Widget name**, then under **Widget type** choose **Slider**.
4. Choose the **Slider type** — **Simple**, **Circular**, or **Vertical** — whichever looks best on your dashboard.
5. Set the **Command** it controls, the **Parameter** it sets, and a starting **Value**.
6. Add **Start and End labels** for the range (for example `0` and `254`) and toggle **Display** to show them. Pick a **Slider color** and toggle the name/last-update line.
7. Tap **Save**.

<figure><img src="../../../.gitbook/assets/control-widget-slider.jpg" alt="Vertical Slider Control setting a lamp's brightness on a Chirp dashboard"><figcaption></figcaption></figure>

## What happens when you use it

Sliding sends the command with the new value, the same way the device's States tab does. The slider follows the **Device metric**, so it shows the value the device is actually reporting.

## Common mistakes

* **Choosing a command that's only on/off** — a slider needs an input it can set to a number; a plain on/off command won't work (use a [Switch](switch.md)).
* **The range doesn't match the device** — set Start and End to the real lowest and highest values (like 0 and 254) so the whole slider maps to values the device accepts.

## See also

* [Control widget](../control-widget.md) — overview and the other control types
* [Controlling Your Devices](../../../devices/commands/) — set up the command this slider controls
