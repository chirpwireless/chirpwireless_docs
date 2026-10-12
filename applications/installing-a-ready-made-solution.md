---
description: "Press Use this solution, then Install solution to get practice sensors, running automations, alerts, and a dashboard in your account. Fixes included."
---

# How do I install a ready-made solution?

One install turns a solution into an application of your own, already working. You set nothing up first. If you like how it behaves, you buy the devices the install screen lists and swap them in for the practice sensors. Everything else is already in place.

The whole path: **Preview**, then **Use this solution**, then **Install solution**.

## How do I open the install screen?

1. In the left sidebar, choose **Applications**, then stay on the **Solutions** tab.
2. Press **Preview** on the solution you want.
3. Press **Use this solution** in the top-right corner.

The page is now titled **Install** plus the solution's name, with the description underneath. A back arrow returns you to the preview. Nothing exists yet. That only changes when you press **Install solution**.

<figure><img src="../.gitbook/assets/chirp-solutions-install.jpg" alt="The Install screen with the What will be created card, the Devices card, the Data source Emulator connector card with the Backfill 24h switch, and the Cancel and Install solution buttons"><figcaption><p>The install page before you press Install solution.</p></figcaption></figure>

## What does each part of the install screen mean?

* **What will be created.** A card with four tiles. They count the virtual devices (your practice sensors), the rules (automations), the alarm rules, and the widgets (tiles on your dashboard).
* **Alarm rules.** These are your alerts, with escalation. If nobody reacts, an alert can repeat or reach another contact you add later.
* **Devices.** A card on the right side. It opens with "To run this application on real data later, you'll need:" and then lists names. Each one is a real sensor you can buy and connect when you are ready.
* **Data source: Emulator connector.** This says the practice sensors send realistic readings, so the dashboard is alive straight away, and that any sensor can be swapped for a real one. A connector is the link that carries a sensor's readings into Chirp.
* **Backfill 24h of history, so charts aren't empty on first open.** A switch, marked **On** or **Off**. It starts **On**.
* **Cancel and Install solution.** Both sit at the bottom, with a note saying that installing creates an application based on this solution.

### Should I leave the Backfill switch on?

Most of the time, yes. Practice sensors start reporting right away, but charts need some past to draw. With the switch **On**, Chirp adds a day of earlier sample readings, so your first look at the dashboard shows full charts. Choose **Off** if you would like the charts to start empty and grow from now.

## What happens when I press Install solution?

The button changes to **Installing…** and the work continues in the background. Chirp builds these in your organization, which is your Chirp account space (at home, that means just you), in this order:

1. An application named after the solution.
2. The practice sensors, on the Emulator connector.
3. The alerts.
4. The automations, switched on and running.
5. The dashboards, in a folder with the application's name. Every widget reads from a practice sensor.

Press **Cancel** instead if you change your mind, and nothing is created.

You can close the page while it works. The install carries on, and the page picks it up again when you return in the same browser. Past about a minute and a half, you may see **Still installing, this can take a while — you can leave this page and check later.**

## What do I see when the install finishes?

A message appears saying the solution is installed. It tells you the virtual devices, rules, alarms, and dashboard are ready.

<figure><img src="../.gitbook/assets/chirp-solutions-installed.jpg" alt="The success dialog reading that the solution is installed, with a Go to application button"><figcaption><p>The message you see when the install finishes.</p></figcaption></figure>

Press **Go to application** to open it. From then on it is an ordinary application. You can edit anything in it, and it stays under **Applications → My applications**.

## Who receives the alerts?

You do. No matter who the solution was prepared for, the alerts in your copy go to the person who installed it. Open [Alarm](../alarm/README.md) to add household members or other ways to be notified before you count on them.

## What if the install does not complete?

* **Not enough room on your plan.** Your plan caps how many devices, dashboards, and rules you can have, and practice sensors count as devices. If the install would pass a cap, Chirp says what does not fit and creates nothing. Free up room or change plans, then try again. Your limits are in [Subscription](../account/subscription.md).
* **Missing permissions.** You need permission to create each kind of item in the solution. The message names the one that is missing. Ask the person who owns the account.
* **An install is already running.** The message reads "Another installation of this solution is already running in your organisation, or a failed one needs an operator to clean it up before you can retry." (spelled as the product shows it). In plain words, an install is still going, or a failed one needs someone from Chirp support to clear it. Choose **Go to my applications** to check.
* **Installation failed: ...** A red banner with the reason spelled out. It shows when Chirp refuses the request, for example over a limit or a missing permission.
* **Installation cancelled: ...** A red banner with a **Retry** button. Chirp started, hit a problem, and removed everything it had made. **Retry** starts over.
* **The catalog is being updated — please retry in a minute.** This one has a **Retry** button too.
* **Still installing, this can take a while — you can leave this page and check later.** and **The installation status is temporarily unavailable.** Yellow notices, each with a **Retry** button that checks progress again. Neither means the install failed.

If something breaks halfway, Chirp removes whatever it had already made, so nothing half-finished stays behind. In the rare case it cannot, the message says **Installation failed and needs manual cleanup — contact support.**

## What do I do next?

Open the dashboard and watch the practice sensors report. Skim the automations and alerts to see what the setup does. When your real sensors arrive, continue with [From Practice Sensors to Real Ones](from-practice-sensors-to-real-ones.md).

Changed your mind? [Delete the application](deleting-an-application.md). Only your copy goes away, and the solution in the catalog stays as it is.
