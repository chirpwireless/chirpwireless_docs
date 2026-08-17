---
description: Set up a device command in Chirp — name it, pick the device, add inputs like brightness, and test before you save.
---

# Setting up a command

A command is a saved action with a friendly name — "Turn on", "Set brightness", "Warm white" — that you create once and then use again and again. After it's set up, you (or anyone you share your home with) can run it without ever seeing the technical bits.

Open the device, go to the **Commands & States** tab, stay on the **Commands** part, and tap **Add new command**. The setup screen is split into four short steps.

<figure><img src="../../.gitbook/assets/device-command-editor.jpg" alt="The command setup screen with the name, where-to-send, and message steps"><figcaption></figcaption></figure>

## 1. Name it

* **Command name** — Required. Pick something you'll recognize at a glance, like `Turn on` or `Movie lighting`. Each command on a device needs its own name.
* **Description** — Optional. A quick note about what it does.

## 2. Point it at your device

This tells Chirp how to reach the device. What you see depends on how the device is connected.

### Devices on MQTT (most smart home gear)

* **MQTT topic** — The address the message is sent to.
  * On Chirp's hosted broker, the first part of the address (the prefix) is filled in for you; you add the rest, like `living-room-lamp/set`. Your device needs to be listening on the full address.
  * On your own broker, type the full topic exactly as your device expects it.
  * Keep it under 500 characters, leave out the `#` and `+` symbols, don't leave an empty gap between slashes, and don't start it with `iot/`, `external/` or `external-downlink/` — those are reserved.
* If another command already uses the same address, Chirp gives you a heads-up so two actions don't clash.

### Devices on LoRaWAN

* **fPort** — A number from **1 to 223** that tells the device which "channel" the message is for. Your device's manual will tell you which to use.
* **Confirmed downlink** — A switch: leave it **On** to have the network wait for the device to confirm it got the message, or **Off** to simply send and move on. Turn it **On** if you plan to pick *Ask the device* in step 4 — that check waits for the confirmation, so it can't be saved without one.
* LoRaWAN messages always go out as raw bytes, so they always go through a converter. The send-as-is option only applies to MQTT devices.

### Devices that can't be controlled

Some devices only ever report in — there's no way to send anything back to them, so they don't offer commands at all.

## 3. What the command does

This is where you set up any choices the command offers and the message it sends.

### Inputs (parameters)

If your command needs a value — a brightness level, a color temperature, a mode — add it as a **parameter** with **Add Parameter**. For each one:

* Give it a **Name** and a short **Description** (the description is what you'll see when you run the command).
* Pick a **Type**:
  * **Integer** or **Float** for numbers, with an optional smallest (**Min**), largest (**Max**), and starting (**Default**) value — great for a 0–100 brightness.
  * **String** for text, with an optional list of allowed choices (an **Enum** like `auto, manual, off`).
  * **Boolean** for a simple on/off or true/false.

Setting a Min and Max means you can never accidentally send a brightness of 500% — Chirp keeps the value sensible for you.

### The message itself

For MQTT devices, you choose how the message is built:

* **Send as-is** — send the message straight through (best when your device understands plain JSON).
* **Process with encoder** — run it through a small converter first.

When a converter is used (and it always is for LoRaWAN, where messages have to be turned into raw bytes), you write a short **template** with `{{ placeholders }}` that get filled in with your inputs — so a "set brightness" command drops the brightness number into the right spot. Most of the time the converter that came with your device's setup is all you need; advanced users can supply their own.

## 4. Decide how Chirp checks it worked

The last step is where you say whether Chirp should confirm the command actually did something — send and forget, wait for the device's next update, or ask the device outright. It's also where you pick which reading should change and what it should say.

It has a page of its own: [Making sure it worked](verification.md). To find out what your device reports back and how it writes it, see [What Your Device Is Sending](../what-your-device-is-sending.md).

## Test it before you save

Whenever a converter is involved, there's a **Try it** tool right in the setup screen. Put in some test values and run it to see exactly what will be sent — including the technical form of the message and whether it ran cleanly. It's a no-risk way to be sure the command is right *before* it ever reaches your device.

## Save

Tap **Save**. The command shows up straight away in your list of commands and on the **States** tab, ready to use. You can **Edit** it later, or **Delete** it if you no longer need it.

## What's next

* Decide how Chirp confirms the command worked — [Making sure it worked](verification.md).
* Actually press the button — [Sending a command](executing-commands.md).
