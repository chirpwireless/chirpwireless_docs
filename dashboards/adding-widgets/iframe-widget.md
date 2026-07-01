---
description: Drop a live web page — a weather map, live traffic, or your calendar — onto a Chirp dashboard with the iFrame Widget.
---

# iFrame Widget

<figure><img src="../../.gitbook/assets/iframe-widget.jpg" alt="Setting up the iFrame Widget — an embed link in the Data source box, the list of supported services below, and a live preview"><figcaption></figcaption></figure>

Your home dashboard is where you glance to see how things are. Some of what you want there isn't a sensor reading at all: the local weather map, the traffic before the school run, the family calendar, a published camera or video feed. The iFrame Widget lets you pin those web pages right onto your dashboard, so the things you check every morning live in one place instead of a pile of open tabs.

An iFrame Widget shows a live web page inside a tile on your dashboard. The page keeps doing its thing — updating, animating, refreshing — just as it would in its own window, only now it sits next to your temperature, humidity, and door sensors. You give the widget a web address (an **embed link**) from a supported service, name it, and it appears.

Because the tile loads a real page from the web, Chirp only lets you embed sites from a friendly, checked list of services that are safe to show this way. That keeps your dashboard tidy and trustworthy — a tile can only show a page from a service we've okayed, so nothing unexpected ends up on your home screen.

## Add an iFrame Widget

Here's how to add a live local weather map to a dashboard so you can see the forecast next to your sensors. It's the same for anything else you embed — only the link changes.

1. Open your dashboard and tap the **actions menu** (three dots), then **Edit dashboard**. Tap the **plus (+) button** and pick **iFrame** from the widget picker — its tile says *iFrame*, "Connect a weather service or something else."
2. The settings open on the **Data source** tab (headed "iFrame configuration"), with a preview on the right. Look for the **Data source** box.
3. Grab the **embed link** from the service — not the web address at the top of your browser. Most sites tuck it under a **Share** button, then **Embed** or **Get embed code**. Sometimes you get a tidy link; sometimes you get a whole chunk of code like `<iframe width="650" height="450" src="https://…/embed…" frameborder="0"></iframe>`. **Copy only the bit inside `src="…"`** — the address that starts with `https://` — and nothing else. Don't paste the whole `<iframe …>` block; the box only wants the link, and pasting the full tag won't work.
4. Paste that link into the **Data source** box. Just under it, below **The following services are available**, Chirp shows the sites you can embed, sorted into groups — have a look to check yours is there. The link needs to start with **https://**. The preview on the right fills in as soon as the link works; if it isn't supported or isn't quite right, you'll see the message *"Enter a valid https:// embed URL"* instead of the page.
5. Tap **Next** to go to the **Appearance** tab.
6. Type a **Widget name** you'll recognize — like "Weather". You can add a **Description** too, but it's optional.
7. Tap **Save** in the settings, then **Save** in the dashboard header. Your weather map is now live on the dashboard, right beside your sensors.

> **Nothing showing in the preview?** Usually the link isn't quite right. Double-check you copied only the `https://` address from inside `src="…"` (not the whole `<iframe …>` chunk), that it starts with `https://`, and that the service is in the supported list under the box. A regular link, an `http://` one, or a site that isn't on the list won't load.

## What you can embed

The services you can use are sorted into groups in the picker, so it's easy to find what you're after. A few from each:

- **Dashboards & BI** — Power BI, Looker Studio, Tableau, Grafana. Handy if you already keep a chart of your energy use or solar output somewhere.
- **Maps & location** — Google Maps, OpenStreetMap, Mapbox. Show your neighborhood, a trip route, or a spot you're keeping an eye on.
- **Weather & air quality** — Windy, Meteoblue, Ventusky, IQAir. See the forecast, the wind, or today's pollen and air quality at a glance.
- **Video & camera feeds** — YouTube, Vimeo, Twitch. Embed a published stream or a favorite live view.
- **Transport & flights** — Waze, Flightradar24, FlightAware. Pin a Waze traffic map for the morning commute, or watch a flight come in so you know when to leave for the airport.
- **Shipping & parcel tracking** — 17TRACK, AfterShip, TrackingMore. Follow that parcel you're waiting on.
- **Finance & markets** — TradingView, Investing.com, Trading Economics. Keep an eye on a price or a market you follow.
- **Status & docs** — Statuspage, Instatus, Google Docs. Check whether a service you rely on is up, or pin a shared note.
- **Calendars & forms** — Google Calendar, Google Forms, Microsoft Forms, Calendly. Put the family calendar front and center.

The list you see in the widget is always up to date. If the service you want isn't there, tap the **please submit a request to add the desired resource** link under the Data source box and ask us to add it — we'll take a look and see if it can join the list.

## iFrame Widget or Map Widget?

It's easy to mix these up, so here's the difference:

- The **iFrame Widget** shows an external *web page* — including a web map like a Waze traffic view or an embedded Google Map. It shows whatever that website shows; it doesn't know anything about your own sensors.
- The **[Map Widget](map-widget.md)** puts one of *your own* GPS devices on a map and follows where it is right now. If you want to see where a car tracker or a moving sensor is, that's the Map Widget — not the iFrame Widget.

## Home examples

**Morning weather, right where you look**
Add a Windy or Meteoblue map to your main dashboard and it sits next to the indoor temperature and humidity. One glance tells you both what it's like outside and whether you left a window open.

**Traffic before the school run**
Embed a Waze map of your usual route and check it with your morning coffee. See the jams before you set off and decide when to leave — right beside the sensors telling you the house is buttoned up for the day.

**The family calendar on the wall tablet**
If you keep a dashboard on a hallway tablet, embed your shared Google Calendar. Everyone sees the week's plans beside the home's sensors — school runs, bin day, and whether the garage door got left up.

## What the widget shows

<figure><img src="../../.gitbook/assets/iframe-widget-dashboard.jpg" alt="A home dashboard with a live weather map embedded in an iFrame Widget, next to a 3D home model and a tank-level gauge"><figcaption></figcaption></figure>

On your dashboard, the iFrame Widget shows the web page live inside its tile, right beside your other panels — above, a weather map sits next to a 3D home model and a tank-level gauge. The page updates on its own, just like it would in a browser, so there's no separate refresh setting on the widget. In edit mode you can drag the tile around and resize it, so a busy page like a map gets the space it needs.

The iFrame Widget is just for viewing — it doesn't read your sensors, run automations, or send alerts. Use it to keep the web pages you care about close by, and let your sensor widgets (Last Data, Chart, Image, and the Digital Building Twin) handle your device readings.

## See also

- [Adding Widgets](README.md) — Edit mode and the widget picker
- [Map Widget](map-widget.md) — Follow where your own GPS device is (not the same as embedding a web map)
- [Digital Building Twin](digital-building-twin/README.md) — A live 3D model of your home
