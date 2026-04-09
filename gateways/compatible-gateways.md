# Compatible Gateways

Chirp works with LoRaWAN gateways that support the **Basics Station** protocol. This is the key thing to check when buying a gateway for your smart home.

## What is Basics Station?

Basics Station is a modern, secure way for gateways to connect to a LoRaWAN network. It uses encrypted connections (TLS), which means your sensor data is protected in transit — nobody can intercept readings between your gateway and Chirp.

Some older gateways use a different protocol called UDP Packet Forwarder, which sends data without encryption. **Chirp does not support UDP Packet Forwarder.** If a gateway only supports the legacy UDP protocol, it won't be able to connect.

## What to look for when buying

When shopping for a gateway, check for these features:

| Feature | What to look for |
|---------|-----------------|
| **Protocol** | Must support **LoRa Basics Station** (sometimes listed as "LNS protocol" or "Basics Station compatible") |
| **Frequency band** | Must match your region — EU868 for Europe, US915 for the United States, etc. |
| **Internet connection** | Ethernet or Wi-Fi — choose based on where you plan to place it |
| **Power** | Most home gateways use a simple wall adapter. Check that one is included or that you have the right plug for your country |
| **Indoor vs outdoor** | For most homes, an indoor gateway is fine. Outdoor-rated gateways are useful if you want to cover a large garden or outbuildings |

## How to check if your existing gateway is compatible

If you already have a LoRaWAN gateway, check its documentation or settings page for a Basics Station option. Many gateways support multiple protocols and can be switched to Basics Station through a firmware update or configuration change.

Look for settings labels like:
- "Basics Station"
- "LNS mode"
- "Semtech LNS"
- "CUPS/LNS"

If your gateway only mentions "Packet Forwarder" or "Semtech UDP" without a Basics Station option, it may need a firmware update or may not be compatible.

## One gateway is enough for most homes

LoRaWAN has impressive range — a single indoor gateway typically covers:
- An entire apartment
- A multi-story house
- A house plus garden and garage

Signals pass through walls, floors, and ceilings, so you generally don't need one per room. Start with a single gateway placed centrally and at a moderate height (a shelf or wall mount works well). If you find that sensors in far corners aren't connecting reliably, you can always add a second gateway later.
