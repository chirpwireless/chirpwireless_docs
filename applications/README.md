---
description: "Bring a complete home setup together in Chirp Applications, and see how planned templates will let providers prepare solutions for your household."
---

# Applications

An **application** is a complete setup for a household need, with its devices, dashboards, rules, and alarms brought together in Chirp. A **Home Leak Monitoring** application, for example, could include water sensors under the sinks, a dashboard showing their readings, and a rule that sends an alert when a sensor detects a leak.

The idea is for a specialist to prepare that setup so a household can start using a solution without having to design every part of it. A home-equipment provider knows which sensors are suitable, what a useful dashboard should show, and how the notifications should work. Applications gives those pieces a place together.

**The planned next step is to offer those prepared setups as templates.** You would choose a solution for your home, apply its template, and have its digital devices, dashboards, rules, and alarms created together. In release 3.10.0, you can create an application and assemble its contents yourself. Provider templates and the ability to apply them are planned capabilities.

<figure><img src="../.gitbook/assets/chirp-applications-dashboard.jpg" alt="Chirp application showing its assigned home dashboard"><figcaption><p>Open an application's Dashboard tab to see the views associated with that household setup.</p></figcaption></figure>

## What is inside a home application?

A sensor is one part of a working home setup. The other parts make its readings useful:

| Part | Example in Home Leak Monitoring |
|---|---|
| Devices | The digital devices receiving readings from your water sensors. |
| Dashboards | A view of the sensors and whether they report a leak. |
| Rules | The conditions that recognize a leak and start the response you configure. |
| Alarms | The message and notification settings used to tell you about it. |

The application keeps those parts associated with the same household task. Another application might bring together the door sensors, views, and notifications you use while away from a holiday home.

You can also name an application **Home Watch** and build it up around the readings and automations you want to check together. Its **Dashboard** tab is the place to use its views. **Content** shows the devices, dashboards, rules, and alarm definitions that make the setup work.

## How a prepared template would help

An **application** is your own household setup inside Chirp. A **template** is the planned reusable setup that a specialist would prepare for households with a similar need.

For example, an equipment provider could build and configure a leak-monitoring solution, then make it available as a template. Applying it would create a household's own digital device configurations, dashboards, rules, and alarms together. You would connect the setup to your equipment and adapt it to your home, starting from the provider's work rather than assembling every piece independently.

This is the direction for Applications. Template publishing and installation are planned; selecting a ready-made template is not part of the current creation process.

## Build and use an application today

The current release lets you assemble your own solution and keep its parts together. Creating an application starts an empty setup: it does not automatically add sensors, build dashboards, or configure notifications.

1. [Create an application](creating-an-application.md), such as Home Watch, and describe what you use it for.
2. Set up the devices, dashboard, rules, and alarm definitions you need.
3. [Assign the resources](organizing-content.md) through their **Application** fields. Configure the rule to use the intended device and alarm definition; assigning them to the same application does not create that behavior automatically.
4. Choose **Applications → My applications**, open the application, and use **Dashboard** to view its dashboards or **Content** to find its resources.

You can start with one device and a useful view, then add automations and notifications as you configure them. See [Using Application Dashboards](using-application-dashboards.md) when you want to open or change the associated views.

Your application belongs to the selected organization. Family members need the relevant permissions to see or change its devices, dashboards, rules, and alarms; the application does not grant extra access.

If you later retire the setup, [check what deletion removes](deleting-an-application.md). Deleting an application also removes associated resources, so move the pieces you still use to another application or **Default** first.
