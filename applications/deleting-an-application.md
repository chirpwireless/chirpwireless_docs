---
description: "Keep the household resources you still need before removing a Chirp application."
---

# Deleting an Application

You might stop using an application after changing a household setup. Before deleting it, decide which sensors, dashboards, automations, and alerts you still want to keep.

{% hint style="warning" %}
Deleting an application also removes its associated devices, dashboards, and alarm definitions. Associated rules are stopped and moved to Trash. To keep a resource, assign it to another application or **Default** first.
{% endhint %}

An application you installed from a solution is a normal application. Deleting it removes only your copy, never the provider's solution.

<figure><img src="../.gitbook/assets/chirp-applications-delete-confirmation.jpg" alt="Chirp Applications: Review the consequences before confirming application deletion."><figcaption><p>Review the consequences before confirming application deletion.</p></figcaption></figure>

## Keep the useful parts

Open the application and choose **Content**. Review all four sections. For each item you want to keep, open its settings and change the **Application** field. Save your change where needed, then check that the item has left the old application's content list.

For example, if you no longer want Home Watch but still use its temperature dashboard, move both the dashboard and any devices it depends on before deleting the application.

## Remove the application

Open the application and select the trash can icon at the top right. A dialog asks **Are you sure you want to delete the application?** and warns that the devices, rules, alarms, and dashboard linked to the application will be removed from the platform. Choose **Cancel** to back out, or **Yes, delete** once you have checked the remaining contents. A toast reads **Application deleted successfully**, and the application disappears from **My applications**. If it fails you see **Failed to delete application**.

If Chirp reports an error, reopen the application and inspect what remains before trying again. Some resources may already have been removed. If a rule is being edited, finish and close that editing session before retrying.

Restoring a rule from Trash does not recreate deleted sensors, dashboards, or alarm definitions. The rule recovery workflow is explained in [Trash and Restore](../rules-engine/managing-automations/trash-and-restore.md).


## If access is missing

Removing an application needs **Read** access to all four kinds of content and **Write** access to each kind that it contains. A message about missing permission means nothing has been removed by that attempt. An organization administrator can help you obtain the required access.

There is one dashboard-folder consequence to check as well: if the deleted dashboards all came from the same folder and nothing is left in it, Chirp removes that empty folder. Folders containing other items are kept. When the dashboards came from different folders, those folders remain.
