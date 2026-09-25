---
description: Set up on and off commands for a smart lamp from start to finish, and have Chirp confirm the lamp really switched.
---

# Example: Switching a Lamp On and Off

This walks through two commands on one device and gets Chirp confirming they worked. It uses an MQTT-connected Zigbee2MQTT lamp whose state messages contain `state: "ON"` or `state: "OFF"`. Check the payload your own lamp supports before using this example.

Do the parts in order; each one gives you something the next part needs.

## Before you start

* The lamp is already added and sending updates.
* You can see its readings in the device's **Mapping** section.

## 1. Find out how the lamp says "on"

Open the lamp and go to **Mapping**. Look down the list of fields for the one that reports whether it's lit, and note two things: what the field is called, and what it says right now.

For this lamp:

| Field | Right now |
| --- | --- |
| `state` | `OFF` |

That's the value a check will be looking for later, so copy it down exactly as it appears — `OFF`, not the Boolean `false`.

If the field hasn't been mapped to a measurement yet, do that now. Commands pick their readings by measurement name, so an unmapped field can't be used to check anything. See [What Your Device Is Sending](../what-your-device-is-sending.md).

In this example `state` is mapped to a String measurement called **Lamp state**.

## 2. Set up "Turn on"

Open **Commands & States → Commands** and tap **Add new command**.

**1. Name it**

* **Command name** — `Turn on`

**2. Point it at your device**

* For an external broker with the default Zigbee2MQTT base topic, set **MQTT topic** to `zigbee2mqtt/living-room-lamp/set`. Replace the friendly name with your lamp's exact name. For Cloud MQTT, use the displayed prefix and the matching topic suffix.

**3. What the command does**

Leave parameters empty, select **Send as-is**, and enter `{"state": "ON"}` as **Direct payload**. This mode does not use an encoder, so there is no encoder preview to run.

**4. Decide how Chirp checks it worked**

Pick **Wait for next uplink** — the lamp mentions its state in every normal update, so there's no need to go asking.

Under the expected readings, add one:

* **Metric** — *Lamp state*
* **Expected value** — `ON`

Use the String value `ON`, matching this lamp's reported state. See [Making sure it worked](verification.md#what-to-type-as-the-expected-value).

Tap **Save**.

## 3. Set up "Turn off"

Same again, with three changes:

* **Command name** — `Turn off`
* **Direct payload** — `{"state": "OFF"}`
* **Expected value** — `OFF`

Everything else stays as it was.

## 4. Try them out

Go to the **States** tab, find **Turn on**, and tap **Execute**.

Watch it appear in the recent list:

1. It sits at **Pending** while the message is on its way.
2. When the lamp's next update arrives saying `state: ON`, it turns **Confirmed** — Chirp has seen the lamp in the state you asked for.

Run **Turn off** and you'll see the same thing the other way round.

## If it never confirms

A command that isn't confirmed before the wait runs out shows as **Soft warning** — it went out, but Chirp couldn't prove anything changed. Work down this list:

1. **Check the value.** Open Mapping and see what `state` says now. If the lamp switched but reports `1` rather than `ON`, your expected value needs to match that — and since anything you type counts as a word, point at an input set up as a number or true/false instead.
2. **Check the reading.** Make sure the measurement you picked is the one fed by `state`, and that it's mapped and getting updates.
3. **Check the wait.** The default is about 1.5 times how often the lamp normally reports. If that interval isn't set on the device, set it.
4. **Check the message.** Check the MQTT topic and JSON against the manufacturer's instructions. Trigger a fresh state report to check the mapping.

## What's next

* Put both commands on a dashboard so anyone at home can use them without opening the device.
* Let an automation switch the lamp for you — see [An Automation Runs a Command](../../rules-engine/reference/automation-runs-a-command.md).
