---
description: "Replace a solution's practice sensors with your real Chirp devices by swapping the Emulator connector, keeping dashboards, automations, and alerts in place."
---

# From Practice Sensors to Real Ones

The practice sensors in a solution exist so you can watch the whole setup work first. When your real sensors arrive, you point the same setup at them. This page shows the installed application and the exact screens involved.

## What does my new application look like?

After the install, **Go to application** opens the application page. Its header shows **Applications / ** followed by the name, with a pencil (edit) and a trash can (delete) at the top right. A **Publish application** button also appears for accounts that are allowed to share setups; as a household member you can ignore it. Two tabs sit underneath:

* **Dashboard** shows the dashboards that came with the setup, with a **Go to the dashboard** link at the right. Each widget carries an **Emulator** badge while it reads from a practice sensor.
* **Content** lists **Devices**, **Dashboards**, **Rules**, and **Alarms**. At the bottom is an **Emulator** card that explains the swap and offers **Go to connectors**.


<figure><img src="../.gitbook/assets/chirp-installed-application-dashboard.jpg" alt="An installed application with the Dashboard tab selected, a Publish application button, a pencil and trash icon, and a live widget with an Emulator badge"><figcaption><p>An installed application on its Dashboard tab.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/chirp-application-content.jpg" alt="The Content tab of the installed application listing its device, dashboard and the Emulator card with the Go to connectors button"><figcaption><p>The Content tab, with the Emulator card at the bottom of the left column.</p></figcaption></figure>

## How do I swap a practice sensor for the real one?

```mermaid
flowchart LR
    A[Practice sensor on the Emulator] --> B[Open the device and its Connection tab]
    B --> C[Choose Swap connection]
    C --> D[Pick the real connector and enter its details]
    D --> E[Dashboard and automations read real data]
```

1. Make sure the [connector](../connectors/README.md) for your sensor exists. If not, choose **Go to connectors** on the Emulator card and add it first.
2. Open the application's **Content** tab, then select a device under **Devices**. The device editor opens with the tabs **Device info**, **Connection**, **Emulator**, **Mapping**, **Attributes**, **Calculated data**, and **Logs**.
3. Open **Connection**. At the top, under the heading **Choose a connector to add a device**, you will see **Connector type** showing **Emulator**, and a **Swap connection** link on the right.
4. Select **Swap connection**. The link turns into **Cancel swap** and **Connector type** becomes a drop-down. Choose the real connector, such as LoRaWAN, MQTT, or a tracker, then fill in the fields it shows.
5. Keep the **Device data key** rows as they are: each row is one reading, shown with its **Data type**, an **Emulator** button, and a trash can. They carry your mappings across, so the dashboard keeps working.
6. Select **Save**. The **Reception** strip at the bottom reports **Receiving & storing** with a **LIVE** marker once real readings arrive.

Read the solution's **Content** text before you begin. Providers usually write down the identifiers each device needs.


<figure><img src="../.gitbook/assets/chirp-device-connection-emulator.jpg" alt="The Connection tab of a practice sensor showing the Swap connection link, Connector type Emulator, the Device ID, the data sending interval, a Device data key row and the Reception strip"><figcaption><p>The Connection tab of a practice sensor, with Swap connection at the top.</p></figcaption></figure>

## What do the other device tabs do while it is still a practice sensor?

* **Emulator** lets you type a value for any reading and choose **Save**, or **Send once** to push a single reading through right away. Use it to test an automation without waiting.
* **Mapping** lists each reading's **Device data key**, current **Value**, **Last update**, **Normalized key**, **Unit**, **Type**, and **Data type**. For a practice sensor these rows follow the device configuration, so add or rename readings on the **Connection** tab instead.


<figure><img src="../.gitbook/assets/chirp-device-emulator-tab.jpg" alt="The Emulator tab with a Device data key field, a Value field and the Save and Send once buttons"><figcaption><p>The Emulator tab.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/chirp-device-mapping-tab.jpg" alt="The Mapping tab listing Device data key, Value, Last update, Normalized key, Unit, Type and Data type for one reading"><figcaption><p>The Mapping tab.</p></figcaption></figure>

## What stays the same, and what changes?

Readings keep their names and units, and the dashboard, automations, and alerts carry on. Only the source of the numbers changes, and the **Emulator** badge disappears from that device.

## Can I swap one sensor at a time?

Yes. Replace them in any order; the rest keep simulating until you get to them. For background reading, see [Pretend Sensors](../devices/pretend-sensors.md) and the [Emulator Connector](../connectors/emulator-connector.md).
