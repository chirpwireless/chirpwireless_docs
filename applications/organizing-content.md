---
description: "Put household devices, views, rules, and alarm definitions into the right Chirp application."
---

# How do I organize an application's content?

Your application's **Content** tab shows everything that belongs to it in one place. Say you made an application called `Home Watch`. It could hold a door sensor, a home dashboard, an automation that checks the door reading, and an alert that notifies you. (`Home Watch` is just an example name.)

An application installed from a [solution](solutions-explained.md) already lists everything it created here, and you can add to it. Each device, dashboard, automation, and alert has an **Application** field. That field decides which application it belongs to. The item has to exist first, so create it on its usual screen.

## How do I add devices, dashboards, rules and alarms to an application?

1. Click **Devices** in the sidebar and open a device. On **Device Info**, choose `Home Watch` in **Application** and select **Next** to apply the change.
2. Open **Dashboards** in the sidebar, then create or edit the dashboard you want. Choose `Home Watch` in its **Application** field and select **Next** to apply the change.
3. Click **Rules engine** in the sidebar. In the list, set the automation's **Application** selector to `Home Watch`. (An automation is a rule that reacts to a reading. In the screens you may see it called a rule chain.)
4. Click **Alarm** in the sidebar, open the **Alarm definitions** tab, then create or edit the alert. Choose the same application and save it.
5. Return to **Applications → My applications → Home Watch → Content**.

Each item appears under its own heading: **Devices**, **Dashboards**, **Rules**, or **Alarms**. You need permission to edit an item to change which application it belongs to.

## Does grouping items in an application create an automation?

No. The pieces still need to be connected in their own settings. For a door alert, the automation has to watch the right sensor and use the right alert. Putting both in `Home Watch` does not send any notifications. Follow [Set Up a Home Alert](../alarm/set-up-a-home-alert.md) to configure that behavior.

## How do I move an item to another application?

An item can belong to one application at a time. Change its **Application** field to move it. **Default** is the application with no name of its own. Pick it when you want to keep an item without putting it in a named application.

The counts next to each card title and in the **My applications** table show how many items of that kind the application holds. **0** means none have been added. A dash means Chirp could not read the number, for example because you lack access. It does not mean the category is empty.

If you are tidying up an old application, move the parts you still need first. [Deleting an application](deleting-an-application.md) also deletes the devices and their stored readings that belong to it.

## What does each card on the Content tab show?

Open **Applications → My applications**, select the application, and choose **Content**. The page has two columns of cards.

* **Devices** lists every device in the application. Each row has a badge: **Emulator** for a practice sensor, or **live** / **offline** plus its technology, such as **live · LoRaWAN**, for a real one. A real device that has stopped reporting is drawn in muted text. Select a row to open the device.
* **Dashboards** lists the dashboards. Select a row to open the dashboard.
* **Rules** opens with a short note about what a rule chain (an automation) does, then lists the rules with their descriptions. Select a row to open the rule.
* **Alarms** explains that an alarm here is a notification recipe, not a trigger. It sets the message, who gets it and how, how it escalates (if nobody reacts, it can repeat or go to someone else), and the schedule. An automation decides when it fires. Each row shows the alarm's message and, on the right, its severity. A gray **Disabled** label appears beside the severity when the definition is switched off, because a disabled alarm stays silent whatever a rule raises.
* **Emulator** appears at the bottom of the left column only while the application still has a practice sensor. Select **Go to connectors** to add the real connector.

Every card shows its count next to the title. An empty card says **Nothing here yet**. A card that cannot be read says **Couldn't load this list — it may require a permission you don't have**, which is a missing permission, not an empty list. Opening a row takes you to that item, and the back navigation returns you to the same tab.

## How do I find an item in a larger application?

Once a card holds more than ten rows, a small search box appears in its header. It looks through the name and the second line of text, such as a description. If nothing matches you see **No matches for this search**.

Good to know: the Rules and Alarms cards show up to 200 entries each. For more, use the full **Rules engine** and **Alarm** pages.

## Which application will a new device or dashboard use?

New forms start with **Default**. Once you save something with another application, Chirp remembers that choice for next time, separately for each organization. Check the selection before you save a device, dashboard, or alert. If you use **Add new application** (type a name, press **Create**, and Chirp selects it for you) and then cancel the form, the new application still exists.

Devices marked **Emulator** are practice sensors. They send sample readings so you can learn the setup before your real sensors arrive. While an application has one, its **Content** tab shows the **Emulator** card with the **Go to connectors** shortcut. The [Emulator Connector](../connectors/emulator-connector.md) guide explains how practice sensors work. A real device's status depends on its connection and recent readings, not on which application it belongs to.

Good to know: you can change an automation's application while someone has it open in the editor. Deleting the application is different, and an open editor can stop it.
