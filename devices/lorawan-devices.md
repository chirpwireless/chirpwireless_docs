---
description: "Connect LoRaWAN sensors to Chirp digital twins: device profiles, keys, decoding, measurement mapping, commands and replacement."
---

# LoRaWAN Devices

LoRaWAN sensors talk by radio: they transmit tiny readings, a nearby gateway picks them up, and Chirp's LNS connector, with its built-in LoRaWAN Network Server, takes it from there. The sensor is only the source of the numbers. Everything you actually look at in dashboards and automations lives on its **digital twin**: the name, the measurement channels and the retained history.

Picture a **Garden Soil** device. Swap the soil-moisture probe next spring and the readings you rely on for watering decisions stay put. Pick this connection when your hardware speaks LoRaWAN; sensors that use Wi-Fi or Zigbee go through a different route.

## Before you start

- Set up the [LNS connector](../connectors/lns-connector/README.md) and make sure a connected [LoRaWAN gateway](../gateways/lorawan-gateways/README.md) covers the spot where the sensor will sit. Installing the gateway and activating the network are separate jobs from registering the sensor.
- Collect these from the manufacturer: the sensor's **Device EUI**, its **AppKey**, the model, the frequency band, the class, and a payload codec that fits the model. The band has to suit both the hardware and your gateway; [LoRaWAN Frequencies](../connectors/lns-connector/lorawan-frequencies.md) lists the options.
- Your account needs permission to create and edit devices, and your plan needs room for one more twin. Users with read-only access can look at the configuration but cannot save.

## Connect the sensor to its digital twin

1. Go to **Devices → Add device**, or press **Add device** on the LNS connector's row.
2. Type a **Device name** such as **Garden Soil**, add photos if you like, and click **Save**. That creates the digital record before any hardware is attached. [Shared registration steps](adding-sensors.md) cover profile and Application settings.
3. Switch to **Connection** and pick your LNS connection under **Connector type**.
4. Fill in the sensor's identity and profile, following the reference tables below.
5. Enter the real reporting schedule in **Data sending interval** and click **Save**.
6. Make the sensor join the network by following the manufacturer's commissioning steps; saving the registration does not start a radio join by itself. A sensor that was commissioned elsewhere may first need a rejoin or reset. Follow the manufacturer's instructions, because simply cutting the power often is not enough.
7. Once the first uplink shows up, go to **Mapping**, assign the decoded readings and save. After the next uplink arrives, open **Logs** to see the recorded measurements.

### Identity and credentials

| Control | What to enter or do |
| --- | --- |
| **Connector type** | Choose the LNS connection that belongs to your organization. Missing from the list? Use **Connector section** to create it. After the physical device is bound, the connection and identity stay locked during normal editing. |
| **Device EUI** | The sensor's 8-byte identifier from the manufacturer: 16 hexadecimal characters, shown in pairs of bytes. It names the hardware, not the thing you are monitoring, and becomes read-only once the device is bound. |
| **Scan QR code** | Point your browser's camera at a compatible label. A scan can fill in Device EUI and, if the code includes one, AppKey. Check what was filled in. No camera, or camera access refused? Type the values yourself. |
| **AppKey** | The sensor's 16-byte activation key, written as 32 hexadecimal characters. Use the key that is set on the hardware itself; a profile template never carries the key of your individual sensor. While you type, the key is visible, and it is hidden again when you leave the field or press Enter. The eye icon toggles a non-empty key, and a key that arrived through a QR scan stays hidden. Keep it out of screenshots you share. |
| **Add to Vault** | Stores the EUI and key as a pair in [Key Vault](../reports/key-vault.md) while you still have the credentials in front of you. Saving to the vault is a separate action from saving the device's connection. |
| **Detach physical device** | Removes the hardware binding at once. Reach for it when swapping hardware, then bind the replacement to the same twin. The measurement rows can stay as they are; only their incoming keys need remapping. [Replacement and history](sensor-details.md) walks through it. |

### Templates and manual profiles

A **device profile** carries the radio settings plus a **codec**, a piece of JavaScript that turns the sensor's binary uplinks into named readings. It does not build the measurement mappings for you.

| Control | Configuration |
| --- | --- |
| **Use device profile templates** | Turn on to choose a known profile; turn off to type the profile in by hand. Whatever gets filled in, look it over before saving, particularly when firmware or regional variants differ. |
| **Brand** (template selector) | Pick the manufacturer. The choice decides which models you can select. |
| **Model** (template selector) | Pick the hardware model. The choice decides which regional profiles appear. |
| **Profile** | Pick the regional profile that fits. It fills in the profile's class, band and codec, and can overwrite values you entered earlier. |
| **Class A / Class C** | Required. Pick the class the sensor really supports or has been set to. Class A only listens for downlinks in short windows right after it transmits, while Class C keeps listening between transmissions. Choosing Class C in the form does not turn Class A hardware into an always-listening device. Commands can be defined for both classes, but the delivery timing is different. |
| **Brand / Model** (text fields) | Required names of the manufacturer and the model for the saved profile. They stay visible and editable after you choose a template. |
| **Band** | Required regional radio plan, with EU868, US915, AU915, AS923, KR920, IN865, RU864, CN470, CN779, EU433 and ISM2400 on offer. Use the plan that matches both sensor and gateway. |
| **Code functions** | Review or paste the codec supplied for your sensor. A radio message that arrives without a suitable decoder does not necessarily yield measurement fields you can use. Edits apply to messages received after you save; history that was already decoded is not decoded again. |
| **Data sending interval** | A positive whole number plus a unit: **minute**, **hour**, **day**, **week** or **month**. It starts at **1 hour**. Set it to match the hardware's real schedule. Diagnostics use it to know when to expect data, but it never changes how the physical sensor transmits. |

Always take the codec made for the exact model and payload format. The **Code functions** editor may also hold the codec's downlink encoder; the [custom encoder](commands/creating-commands.md) section of the command guide explains when a command relies on it and when it brings its own.

## Map the readings you need

Say a probe decodes into `temperature` and `battery`. Go to **Mapping**, click **Add key**, pick a **Normalized key** template, then choose the matching **Device data key**. For decimal temperatures, take a template with the right unit and the Float type. Save your assignments and wait for a fresh uplink.

A template fixes the meaning, the unit and the value type; choosing °C does not convert a reading that is in Fahrenheit. The **Value** and **Last update** columns help you recognize an incoming field, and **Logs** shows the retained measurements once mapping is done. [Mapping controls](sensor-details.md#metrics), [metric templates](data-templates.md) and [payload interpretation](what-your-device-is-sending.md) cover every field and the conversion rules.

## Commands and ongoing operation

Once the physical binding is saved, devices that support it get a **Commands & States** area. Press **Add new command** to define an action the hardware can carry out. On LoRaWAN, a command needs an **fPort** and an encoded payload; the **Confirmed downlink** switch decides whether the radio acknowledges it, and the verification settings then check what the device reports back. Details are in [Creating Commands](commands/creating-commands.md) and [verification](commands/verification.md).

With **Garden Soil**, the readings you mapped can drive a chart and an alarm at the same time. When the probe has to be replaced, keep the twin and its measurement rows and connect the new probe's decoded fields to them. Retained history stays available for as long as your plan's retention period allows.

## If readings do not arrive

| What you see | What to check |
| --- | --- |
| Save fails | Whether every required identity and profile field is filled, whether you may edit devices, whether your plan allows it, and whether another device already uses the identifier. |
| The sensor never joins or sends an uplink | Gateway reception, the regional band, the EUI and AppKey, power to the hardware, and the manufacturer's join procedure. |
| Uplinks arrive, but some fields are missing | Whether the codec fits, the firmware version, and the keys the decoder really produces. |
| Values show up but there is no history | Saved key mappings, template types that fit, and a new uplink after saving. |
| An unexpected missing-data status | The sensor's real reporting schedule against the Data sending interval you set. Command execution has its own last-seen check. |

Continue with [device diagnostics](connection-diagnostics.md) for reception status and processing errors.
