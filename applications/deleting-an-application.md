---
description: "Keep the household resources you still need before removing a Chirp application."
---

# How do I delete an application in Chirp?

You might stop using an application after changing your setup. Before you delete it, decide which sensors, dashboards, automations, and alerts you still want to keep.

{% hint style="warning" %}
Deleting an application also deletes its devices and their stored readings, its dashboards, and its alerts. Its automations are stopped and moved to the Trash (the place where deleted automations wait before they are removed for good). To keep something, move it to another application or to **Default** first.
{% endhint %}

An application you installed from a solution is a normal application. Deleting it removes only your copy, never the catalog's solution.

<figure><img src="../.gitbook/assets/chirp-applications-delete-confirmation.jpg" alt="Chirp Applications: Review the consequences before confirming application deletion."><figcaption><p>Review the consequences before confirming application deletion.</p></figcaption></figure>

## How do I keep the devices and dashboards I still need?

Open the application and choose **Content**. Look at all four cards. For each item you want to keep, open it and change its **Application** field. Save, then check that the item has left the old application's list.

For example, say you no longer want `Home Watch` but still use its temperature dashboard. Move the dashboard and the devices it shows before you delete the application.

## How do I remove the application itself?

Open the application and select the trash can icon at the top right. A dialog asks **Are you sure you want to delete the application?** and warns that the devices, rules, alarms, and dashboard linked to the application will be removed from the platform. Remember: the devices go with their stored readings. Choose **Cancel** to back out, or **Yes, delete** once you have checked the remaining contents. A toast reads **Application deleted successfully**, and the application disappears from **My applications**. If it fails you see **Failed to delete application**.

If Chirp shows an error, reopen the application and check what is left before you try again. Some items may already be gone. If someone has an automation open in the editor, close it first, then retry.

Bringing an automation back from the Trash does not bring back deleted sensors, dashboards, or alerts. The rule recovery workflow is explained in [Trash and Restore](../rules-engine/managing-automations/trash-and-restore.md).


## Why can't I delete an application?

To delete an application you need **Read** and **Write** access. In plain words, that depends on your role in the home. The person who owns the account can do it. Otherwise, ask them. If you see a message about a missing permission, nothing was deleted.

One more thing about dashboard folders: if all the deleted dashboards came from one folder and nothing else is in it, Chirp removes that empty folder. Folders that still hold other dashboards stay.
