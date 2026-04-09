# Adding Sensors

Every sensor you add to Chirp gets its own profile — a record that remembers the sensor's name, connection details, measurement settings, and full data history. Even when a sensor goes to sleep between transmissions, its profile keeps everything organized and ready for dashboards and automation. Because the physical sensor binding is optional, you can set up your entire system first and connect the actual hardware later — opening the door for device emulators that let you design and test your setup before any physical sensors are installed.

## Before you start

You'll need:
- **A connection** set up — an LNS connection for LoRaWAN sensors, or a Tracker connection for vehicle trackers. See [Setting Up a Connection](../connectors/setting-up-a-connection.md).
- **Your sensor's identifiers** — for LoRaWAN sensors: the **Device EUI** and **AppKey**, usually printed on the sensor or its packaging. For trackers: the **Unique ID** from the manufacturer.

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

After the first save, the dialog reopens with four tabs — **Device info**, **Connection**, **Metrics**, and **Logs** — and a **Next** button for navigating between them.

### Connection

Click the **Connection** tab to link your sensor to a physical device.

**For LoRaWAN sensors (LNS connection):**

1. Select your **LNS** connection from the **Connector type** dropdown (if you only have one, it may be pre-selected).
2. Enter the **Device EUI** — the unique identifier from your sensor's label. Once entered and saved, this field locks to prevent accidental changes.
3. Choose how to set up the sensor profile:
   - **Use device profile templates** — Check this box to select from a library of pre-configured sensor profiles. Pick the **Brand**, **Model**, and **Profile** (frequency band) from the dropdowns. This is the easiest approach if your sensor brand is in the library.
   - **Manual setup** — Leave the checkbox unchecked to enter details yourself: **Class** (A for battery sensors, C for mains-powered), **Brand**, **Model**, **Band** (frequency), and **AppKey** (the encryption key from your sensor's documentation).

**For vehicle trackers (Tracker connection):**

1. Select your **Tracker** connection from the **Connector type** dropdown.
2. Enter the **Unique ID** for your tracker.
3. Select a **Device model** by searching the tracker library.
4. A **Url for GPS tracker** panel appears — copy this URL and configure your tracker to send data to it.

### Metrics

Click the **Metrics** tab to map your sensor's raw data to measurement definitions. If you selected a device profile template, the mappings may already be filled in. Otherwise, you can assign data templates manually here or come back to it later.

#### See what your sensor is sending

Once your sensor is connected and transmitting, the Metrics tab shows a live view of the raw data — a table listing every field your sensor sends, its current value, and when it last updated. You see exactly what's coming in, with the actual field names the sensor uses (like `t`, `hum`, `battery_mv`, or whatever the manufacturer chose).

#### Map raw fields to your data templates

To turn raw data into something useful:

1. **Add a metric** — Tap **Add metric** and pick a data template from your library (e.g., "Temperature", °C, Float). If you need a template that doesn't exist yet, create one in [Data Templates](data-templates.md).
2. **Choose the matching field** — In the dropdown next to that metric, pick the raw field name that carries this measurement (e.g., pick `t` if your sensor sends temperature as `t`).
3. **Save** — The data starts flowing immediately through your dashboards, automations, alerts, and history.

Add as many metrics as your sensor reports — you can map them all in one go.

#### Works with any sensor — even prototypes

This is not limited to sensors in Chirp's device library. If you're testing a prototype sensor that doesn't have a standard codec, a DIY sensor with custom firmware, or older hardware that sends cryptic field codes instead of readable names — it all works. As long as Chirp receives the data, you see the fields and map them.

For details on data templates, see [Data Templates](data-templates.md).

### Logs

The Logs tab is empty until your sensor starts sending data. Once it does, raw readings appear here grouped by timestamp.

Click **Save** again to persist the connection and metrics configuration.

## After saving

Your sensor's profile appears in the sensor lists throughout Chirp.

For LoRaWAN sensors, data starts flowing once the sensor powers on and connects to your gateway. For trackers, data flows once the physical device starts reporting to the URL you configured.

## What's next

- **Customize data templates** if Chirp doesn't automatically recognize what your sensor measures. See [Data Templates](data-templates.md).
- **View and edit your sensor** anytime. See [Sensor Details](sensor-details.md).
