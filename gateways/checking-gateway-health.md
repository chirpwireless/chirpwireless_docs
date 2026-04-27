# Checking Gateway Health

Once your gateway is registered, you can check on it anytime to see whether it's online, how long it's been running, and how much sensor data it's handling.

## Finding your gateway

Click **Gateways** in the sidebar to see all your gateways. Each one shows its name, current status (online or offline), and when it was last seen. Click any gateway to open its detail page.

## The gateway detail page

Your gateway's detail page shows an overview card at the top and several health cards below it.

### Overview card

The overview card shows your gateway's photo (if you've added one), its name, and its current status. You can also star your gateway from here to add it to your [Favorites](../devices/favorite-devices.md).

### Availability

The Availability card shows your gateway's uptime — how reliably it's been connected to Chirp over time. A healthy home gateway should show high availability. If you see dips, it usually means the gateway lost internet or power during those periods.

### Traffic

The Traffic card shows how much data your gateway has handled. This gives you a sense of how active your sensors are. If you have several sensors reporting regularly, you'll see steady traffic here.

### Pings

The Pings card shows the history of connectivity checks between your gateway and Chirp. Regular successful pings mean your gateway's connection is stable. Gaps in pings might indicate intermittent internet issues.

## When to worry (and when not to)

**Normal behavior:**
- Brief offline periods during internet outages or router restarts
- Small dips in availability after a power cut — the gateway reconnects automatically
- Traffic that varies depending on how many sensors you have and how often they report

**Worth investigating:**
- Gateway shows offline for more than an hour when your internet is working fine
- Availability drops significantly over several days
- No traffic at all even though you have active sensors

If your gateway stays offline, try the troubleshooting steps in [Setting Up Your Gateway](setting-up-your-gateway.md) — the most common fix is verifying the LNS address and certificates.

## Gateway settings

From the gateway detail page, you can also access the **Settings** section where you can:

- Update the gateway's name
- Change its assigned location (room)
- Download or regenerate certificates if you need to reconfigure the hardware
- View the gateway's unique identifier (EUI) and region
- Delete the gateway if you no longer need it
