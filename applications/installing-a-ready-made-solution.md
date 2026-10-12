---
description: "Press Use this solution, then Install solution to get practice sensors, working automations, alerts, and a dashboard. Plus fixes if the install stops."
---

# How do I install a ready-made solution?

This page walks you through the install screen and what happens after you press the button. You do not need to set anything up first.

The whole path is: press **Preview**, then **Use this solution**, then **Install solution** on the next screen.

## How do I start the install?

1. Press **Preview** on a solution card.
2. Press **Use this solution**, the button at the top right of the preview.

The install page opens with **Install** and the solution's name as its title. Use the back arrow beside the title to return to the preview. Nothing is created until you press **Install solution** at the bottom.

## What is on the install screen?

* **What will be created** is a card with four tiles. They count the virtual devices (the practice sensors, running on the Emulator connector), the rules (automations), the alarm rules, and the widgets (the tiles on your dashboard). Think of it as a checklist.
* **Alarm rules** are your alerts, with escalation. If nobody reacts, the alert can repeat or go to another contact you add later.
* **Devices** is a card on the right side of the page. It begins "To run this application on real data later, you'll need:" followed by a list of names. Each name is underlined and stands for a real sensor you can buy and connect later.
* **Data source: Emulator connector** says the practice sensors send realistic readings, the dashboard is live right away, and you can swap any sensor for a real one later. A connector is the link that brings a sensor's readings into Chirp.
* **Backfill 24h of history, so charts aren't empty on first open** is a switch labeled **On** or **Off**. It starts **On**, which fills the charts with a day of earlier sample readings. Switch it **Off** if you want empty charts.
* **Cancel** and **Install solution** sit at the bottom. A note underneath says that installing creates an application based on this solution.

<figure><img src="../.gitbook/assets/chirp-solutions-install.jpg" alt="The Install screen with the What will be created card, the Devices card, the Data source Emulator connector card with the Backfill 24h switch, and the Cancel and Install solution buttons"><figcaption><p>The install page before you press Install solution.</p></figcaption></figure>

## What happens when I press Install solution?

The button changes to **Installing…** and the work runs in the background. Chirp creates these, in this order, in your organization (your Chirp account space; for a single household, that is your home):

1. An application named after the solution.
2. The practice sensors, on the Emulator connector.
3. The alerts.
4. The automations, switched on and running.
5. The dashboards, placed in a folder that carries the application's name. Every widget reads from a practice sensor.

You can leave the page. The install keeps going, and the page picks up where it left off when you come back in the same browser. After about a minute and a half you may see **Still installing, this can take a while — you can leave this page and check later.**

When it finishes, a message tells you the solution is installed ("Virtual devices, rules, alarms and the dashboard are ready"). Press **Go to application** to open it.

<figure><img src="../.gitbook/assets/chirp-solutions-installed.jpg" alt="The success dialog reading that the solution is installed, with a Go to application button"><figcaption><p>The message you see when the install finishes.</p></figcaption></figure>

## Who receives the alerts?

The alerts in your copy always go to you, the person who installed it. You can add household members or other ways to be notified later in [Alarm](../alarm/README.md).

## What if the install does not complete?

Find your message in this list.

* **Not enough room on your plan.** Your plan limits how many devices, dashboards, and rules you can have, and practice sensors count as devices. If the install would go over a limit, Chirp tells you what does not fit and creates nothing. Free up room or change plans, then try again. Your limits are in [Subscription](../account/subscription.md).
* **Missing permissions.** You need permission to create each kind of item. The message names the one that is missing. Ask the person who owns the account.
* **An install is already running.** The message reads "Another installation of this solution is already running in your organisation, or a failed one needs an operator to clean it up before you can retry." (spelled as the product shows it). In plain words: an install is still running, or a failed one needs someone from Chirp support to clean it up. Choose **Go to my applications** to check.
* **Installation failed: ...** with the reason spelled out appears as a red banner when Chirp refuses the request, for example because of a limit or a missing permission.
* **Installation cancelled: ...** is a red banner with a **Retry** button. Chirp started, hit a problem, and removed everything it had made. **Retry** starts again.
* **The catalog is being updated — please retry in a minute.** has a **Retry** button too.
* **Still installing, this can take a while — you can leave this page and check later.** and **The installation status is temporarily unavailable.** are yellow notices with a **Retry** button that checks the progress again. Neither means the install failed.

If something goes wrong halfway, Chirp removes whatever it had already built, so nothing half-finished is left. In the rare case it cannot, the message says **Installation failed and needs manual cleanup — contact support.**

## What do I do next?

Changed your mind? [Delete the application](deleting-an-application.md). Only your copy goes away. Otherwise, continue with [From Practice Sensors to Real Ones](from-practice-sensors-to-real-ones.md).
