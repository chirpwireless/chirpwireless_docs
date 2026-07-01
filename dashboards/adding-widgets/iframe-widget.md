---
description: Drop a live web page — a weather map, your calendar, a flight tracker — onto a Chirp dashboard with the iFrame Widget.
---

# iFrame Widget

Your home dashboard is where you glance to see how things are. Some of what you want there isn't a sensor reading at all: the local weather map, the family calendar, the flight your partner is on, the live view from a webcam service. The iFrame Widget lets you pin those web pages right onto your dashboard, so the things you check every morning live in one place instead of a pile of open tabs.

An iFrame Widget shows a live web page inside a tile on your dashboard. The page keeps doing its thing — updating, animating, refreshing — just as it would in its own window, only now it sits next to your temperature, humidity, and door sensors. You give the widget a web address (an **embed link**) from a supported service, name it, and it appears.

Because the tile loads a real page from the web, Chirp only lets you embed sites from a friendly, checked list of services that are safe to show this way. That keeps your dashboard tidy and trustworthy — a tile can only show a page from a service we've okayed, so nothing unexpected ends up on your home screen.

## Add an iFrame Widget

Here's how to add a live local weather map to a dashboard so you can see the forecast next to your sensors. It's the same for anything else you embed — only the link changes.

1. Open your dashboard and tap the **actions menu** (three dots), then **Edit dashboard**. Tap the **plus (+) button** and pick **iFrame** from the widget picker — its tile says *iFrame*, "Connect a weather service or something else."
2. The settings open on the **Data source** tab, with a preview on the right. Look for the **Data source** box.
3. Grab the **embed link** from the service — not the web address at the top of your browser. Most sites tuck it under a **Share** button, then **Embed** or **Get embed code**, which gives you a link (or a snippet of code with a link inside it). On a weather site like Windy, use its **Embed on your website** option and copy the URL it shows.
4. Paste that link into the **Data source** box. Just under it, Chirp shows the services you can embed, sorted into groups — have a look to check yours is there. The link needs to start with **https://**. The preview on the right fills in as soon as the link works; if a link isn't supported or isn't quite right, you'll see a little placeholder instead of the page.
5. Tap **Next** to go to the **Appearance** tab.
6. Type a **Widget name** you'll recognize — like "Weather". You can add a **Description** too, but it's optional.
7. Tap **Save** in the settings, then **Save** in the dashboard header. Your weather map is now live on the dashboard, right beside your sensors.

> **Nothing showing in the preview?** The link probably isn't an embed link. Double-check you copied the one from **Share → Embed** (not the normal page address), that it starts with `https://`, and that the service is in the supported list under the box. A regular link, an `http://` one, or a site that isn't on the list won't load.

## What you can embed

The services you can use are sorted into groups in the picker, so it's easy to find what you're after. A few from each:

- **Dashboards & BI** — Power BI, Looker Studio, Tableau, Grafana. Handy if you already keep a chart of your energy use or solar output somewhere.
- **Maps & location** — Google Maps, OpenStreetMap, Mapbox. Show your neighborhood, a trip route, or a spot you're keeping an eye on.
- **Weather & air quality** — Windy, Meteoblue, Ventusky, IQAir. See the forecast, the wind, or today's pollen and air quality at a glance.
- **Video & camera feeds** — YouTube, Vimeo, Twitch. Embed a published stream or a favorite live view.
- **Transport & flights** — Waze, Flightradar24, FlightAware. Watch a flight come in so you know when to leave for the airport.
- **Shipping & parcel tracking** — 17TRACK, AfterShip, TrackingMore. Follow that parcel you're waiting on.
- **Finance & markets** — TradingView, Investing.com, Trading Economics. Keep an eye on a price or a market you follow.
- **Status & docs** — Statuspage, Instatus, Google Docs. Check whether a service you rely on is up, or pin a shared note.
- **Calendars & forms** — Google Calendar, Google Forms, Microsoft Forms, Calendly. Put the family calendar front and center.

The list you see in the widget is always up to date. If the service you want isn't there, tap the **request** link under the Data source box and ask us to add it — we'll take a look and see if it can join the list.

## Home examples

**Morning weather, right where you look**
Add a Windy or Meteoblue map to your main dashboard and it sits next to the indoor temperature and humidity. One glance tells you both what it's like outside and whether you left a window open.

**The family calendar on the wall tablet**
If you keep a dashboard on a hallway tablet, embed your shared Google Calendar. Everyone sees the week's plans beside the home's sensors — school runs, bin day, and whether the garage door got left up.

**Track a flight home**
Waiting to pick someone up? Drop a Flightradar24 embed onto a dashboard and watch the flight approach, so you head out at the right moment instead of guessing.

## What the widget shows

On your dashboard, the iFrame Widget shows the web page live inside its tile. The page updates on its own, just like it would in a browser — there's no separate refresh setting on the widget. In edit mode you can drag the tile around and resize it, so a busy page like a map gets the space it needs.

The iFrame Widget is just for viewing — it doesn't read your sensors, run automations, or send alerts. Use it to keep the web pages you care about close by, and let your sensor widgets (Last Data, Chart, Image, and the Digital Building Twin) handle your device readings.

## See also

- [Adding Widgets](README.md) — Edit mode and the widget picker
- [Chart Widget](chart-widget.md) — See how a sensor reading changed over time
- [Digital Building Twin](digital-building-twin/README.md) — A live 3D model of your home
