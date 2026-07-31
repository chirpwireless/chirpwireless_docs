---
description: Register a LoRaWAN, tracker, MQTT or pretend sensor in Chirp and map its readings, step by step.
---

# Adding Sensors

Every sensor you add to Chirp gets its own profile — a record that remembers the sensor's name, connection details, measurement settings, and full data history. Even when a sensor goes to sleep between transmissions, its profile keeps everything organized and ready for dashboards and automation. Because the physical sensor binding is optional, you can create and configure a sensor profile before the actual hardware is connected — so you can plan your setup first and plug in the sensors when you're ready.

## Before you start

You'll need:
- **A connection** set up — an LNS connection for LoRaWAN sensors, a Tracker connection for vehicle trackers, an MQTT connector (Cloud or External) for Zigbee2MQTT and other MQTT-publishing hardware, or an Emulator connection if your sensor hasn't arrived yet. See [Setting Up a Connection](../connectors/setting-up-a-connection.md) and the [MQTT Connector](../connectors/mqtt-connector.md) docs.
- **Your sensor's identifiers** — for LoRaWAN sensors: the **Device EUI** and **AppKey**, usually printed on the sensor or its packaging. For trackers: the **Unique ID** from the manufacturer. For MQTT sensors: the **device-level topic identifier** that the device publishes under — for Zigbee2MQTT this is the friendly name. The Device ID field in Chirp must match it byte-for-byte (no whitespace). A [pretend sensor](pretend-sensors.md) needs none of this — you choose its Device ID yourself, within the naming rules on that page.
- **For MQTT sensors only — the device must be publishing before you can finish mapping.** The Connector key dropdown in the Mapping tab is populated from payload keys actually received from the device. See the [MQTT-specific note](#a-note-for-mqtt-sensors) further down for the two-pass save flow.

## Where to add a sensor

There are several ways to start — they all open the same registration dialog:

- **Devices in the sidebar** — Click **Devices**, then click **Add device** in the top-right corner.
- **From a connection** — Open your LNS or Tracker connection, then click the **+** (Add device) button on the connection row, or open the connection and click **Add device** in the Connected Devices tab.

## Step 1 — Create the sensor profile

The dialog opens in Add mode, showing only the basic sensor info. No tabs or navigation are visible yet.

- **Device photos** — Snap a picture of the sensor so you can easily identify it later. Helpful when you have several similar-looking sensors.
- **Device name** — Give it a name that tells you what it is and where it is. "Kitchen Temperature" is much more useful than "Sensor 4."

Enter a name for your sensor and click **Save**. The profile is created and the dialog transitions to edit mode.

## Step 2 — Configure the connection and details

After the first save, the dialog reopens with **Device info**, **Connection**, **Metrics** and **Logs** tabs, and a **Next** button for navigating between them. Two more appear when they apply: **Commands & States** on a device you can switch on and off, and **Emulator** on a pretend sensor.

### Connection

Click the **Connection** tab to link your sensor to the thing that feeds it.

**For LoRaWAN sensors (LNS connection):**

1. Select your **LNS** connection from the **Connector type** dropdown (if you only have one, it may be pre-selected).
2. Enter the **Device EUI** — the unique identifier from your sensor's label (a string of hexadecimal characters, usually printed on the sensor or its packaging). Once entered and saved, this field locks to prevent accidental changes. Capital and lowercase letters are treated the same here, so it doesn't matter which your label uses — just copy it carefully.

   **Or skip the typing entirely.** Most sensors carry a QR code on the label or the box. Click **Scan QR code**, point your laptop or phone camera at it, and Chirp fills the identifiers in for you — no squinting at sixteen characters of hex, no transposed digits to hunt down later. If your device doesn't have a camera available, you'll see "QR code scanner is not found. Please try again." — just type the values in by hand instead.
3. Choose how to set up the sensor profile:

   **Option A: Use device profile templates** — Check the **Use device profile templates** box to select from a library of known sensors. This is the easiest approach if your sensor brand is in the library.

   - Pick the **Brand**, **Model**, and **Profile** from the dropdowns. These selections identify which template to load.
   - Once all three are selected, Chirp fetches the matching template and fills in the sensor's settings automatically — including the LoRaWAN class, frequency band, and a **codec** (the decoding logic that translates the sensor's raw data into readable fields).

   Templates are provided as convenience helpers. If a template's codec doesn't produce the correct readings for your sensor — for example, if values look wrong or fields are missing — you can edit the **Code functions** field directly (see below).

   **Option B: Manual setup** — Leave the checkbox unchecked to enter details yourself:

   - **Class** — Choose the LoRaWAN device class:
     - **Class A** — The sensor sleeps between transmissions and only briefly wakes to listen for responses. This is extremely power-efficient — most battery-powered home sensors use Class A and can run for years on a single battery.
     - **Class C** — The sensor keeps its receiver on continuously, so it can receive commands from Chirp at any time. Because the radio is always listening, Class C sensors use significantly more power and are typically plugged into mains power. Choose Class C for devices that need to respond to commands instantly, such as smart switches or displays. A Class C sensor gets a **Commands & States** tab so you can control it — see [Controlling Your Devices](commands/).
   - **Brand** and **Model** — Type the sensor manufacturer and model name.
   - **Band** — Select the LoRaWAN frequency band for your region. Sensors purchased from a local supplier are almost always on the correct band already. Available options: EU868 (Europe), US915 (USA), AU915 (Australia), AS923 (Asia), KR920 (South Korea), IN865 (India), RU864 (Russia), CN470 (China), CN779 (China), EU433 (Europe 433 MHz), ISM2400 (2.4 GHz global). For a complete list by country, see [LoRaWAN Frequencies](../connectors/lns-connector/lorawan-frequencies.md).
   - **AppKey** — The encryption key for your sensor, typically found on the sensor's packaging or in its documentation.

#### Keep the identifiers somewhere safe

Once you've entered the sensor's identifiers, click **Add to Vault**. Chirp saves the EUI and its key together in your Key Vault, so you can look them up later without hunting for the box in the loft or unscrewing the sensor off the wall. For LoRaWAN sensors it stores the AppKey alongside the Device EUI.

It's worth doing at the moment you have the label in your hand — that's the one time the numbers are easy to get at. See [Key Vault](../reports/key-vault.md).

#### Code functions (codec)

The **Code functions** field contains the logic that decodes your sensor's raw data into readable fields. Think of it as a translator — your sensor sends its readings as compact binary data, and the codec turns that into named values like `temperature`, `humidity`, or `battery`.

When you pick a device profile template, this field is filled in automatically. If you set up manually, it starts empty — you may need to paste a codec from your sensor's manufacturer documentation.

If the readings in the Metrics tab don't look right after connecting your sensor — values seem wrong, some fields are missing, or names don't match what you expected — you can open this field and edit the code. The field is a text editor with a code-friendly monospace font.

#### Data sending interval

Every sensor sends on its own schedule — some every few minutes, some once a day, some once a month. That schedule is set **on the sensor itself**, and it differs from brand to brand: some sensors arrive with it already set by the manufacturer, others you set yourself when you install the sensor. The **Data sending interval** field is simply where you tell Chirp what that schedule is.

Set it to match how the sensor is actually configured to send. A sensor that reports once a day → **1 day**; once a month → **1 month**. The field starts at **1 hour** by default, but that's only a placeholder — Chirp has no way to know your sensor's real schedule, so replace it with the right value.

If nothing arrives within the interval, the sensor shows as offline in your sensor list and the Devices card on your home overview flags it. Getting this right is what stops a perfectly healthy sensor from looking offline just because it's quiet between its scheduled reports.

Pick a number and a unit: **minute**, **hour**, **day**, **week**, or **month**.

A [pretend sensor](pretend-sensors.md) is the exception: there is no hardware keeping a schedule, so this field *is* the schedule — Chirp sends on it.

**For vehicle trackers (Tracker connection):**

1. Select your **Tracker** connection from the **Connector type** dropdown.
2. Enter the **Unique ID** for your tracker.
3. Select a **Device model** by searching the tracker library.
4. A **Url for GPS tracker** panel appears — copy this URL and configure your tracker to send data to it.

**For MQTT sensors (Cloud or External MQTT):**

1. Select your **MQTT** connection from the **Connector type** dropdown.
2. Enter the **Device ID** — the device-level part of the topic your sensor publishes under. For Zigbee2MQTT that's the friendly name, and it has to match byte-for-byte.
3. Save, and let the sensor publish at least once before you map its readings — see [A note for MQTT sensors](#a-note-for-mqtt-sensors) below.

**For pretend sensors (Emulator connection):**

1. Select your **Emulator** connection from the **Connector type** dropdown.
2. Choose a **Device ID** — up to 64 characters (letters, numbers, spaces, dots, underscores, dashes), unique across all of Chirp. See [Pretend Sensors](pretend-sensors.md).
3. Say **how often it reports**, and either tick **Use device preset** to borrow a real model's readings or add them yourself.

Chirp then invents the readings for you, and an extra **Emulator** tab appears so you can push a value whenever you want to test something. This is how you get your dashboards and alerts working before the hardware arrives — and you can switch the same sensor over to the real one when it does. See [Pretend Sensors](pretend-sensors.md).

### Metrics

Click the **Metrics** tab to map your sensor's raw data to measurement definitions. If you selected a device profile template, the mappings may already be filled in. Otherwise, you can assign data templates manually here or come back to it later.

#### See what your sensor is sending

Once your sensor is connected and transmitting, the Metrics tab shows a live view of the raw data — a table listing every field your sensor sends, its current value, and when it last updated. You see exactly what's coming in, with the actual field names the sensor uses (like `t`, `hum`, `battery_mv`, or whatever the manufacturer chose).

#### Map raw fields to your data templates

This is where cryptic sensor output becomes something you can actually read. When you map a raw field like `t` to a data template called "Temperature" with the unit °C, Chirp starts displaying that reading as "Temperature (°C)" everywhere — in dashboards, automations, alerts, and history charts. You're giving each raw field a proper name, unit, and format.

To set up a mapping:

1. **Add a metric** — Click **Add key** and pick a data template from the dropdown (e.g., "Temperature", °C, Float). The Unit, Type, and Data type columns fill in automatically from the template. If you need a template that doesn't exist yet, create one in [Data Templates](data-templates.md).
2. **Choose the matching field** — In the **Connector key** dropdown, pick the raw field name that carries this measurement (e.g., pick `t` if your sensor sends temperature as `t`).
3. **Save** — The data starts flowing immediately through your dashboards, automations, alerts, and history.

If the Connector key is not filled in, the data for that metric will be ignored.

Add as many metrics as your sensor reports — you can map them all in one go.

#### Works with any sensor — even prototypes

This is not limited to sensors in Chirp's device library. If you're testing a prototype sensor that doesn't have a standard codec, a DIY sensor with custom firmware, or older hardware that sends cryptic field codes instead of readable names — it all works. As long as Chirp receives the data, you see the fields and map them.

For details on data templates, see [Data Templates](data-templates.md).

#### A note for MQTT sensors

Two things behave differently for sensors connected through the [MQTT connector](../connectors/mqtt-connector.md), worth knowing before you start mapping:

- **The Connector key dropdown is empty until your sensor has published at least once.** The dropdown lists keys actually received from your device. For a brand-new MQTT device, that means a two-pass save: add a row per metric and pick a normalized template, leave the Connector key blank, save, ensure your device is publishing, reopen the device — the dropdown now lists the payload keys, match each row, save again.
- **The Mapping tab Value column and the Logs tab show different things.** The Value column is a live snapshot of the most recent payload. The Logs tab is per-sensor history, populated only by publishes that arrive *after* you save the Connector keys. Older publishes don't fill in retroactively — generate a fresh publish (use a Z2M web UI control, send a `/get` poll, or wait for the device's next scheduled report — don't rely on a wall-switch toggle, which doesn't generate a publish on many Zigbee bulbs) after saving Connector keys to populate the Logs tab.
- **Mapping is iterative.** The first publish may reveal payload keys you didn't anticipate. Return to the device's Mapping tab whenever you want to add more fields — review the Connector key dropdown and Value column, add rows for the keys you missed, set the right Data type, save, and generate another publish so the Logs tab starts collecting history for the new mappings.

For full details, see [Topics and device routing](../connectors/mqtt/topics-and-device-routing.md).

### Logs

The Logs tab is empty until your sensor starts sending data. Once it does, raw readings appear here grouped by timestamp.

Click **Save** again to persist the connection and metrics configuration.

## After saving

Your sensor's profile appears in the sensor lists throughout Chirp.

For LoRaWAN sensors, data starts flowing once the sensor powers on and connects to your gateway. For trackers, data flows once the physical device starts reporting to the URL you configured.

Worth knowing about that LoRaWAN connection: registering the sensor here sets Chirp up to recognize it, but the sensor still has to *join* the network itself before it sends anything. A sensor straight out of the box does that on its own the moment you power it up. A sensor with a past life — second-hand, inherited with the house, or previously set up on something else — is still joined to that old network and needs a reset before it will join yours. See [First things first: joining the network](connection-diagnostics.md#first-things-first-joining-the-network).

**Saved everything and still seeing no readings?** Don't start pulling batteries out. Open the sensor's **Connection** tab — Chirp will tell you exactly where the data has stopped and what to do about it. See [Connection Diagnostics](connection-diagnostics.md).

The registration dialog works comfortably on a phone, so you can add a sensor while you're standing at the spot where you're installing it.

## What's next

- **Customize data templates** if Chirp doesn't automatically recognize what your sensor measures. See [Data Templates](data-templates.md).
- **View and edit your sensor** anytime. See [Sensor Details](sensor-details.md).
- **Nothing showing up?** See [Connection Diagnostics](connection-diagnostics.md).
