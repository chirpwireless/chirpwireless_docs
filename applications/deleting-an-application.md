---
description: "Before you delete a Chirp application, keep the devices, dashboards, and alerts you still need. Then remove it and fix any permission errors."
---

# How do I delete an application in Chirp?

This page helps you remove an application you no longer use, without losing the parts you still want. Deleting takes a few clicks, so look at what is inside first.

{% hint style="warning" %}
Deleting an application also deletes its devices and their stored readings, its dashboards, and its alerts. Its automations are stopped and moved to the Trash (the place where deleted automations wait before they are removed for good). To keep something, move it to another application or to **Default** first.
{% endhint %}

Did you install the application from a solution? It is a normal application. Deleting it removes only your copy, never the catalog's solution.

<figure><img src="../.gitbook/assets/chirp-applications-delete-confirmation.jpg" alt="The delete confirmation dialog in Chirp Applications, with a warning about what will be removed"><figcaption><p>Read the warning in the confirmation dialog before you delete.</p></figcaption></figure>

## How do I keep the devices and dashboards I still need?

1. Open the application and choose **Content**.
2. Look at all four cards.
3. For each item you want to keep, open it and change its **Application** field.
4. Save, then check that the item has left the old application's list.

Say you no longer want `Home Watch` but still use its temperature dashboard. Move the dashboard and the devices it shows before you delete the application.

## How do I remove the application itself?

1. Open the application and select the trash can icon at the top right.
2. A dialog asks **Are you sure you want to delete the application?** It warns that the devices, rules, alarms, and dashboard linked to the application will be removed from the platform. The devices go with their stored readings.
3. Choose **Cancel** to back out, or **Yes, delete** once you have checked the remaining contents.

A toast reads **Application deleted successfully**, and the application disappears from **My applications**. If it fails, you see **Failed to delete application**.

## What if deleting shows an error?

Reopen the application and check what is left before you try again. Some items may already be gone. If someone has an automation open in the editor, close it first, then retry.

Bringing an automation back from the Trash does not bring back deleted sensors, dashboards, or alerts. [Trash and Restore](../rules-engine/managing-automations/trash-and-restore.md) explains how to recover a rule.

## Why can't I delete an application?

To delete an application you need **Read** and **Write** access. That depends on your role in the home, and the person who owns the account can do it. Otherwise, ask them. If you see a message about a missing permission, nothing was deleted.

## What happens to dashboard folders?

If all the deleted dashboards came from one folder and nothing else is in it, Chirp removes that empty folder. Folders that still hold other dashboards stay.
