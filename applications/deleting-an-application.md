---
description: "Remove a Chirp application you no longer need, and save the sensors, dashboards, and alerts you want to keep before you confirm."
---

# What happens when I delete an application?

Retiring an application takes a few clicks. First, take a minute to see what is inside it, because most of it goes away with it.

{% hint style="warning" %}
Deleting an application also deletes its devices together with their stored readings, its dashboards, and its alerts. Its automations stop and land in the Trash, the holding place for deleted automations before they are gone for good. Anything you want to keep must move to another application or to **Default** first.
{% endhint %}

Did the application come from a solution? Then it is a regular application like any other. Deleting it affects your copy only. The solution in the catalog stays, and so do other people's copies.

<figure><img src="../.gitbook/assets/chirp-applications-delete-confirmation.jpg" alt="The delete confirmation dialog in Chirp Applications, with a warning about what will be removed"><figcaption><p>Read the warning in the confirmation dialog before you delete.</p></figcaption></figure>

## How do I save the things I still need?

1. Open the application and select **Content**.
2. Go through all four cards: devices, dashboards, rules, and alarms.
3. Open each item worth keeping and switch its **Application** field to another application or to **Default**.
4. Save, then check that the item no longer shows up in the old application.

Picture it: you are done with `Home Watch`, but you like its temperature dashboard. Move that dashboard first. Move the sensors it shows as well.

## How do I delete the application?

1. Open the application and select the trash can icon at the top right.
2. Read the question **Are you sure you want to delete the application?** The dialog warns that the devices, rules, alarms, and dashboard linked to the application will be removed from the platform. Devices leave with their stored readings.
3. Select **Yes, delete** if you have checked what is left, or **Cancel** to stop.

Once it works, a message says **Application deleted successfully** and the application is gone from **My applications**. If something goes wrong, you see **Failed to delete application**.

## What if deleting shows an error?

Open the application again and look at what remains before you retry. Part of the cleanup may already have happened. An automation that someone has open in the editor can also get in the way. Close the editor, then try again.

The Trash gives back automations only. Sensors, dashboards, and alerts that were deleted stay deleted. To bring an automation back, follow [Trash and Restore](../rules-engine/managing-automations/trash-and-restore.md).

## Why can't I delete an application?

Deleting asks for two kinds of access. **Read** means you can see an item. **Write** means you can change it. You need both for the things inside. Your role in the home decides this, and the person who owns the account has it. Otherwise, ask them. If a message names a missing permission, nothing was deleted.

## What happens to dashboard folders?

Say every dashboard you delete sat in one folder, and nothing else lives there. Chirp then removes that empty folder too. A folder that still holds other dashboards stays where it is.
