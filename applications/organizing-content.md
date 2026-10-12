---
description: "Choose the Application field for devices, dashboards, automations, and alerts so the Content tab lists them together. Learn what Default and the counts mean."
---

# How do I organize an application's content?

An application's **Content** tab shows everything that belongs to it in one spot. Picture an application called `Home Watch` (just an example name). It could gather a door sensor, a home dashboard, an automation that checks the door reading, and an alert that tells you when the door opens.

If you installed the application from a [solution](solutions-explained.md), its parts are already listed, and you can add more whenever you like. Each device, dashboard, automation, and alert has an **Application** field, and that field decides where it lives. The item has to exist first, so create it on its usual screen.

## How do I add things to an application?

| What | Where to choose the application |
|---|---|
| Device | Click **Devices** in the sidebar and open the device. On **Device Info**, pick the application in **Application**, then select **Next** to apply the change. |
| Dashboard | Open **Dashboards** in the sidebar, then create or edit the dashboard. Pick the application in its **Application** field and select **Next**. |
| Automation | Click **Rules engine** in the sidebar. In the list, set the **Application** selector on the automation. |
| Alert | Click **Alarm** in the sidebar and open the **Alarm definitions** tab. Create or edit the alert, pick the application, and save. |

Choose `Home Watch` in each field. Then go to **Applications → My applications → Home Watch → Content** and check that every item appears under the right heading. You need permission to edit an item to change its application.

An automation is a rule that reacts to a reading. Some screens call it a rule chain.

## What is included in an application?

The **Content** tab has one card each for **Devices**, **Dashboards**, **Rules**, and **Alarms**. Open any row to keep working on that item.

Does grouping create an automation? No. Putting the door sensor, the automation, and the alert into `Home Watch` does not send you a single notification. The automation still has to watch the right sensor and use the right alert. [Set Up a Home Alert](../alarm/set-up-a-home-alert.md) walks you through it.

## How do I move something to another application?

An item belongs to one application at a time. Change its **Application** field and it moves.

**Default** is the application with no name of its own. Choose it when you want to keep an item without placing it in a named application.

## How do I keep things when reorganizing?

Moving an item only changes where it is listed. Deleting an application is different, because it also deletes the devices in it and their stored readings. Before you tidy up an old application, move out whatever you still want. [Deleting an application](deleting-an-application.md) has the details.

## What does each card on the Content tab show?

Open **Applications → My applications**, select the application, and choose **Content**. Two columns of cards appear.

* **Devices** lists every device. Each row carries a badge: **Emulator** for a practice sensor, or **live** / **offline** plus its technology, such as **live · LoRaWAN**, for a real one. A real device that stopped reporting appears in muted text.
* **Dashboards** lists your dashboards.
* **Rules** starts with a short note about what a rule chain (an automation) does, then lists the rules with their descriptions.
* **Alarms** explains that an alarm here is a notification recipe, not a trigger. It holds the message, who gets it and how, how it escalates (if nobody reacts, it can repeat or go to someone else), and the schedule. An automation decides when it fires. Each row shows the message and, on the right, the severity. A gray **Disabled** label means the definition is off, and a disabled alarm stays silent whatever a rule raises.
* **Emulator** sits at the bottom of the left column while the application still has a practice sensor. Select **Go to connectors** to add the real connector.

Select any row to open the item. The back navigation brings you to the same tab again.

## What do the counts mean?

The number beside each card title, and in the **My applications** table, tells you how many items of that kind the application holds. **0** means you have not added any yet.

A dash means Chirp could not read the number, for example because you lack access. It does not mean the category is empty.

An empty card says **Nothing here yet**. A card that cannot be read says **Couldn't load this list — it may require a permission you don't have**. That points to a missing permission, not an empty list.

## How do I find an item in a larger application?

When a card has more than ten rows, a small search box appears in its header. It looks through the name and the second line of text, such as a description. No hits? You see **No matches for this search**.

## Good to know

* New forms start with **Default**. After you save something with another application, Chirp remembers that choice for next time, separately for each organization. Check the selection before saving a device, dashboard, or alert.
* **Add new application** creates the application as soon as you press **Create**, and Chirp selects it for you. If you then cancel the form, the new application still exists.
* An **Emulator** badge marks a practice sensor that sends sample readings so you can learn the setup before your real sensors arrive. The [Emulator Connector](../connectors/emulator-connector.md) guide explains them.
* A real device's status depends on its connection and recent readings, not on which application it belongs to.
* The Rules and Alarms cards show up to 200 entries each. For more, use the full **Rules engine** and **Alarm** pages.
* You can change an automation's application while someone has it open in the editor. Deleting the application is different, and an open editor can stop it.
