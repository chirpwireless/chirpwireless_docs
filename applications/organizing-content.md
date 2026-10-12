---
description: "Put household devices, views, rules, and alarm definitions into the right Chirp application."
---

# How do I organize an application's content?

Your application's **Content** tab brings its working parts together. For Home Watch, that could mean a door sensor, a home dashboard, a rule that checks the door reading, and an alarm definition for the notification.

An application installed from a [solution](solutions-explained.md) already lists everything it created here, and you can add to it. Use each resource's **Application** field to choose where it belongs. The resource must already exist or be created through its usual setup screen.

## How do I add devices, dashboards, rules and alarms to an application?

1. Open a device's details. On **Device Info**, choose `Home Watch` in **Application** and select **Next** to apply the change.
2. Create or edit the dashboard you want to use, choose `Home Watch` in its **Application** field, and select **Next** to apply the change.
3. In the rules list, set the rule's **Application** selector to `Home Watch`.
4. Create or edit the alarm definition, choose the same application, and save it.
5. Return to **Applications → My applications → Home Watch → Content**.

Each item appears under its own heading: **Devices**, **Dashboards**, **Rules**, or **Alarms**. You need editing access to a resource to change its assignment.

## Does grouping items in an application create an automation?

The pieces still need to be connected through their settings. For a door alert, the rule needs to check the correct sensor and use the intended alarm definition. Simply placing both items in Home Watch does not cause notifications. Follow [Set Up a Home Alert](../alarm/set-up-a-home-alert.md) to configure that behavior.

## How do I move an item to another application?

A resource can be assigned to one application. Change its **Application** field to move it. Choose **Default** when you want to keep the resource without assigning it to a named application.

Content counts show how many resources are associated with a category you can access. **0** means none have been added. A dash means the number could not be obtained, which can happen when access is missing or the content cannot be loaded. It is not the same as an empty category.

If you are tidying up an old application, move the useful parts first. [Deleting an application](deleting-an-application.md) also removes associated resources.

## What does each card on the Content tab show?

Open **Applications → My applications**, select the application, and choose **Content**. The page has two columns of cards.

* **Devices** lists every device in the application. Each row has a badge: **Emulator** for a practice sensor, or **live** / **offline** plus its technology, such as **live · LoRaWAN**, for a real one. A real device that has stopped reporting is drawn in muted text. Select a row to open the device.
* **Dashboards** lists the dashboards. Select a row to open the dashboard.
* **Rules** opens with a short explanation of what a rule chain does, then lists the rules with their descriptions. Select a row to open the rule.
* **Alarms** explains that an alarm here is a notification recipe, not a trigger: it defines the message, the recipients and channels, how it escalates, and the schedule, and a rule decides when it fires. Each row shows the alarm's message and, on the right, its severity. A gray **Disabled** label appears beside the severity when the definition is switched off, because a disabled alarm stays silent whatever a rule raises.
* **Emulator** appears at the bottom of the left column only while the application still has a practice sensor. Select **Go to connectors** to add the real connector.

Every card shows its count next to the title. An empty card says **Nothing here yet**. A card that cannot be read says **Couldn't load this list — it may require a permission you don't have**, which is a missing permission, not an empty list. Opening a row takes you to that item, and the back navigation returns you to the same tab.

## How do I find an item in a larger application?
Once a card holds more than ten rows, a small search box appears in its header. It looks through the row's name and its second line of text, such as a description. If nothing matches you see **No matches for this search**. The Rules and Alarms cards show up to 200 entries each, and disabled alarm definitions are included. Use the full **Rules engine** and **Alarm** lists for larger collections.

## Which application will a new device or dashboard use?

New resource forms begin with **Default** until you create a resource using another application. Chirp then remembers your last successful choice separately for each organization. Check the selection before saving a device, view, or alert. If you use **Add new application** (type a name, press **Create**, and Chirp selects it for you) and then cancel the surrounding resource form, the application you just created still exists.

Devices marked **Emulator** use simulated readings. While an application has one, its **Content** tab includes the **Emulator** explanation and the **Go to connectors** shortcut. You can learn the setup before connecting the actual equipment; the [Emulator Connector](../connectors/emulator-connector.md) guide explains how simulated devices work and how to switch their input. A real device's status depends on its connection and recent readings, rather than simply being assigned to an application.

Changing a rule's Application selection is allowed even while its flow is open in an editor. Removing the application is different: an active editor lock can interrupt deletion.
