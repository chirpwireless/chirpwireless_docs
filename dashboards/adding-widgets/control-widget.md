# Control widget

Every other widget *shows* you something. The **Control widget** lets you *do* something. It puts a **switch** or a **button** right on your dashboard, so you can turn a device on or off — or run any action you've set up for it — without leaving the screen you're already looking at. It's the dashboard version of [Controlling Your Devices](../../devices/commands/): the command does the work, the widget is the switch on the wall.

Connect it to a sensor that reports the device's state, and the switch even keeps itself up to date — it shows *on* when the device is actually on, and flips when you tap it. The control and the status light are the same thing.

## Before you add one

A Control widget needs a device that already has a command set up on its **Commands & States** tab — a "Turn on", a "Set brightness", that sort of thing. Devices with no commands won't show up to choose from (you'll see *"No controllable devices in this organization"*). Set the command up first; see [Setting up a command](../../devices/commands/creating-commands.md).

## Adding a Control widget

In dashboard edit mode, pick **Control** from the widget picker. The settings panel has two tabs: **Datasource** and **Appearance**.

### Datasource

Titled **"Control configuration."**

* Choose the device you want to control — only controllable devices appear.
* Pick the **sensor that tells the widget the current state** (for example, a reading that says whether the device is on or off). The first sensible one is chosen for you; change it if you'd like.

Tap **Next**.

### Appearance

Headed **"Add Control widget."**

* **Widget name** *(required)* — the label on your dashboard.
* **Description** — optional.
* **Widget type** — how the control looks:
  * **Switch** — a flip toggle, perfect for on/off things like a plug or a light.
  * **Button** — a press control, nice for a single action.
* **The states** — this is where you connect the control to what it does:
  * **Label** — what to call the state ("On", "Off").
  * **Command** *(required)* — which of the device's commands this state runs.
  * **Expected value** *(required)* — what the status sensor reads when the device is in this state, so the switch knows when to show as on. Chirp fills this in for you where it can — adjust it if your device reports something different.
  * If the command has any inputs (like a brightness number), set them here too.

  A switch connects an "on" and an "off"; a button connects the one action it sends.
* **Looks** — choose the on, off, and unavailable **colors**, show or hide the **labels** (switch), pick a **button size** of S, M, or L (button), and choose whether to show the widget's **name and last update**.

Tap **Save** to drop it on your dashboard.

## How it behaves

* **Tap to control.** Tapping the switch or button sends the command the same way the device's States tab does — same checks, same history.
* **Stays in sync.** It watches the status sensor and shows the real state, so it's never just guessing based on your last tap.
* **Greys out when it can't.** If the device is offline or a state isn't fully set up, the control is shown unavailable rather than sending a command into thin air.

## See also

* [Controlling Your Devices](../../devices/commands/) — set up the commands this widget uses
* [Setting up a command](../../devices/commands/creating-commands.md)
* [Sending a command](../../devices/commands/executing-commands.md) — where every tap is recorded
