---
description: "See the dashboards that belong to your application and change them on the dashboard page. Plus what the empty messages mean."
---

# How do I use an application's dashboards?

An application's **Dashboard** tab is a quick way to look at the dashboards that belong to it. For example, an application called `Home Watch` might have one dashboard for the whole home and another for the garden's sensors.

An installed [solution](installing-a-ready-made-solution.md) came with its own dashboard, already showing its sensors. Any dashboard you build yourself can be added to the application too. You do that with the **Application** field when you add or edit the dashboard.

## How do I check my home from an application?

1. Select **Applications**, then open the application from **My applications**.
2. Choose **Dashboard**.
3. Select the dashboard you want. Each dashboard in the application has its own button above the preview, named after the dashboard.
4. Read the widgets or use the controls available to your account.

Use **Content** when you want to find the sensors or automations behind the view.

## How do I change what a dashboard shows?

Select **Go to the dashboard** to open the dashboard itself. Change the layout or widgets there and save. When you return to the application, you see the updated dashboard, because there is only one copy.

For detailed instructions, see [Building a Dashboard](../dashboards/building-a-dashboard.md).

## What do the empty messages mean?

* **This application has no dashboards yet** means no dashboard is assigned to the application.
* **This dashboard has no widgets yet** means the dashboard exists but nothing has been added to it.
* **Dashboard is unavailable** means Chirp could not load that dashboard; reload the page, then check your access.

## Why is the Dashboard tab empty?

Open **Content** and look under **Dashboards**. If it is empty, edit the dashboard you want and choose this application in its **Application** field.

<figure><img src="../.gitbook/assets/chirp-add-dashboard-dialog.jpg" alt="The Add dashboard dialog with Icon, Name, Folder, Application and Description fields, where the Application field names the current application"><figcaption><p>Pick the application in the Add dashboard dialog.</p></figcaption></figure>

You can also make a new dashboard and pick the application in the **Add dashboard** dialog. If a dashboard exists but you cannot see it, ask the person who owns the account to check your access.

## Why does the application page say Application not found?

The page shows **Application not found** alone in the middle of the screen, with no tabs and no buttons, when Chirp cannot load that application. Likely causes: the application was deleted, the link points to an application in another organization, or the page could not be read. Choose **Applications** in the sidebar and open **My applications** to see what you can open. Also check which organization is selected in the sidebar, because an application belongs to one organization (your Chirp account space).
