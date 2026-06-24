---
description: Tour the Chirp interface — left menu, profile options, notification bell, home screen — find where everything lives.
---

# Finding Your Way Around

Here's a quick tour of the Chirp interface so you know where everything lives.

## The menu on the left

The left side of the screen has your main menu. Everything you need is organized here, top to bottom.

You can tuck the menu away when you do not need it — hover over the Chirp logo at the top and click the double-chevron that appears. The menu collapses to just icons, giving your dashboards and data the full screen. Click the chevron again to bring the labels back. This is especially handy if you use a tablet or touchscreen to display your dashboards.

### Your main sections

- **Overview** — Your home screen. Summary cards showing your sensor and gateway counts, and recent alarms. Think of it as the front page of your smart home.
- **Dashboards** — Custom views you build for any room or purpose. Create a "Kitchen" dashboard, a "Garden" view, or a "Security" overview. Organize them in folders and fill them with the sensor data that matters to you.
- **Connectors** — Define which protocols Chirp listens on. Connector types: **LNS** (for LoRaWAN sensors), **Tracker** (for vehicle trackers — OBD2, CAN bus, standalone GPS), and **MQTT** (for Zigbee sensors via Zigbee2MQTT, DIY hardware, and other MQTT-capable devices). Click an LNS connection to see **LoRaWAN Gateways** and **Connected Devices** tabs. A Tracker connection shows the sensor list directly. Sensors are registered separately through the sensor dialog.
- **Devices** — See all your registered sensors in one place. Browse and search. Click any sensor to view or edit its details.
- **Gateways** — Your LoRaWAN gateways (must support Basics Station protocol for secure connectivity). See which ones are online, check their signal stats, add a new gateway, or update firmware.
- **Alarm** — Your alert headquarters, with three tabs:
  - **Inbox** — See every alarm that's been triggered. Each one shows what happened, how serious it is (from Critical down to Info, with High, Medium, and Low in between), which sensor triggered it, and whether it's been resolved. Filter by severity or status, and search through past incidents.
  - **Alarm definitions** — The alarm rules you've set up. Create rules that define when to alert you, who gets notified, and how urgently. Rules support escalation — if nobody responds within a set time, the alert can automatically reach the next person or channel.
  - **Settings** — Configure how different severity levels behave and manage delivery preferences.
- **Rules engine** — Your automation builder. Create rules visually: "if this sensor reads this, then do that." Rules can be as simple or as detailed as you need.
- **Reports** — Activity and audit information for your household.
  - **Audit Trail** — A log of membership activity in your household. See when users were invited, when they joined, when permissions changed, and when someone was removed.

### Settings

Click **Settings** to see more options:

- **Profile settings** — Change your name, email, profile photo, or password. You can also delete your account from here.
- **Locations** — Set up your rooms and zones. Once defined, you can filter devices by location and organize dashboards by room.
- **Device sharing** — See which devices you've shared with family members and manage who has access to what.
- **API Keys** — For power users and tinkerers. Create secure keys to connect Chirp with your own scripts, home automation setups, or other services. Each key has specific permissions and can be set to expire automatically.
- **New device request** — Can't find your sensor's model when adding it? Choose **New device request** to ask the team to add support. Tell them the **Brand**, **Model**, and **Band**, and add a **Documentation link** or **Codec link or code** if you have one, then tap **Send request** — you'll see a confirmation once it's on its way.
- **Changelog** — See what's new in the latest platform updates.

### At the bottom

- **Get Help** — Opens a form where you can describe your issue, enter your email, and send a message directly to the support team.
- **Docs** — Opens this documentation.

### Making more space

You can collapse the menu to just icons by using the collapse arrow. This gives more room for dashboards and device views. Hover over the collapsed menu to temporarily see the labels.

## Your profile menu

Click your **name or photo** in the bottom-left corner to open a dropdown. This is where you'll find several important things that aren't in the main menu:

- **Language** — Switch between English, German, French, Spanish, and Portuguese. The change is instant and Chirp remembers your choice.
- **Dark / Light mode** — Toggle between themes. Dark mode is great for checking sensors before bed or in dimly lit rooms.
- **Subscription** — See which plan you're on, how many devices and rules you're using, and upgrade if you need more.
- **Users** — Manage members of your organization — invite people, set permissions, and control who can see or change what. This is how you share your smart home with family members, roommates, or a landlord.
- **Organization settings** — Change your organization's name or transfer ownership. Only visible to the organization owner.
- **Log out** — End your session.

### Switching organizations

Under **My organizations** in the menu, you'll see all organizations you belong to — for example, your own home and a vacation property you manage. Pick a different one and the entire interface switches — different devices, different rules, different members. Each organization is completely separate.

## The notification bell

On desktop, a small **bell icon** appears near your profile. It shows a number badge when you have unread alarms. Click it to see recent alarms in a sidebar without leaving whatever page you're on.

## Your home screen (Overview)

When you open Chirp, you land on the **Overview** page — titled **"My board"** in the interface.

### At the top: counts and status

Two cards show how your home is doing:

- **Devices** — How many sensors you have. Warnings appear if any aren't communicating.
- **Gateways** — How many are online. If one drops off, you'll see it immediately.

### Below: recent alarms

- **Recent alarms** — Latest triggered alarms. What happened, which device, when. Mark all as read, or click one for the full story.

Everything updates automatically — new readings and alarms appear without refreshing.

## Managing your devices

Sensors are added and managed through **Connectors** or **Devices**. Adding a new sensor opens a dialog where you enter a name and save. The dialog then transitions to edit mode with four tabs:

- **Device info** — Name your sensor and add photos.
- **Connection** — Choose the connector type, select a known device profile (brand, model, frequency band) or enter credentials manually (Device EUI, AppKey).
- **Metrics** — Choose which sensor parameters the device reports, using templates.
- **Logs** — See the device's activity history.

This same dialog is used for adding new devices and editing existing ones.

## Inside a gateway page

Click a gateway to see:

- **Overview** — Whether it's online, how long it's been running, signal quality, traffic, and which devices connect through it.
- **Settings** — Change the name, update the location, manage antenna configuration.
