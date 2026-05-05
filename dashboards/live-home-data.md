# Live Home Data

One of the best things about a smart home is knowing what's happening right now — not five minutes ago, not after refreshing a page, but right now. Chirp delivers sensor readings to your screen in real time: the moment a sensor reports a temperature, humidity level, or door status, you see the updated value on your overview or dashboard.

This page explains how live data works in Chirp, what the Live Data indicators mean, and what to check if data isn't showing up.

## The Live Data button on the overview

When you open the [home overview](../overview.md), the header shows **"My board"** alongside a **"Live Data"** label with a small clickable icon. If you hover over it, a tooltip says **"New data is automatically displayed"**.

**You can tap this button.** Tapping it tells Chirp to pull the latest information for the overview — updated sensor counts, gateway status, and notification cards. This is handy when you've just added a new sensor and want to see it appear right away instead of waiting for the next automatic refresh.

## The Live Data indicator on dashboards

When you open any [dashboard](building-a-dashboard.md), the header shows the dashboard name and a **"Live Data"** label with a small icon on the right.

**This one is not a button** — it's a status indicator. You can't tap it, and it doesn't do anything when you hover. It simply tells you that the dashboard is connected and receiving fresh data automatically. As your sensors report new readings, the widgets on the dashboard update on their own.

When you enter edit mode to modify widgets, the Live Data indicator disappears (replaced by the edit controls). It comes back when you exit edit mode.

## How it works

Behind the scenes, Chirp maintains a live connection between your browser (or phone) and the platform. When a sensor sends a new reading:

1. The reading arrives at Chirp through the sensor's connection.
2. Chirp processes and stores it.
3. At the same time, the new value is pushed directly to your screen.
4. Any widget or card displaying that sensor's data updates immediately — no page refresh needed.

The speed of updates depends on how often your sensor reports. A temperature sensor that sends a reading every 5 minutes will update your dashboard every 5 minutes. A motion sensor that reports events instantly will show up as soon as motion is detected.

## "Waiting for live data"

Sometimes a widget or dashboard shows the message **"Waiting for live data"**. This is normal and happens when:

- **A sensor was just added** — It hasn't sent its first reading yet. Give it a moment (or trigger a reading if the sensor supports manual transmission).
- **The reporting interval hasn't passed** — If a sensor reports every 15 minutes, you might need to wait until the next cycle.
- **The sensor is offline** — Check whether the sensor is powered on and within range of your gateway.

## What to check if data isn't appearing

If your overview or dashboard isn't showing fresh data:

1. **Is the sensor online?** Open the sensor's detail page and check the last-seen time. If it's been a while, the sensor may have lost power or connectivity.
2. **Is the gateway running?** *(LoRaWAN sensors)* Your gateway needs to be powered on and connected to your home internet. Check [Checking Gateway Health](../gateways/lorawan-gateways/checking-lorawan-gateway-health.md).
3. **Is the sensor within range?** If the sensor is too far from the gateway, readings may not arrive. Try moving the sensor closer or repositioning the gateway.
4. **Try the Live Data button** on the overview page. Tapping it forces a fresh data pull.
5. **Refresh the page.** In rare cases, the live connection between your browser and Chirp may need to reconnect. A simple page refresh usually fixes this.

## The difference between overview and dashboard live data

| | Overview | Dashboard |
|---|---------|-----------|
| **Live Data control** | Clickable button — tap to refresh | Non-clickable indicator — status only |
| **Tooltip** | "New data is automatically displayed" | No tooltip |
| **What updates** | Summary cards (sensor count, gateway status, warnings) | Individual widget values |
| **Manual refresh** | Yes (tap the button) | No (automatic only; refresh the page if needed) |

Both surfaces receive real-time data automatically. The difference is that the overview gives you an extra manual refresh option through its clickable button.

## What's next

- [Home Overview](../overview.md) — The page where the clickable Live Data button lives.
- [Adding Widgets](adding-widgets/README.md) — Add widgets that display live sensor readings.
- [Checking Gateway Health](../gateways/lorawan-gateways/checking-lorawan-gateway-health.md) — Make sure your gateway is delivering data.
