# Connect Your First Sensor

Let's get something working. This guide walks you through the simplest LoRaWAN path to live data on your screen and an alarm watching over it. Not every Chirp setup starts with a gateway, but this one does because it covers the LNS / LoRaWAN route. Every feature has its own section later — here we're just getting you up and running.

**You'll need:**
- A Chirp account
- A LoRaWAN gateway (the small box that receives signals from your sensors)
- A LoRaWAN sensor (like a door sensor or temperature sensor) — along with its Device EUI and AppKey, usually printed on the device or its packaging

**By the end, you'll have:**
- A gateway receiving signals in your home
- A connector linking the gateway to Chirp
- A sensor sending live readings
- A room dashboard showing your data
- An alarm that notifies you when something needs attention

---

## Step 1: Set up your gateway

The gateway is the bridge between your wireless sensors and Chirp. It plugs into your home network and listens for sensor signals within range.

Your gateway needs to support the **Basics Station** protocol — this is how it connects securely to Chirp using encrypted TLS certificates (which is why you'll download a certificate bundle during setup). Most modern LoRaWAN gateways support this; check the specifications when choosing one.

1. Plug in your gateway and make sure it has power plus an internet connection or backhaul (for example Ethernet, Wi-Fi, or LTE, depending on the model).
2. In Chirp, click **Gateways** in the left menu.
3. Click **Add gateway** in the top-right corner.
4. Give it a **name** — like "Living Room Gateway" or "Home Hub."
5. Choose the right **region** for your gateway hardware and location:
   - Usually this matches the band your gateway was sold or configured for
   - **EU868** for most deployments in Europe
   - **US915-0 / US915-1** in the United States, depending on the network setup
   - **EU433** only if your gateway is specifically built or configured for 433 MHz
   - Other regions are in the dropdown
6. Type in the **Gateway EUI** — a 16-character code printed on a sticker on the gateway, usually on the bottom or back.
7. Click **Next**.

### Connect your gateway to Chirp

The next screen shows two important things:

8. An **LNS address** — this is the server URL your gateway needs. Click the **copy icon** to copy it.
9. A **Download certs.zip** button — click it to download the security certificates.
10. Click **Continue**.

Now open your gateway's settings page in your browser (find its IP address on your router's connected devices list) and enter:
- The **LNS address** you just copied
- The **certificates** from the zip file

The exact steps depend on your gateway model — check the guide that came with it. Once connected, the gateway shows as **online** in your Gateways list. This may take a couple of minutes.

> **Where to put it:** A central, elevated location works best. For an apartment, one gateway usually covers everything. For a house, the main floor is a good choice.

---

## Step 2: Create a connection

Before adding sensors, you need a connection. A connection tells Chirp which protocol to listen on — in this case, LoRaWAN.

1. Click **Connectors** in the left menu.
2. Click **Add connector** (or the **Add connector** button if you haven't set one up yet).
3. Select **LNS** from the **Connector type** dropdown.
4. Click **Add**.

Done — the connection is created. No extra setup needed. Chirp handles the LoRaWAN network integration automatically.

---

## Step 3: Add your sensor

With the gateway online and the connection in place, you can register your first sensor — giving it a profile in Chirp that tracks its state, readings, and history.

1. In the **Connectors** page, click on your **LNS** connection to open it.
2. Click the **Connected Devices** tab.
3. Click **Add device**.

### Create the sensor profile

The dialog opens showing only the basic info:

4. Type a **name** — like "Front Door Sensor" or "Bedroom Temp."
5. Optionally add a **photo** of the sensor.
6. Click **Save**.

The sensor profile is created and the dialog transitions to edit mode with all tabs visible.

### Configure the connection

7. Click the **Connection** tab.
8. Select your **connector** from the dropdown.
9. Under **"Use device profile templates"**, check the box if your brand is in the list:
   - Pick the **Brand** (e.g., Dragino, Milesight, Browan).
   - Pick the **Model** — the list narrows by brand.
   - **Profile** (band and device class) fills in automatically.
10. If your sensor isn't listed, leave the checkbox unchecked and enter:
    - **Device EUI** — 16 characters, printed on the sensor or its box.
    - **AppKey** — 32 characters, also included with the sensor.
11. Click **Save**.

The sensor appears in the Connected Devices list. It needs a moment to join the network through your gateway — most sensors send their first reading within a minute or two.

> **Don't see your brand?** No problem — leave the template checkbox unchecked and enter the Device EUI and AppKey manually. Chirp works with any LoRaWAN sensor. You can configure data templates later to define how raw data maps to meaningful readings. See the [Data Templates](../devices/data-templates.md) section for details.

---

## Step 4: See your live data

Once your sensor has reported in, you can view its data in two ways:

- Click a **sensor row** in the Connected Devices list — the sensor's detail page opens. Click the **Metrics** tab to see readings.
- Or check **Devices** in the sidebar to see all your sensors and their status.

The best way to keep an eye on your data is through a dashboard — which we'll set up next.

---

## Step 5: Create a room dashboard

Dashboards let you see data from one or many sensors at a glance.

1. Click **Dashboards** in the left menu.
2. Click **Add dashboard**.
3. In the modal:
   - Pick an **icon** for the dashboard.
   - Enter a **name** — like "Front Door" or "Home Overview."
   - Optionally choose a **folder** or add a **description**.
4. Click **Save**.

### Add your sensor's data

5. On the new dashboard, click **Add widget**.
6. **Choose your device** from the list.
7. **Choose a metric** — like door status or battery level. You'll see a live preview of how the widget will look.
8. Click **Choose** to add it.

Repeat to add more widgets. **Drag** them to rearrange and **resize** by pulling their edges.

> **Idea:** Create a dashboard for each room, or one "Home Overview" with the most important reading from each sensor.

---

## Step 6: Get alerted when something happens

Let's set up an alarm so Chirp tells you when the door opens.

1. Click **Alarm** in the left menu.
2. Click **Add alarm rule** in the top-right corner.
3. In the modal, fill in:
   - **Name** — like "Front Door Opened."
   - **Title** — the subject of the alert (e.g., "Door Alert").
   - **Body** — the message (e.g., "The front door has been opened.").
   - **Severity** — pick **Critical** if this needs immediate attention, **High** or **Medium** for important but non-urgent events, or **Low** / **Info** for things you just want to know about.

### Who gets notified

4. The first **escalation step** is pre-configured with your account and email.
   - Choose additional **channels** if available (SMS, push notifications).
   - To escalate further: click **Add step** — for example, notify your partner if you don't respond within 10 minutes.
   - Set the **delay** between steps.
5. Click **Save**.

The alarm rule is now watching. When triggered, an alarm appears in **Alarm → Inbox** and you receive a notification through your configured channels.

---

## You're up and running

That's it — you have a working LoRaWAN smart home setup:

- A **gateway** receiving signals from your sensors
- A **connector** linking the network to Chirp
- A **sensor** sending live data
- A **dashboard** where you see it all at a glance
- An **alarm rule** keeping watch while you don't

From here, you might want to:

- **Add more sensors** — Repeat Step 3 for each new device through your connector
- **Build automations** — Check out the Automation section for rules like "alert me if the door opens after midnight"
- **Invite your family** — Go to **Users** in the user menu to invite family members and control what they can see and change
- **Explore the AI helper** — Ask it *"When was the front door last opened?"* and get a real answer from your data
