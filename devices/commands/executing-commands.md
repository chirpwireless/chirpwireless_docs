---
description: Send a command to a smart home device from the States tab in Chirp, fill in any values, and see whether it worked in your activity history.
---

# Sending a command

Once a device has commands set up, the **States** part of the **Commands & States** tab is your remote control. It shows what you can do, lets you do it, and keeps a tidy record of everything you've sent.

## What you can do

The **Available commands** list shows every action set up for the device — its name, what it does, how many inputs it needs, and a **Execute** button to run it. If the list is empty, the device doesn't have any commands yet; pop over to the **Commands** part to set one up (see [Setting up a command](creating-commands.md)).

## Pressing the button

Tap **Execute** next to a command.

* If it doesn't need any inputs, just confirm and it's on its way.
* If it does — say, a brightness level — fill in the **value**. Chirp shows the allowed range (like `Min: 0 - Max: 100`) and won't let you send something the device can't handle.
* Tap **Execute** to send, or **Cancel** to change your mind.

## If the device is offline

If Chirp hasn't heard from the device recently, you'll see a note at the top saying it's offline and when it was last seen. You can't send a command to a sleeping device on the spot — but anything you've queued will be sent automatically the moment it wakes up and reconnects, so nothing gets lost.

## Your activity history

Everything you send is listed in **Recent executions**, so you always have a record of what happened:

* **Command** — what you ran
* **Started** — when you sent it
* **Updated** — when its status last changed
* **Status** — how it turned out
* **Details** — a plain-language note

A command's status will be one of:

* **Pending** — on its way.
* **Confirmed** — done, and (if you set up a check) the device's reading matched.
* **Soft warning** — it was sent and received, but Chirp couldn't confirm the result in time. Often it worked anyway — just worth a peek.
* **Failed** — it didn't go through. The **Details** note tells you why.

## Control from your dashboard

For everyday use, you don't even need to open the device. Add a [Control widget](../../dashboards/adding-widgets/control-widget.md) to a dashboard and you'll have a light switch or button sitting right next to your readings — same actions, same history, one tap away.

## See also

* [Setting up a command](creating-commands.md)
* [Making sure it worked](verification.md)
* [Control widget](../../dashboards/adding-widgets/control-widget.md)
