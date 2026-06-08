---
description: Tell Chirp how to confirm a command really worked — skip the check, wait for the next reading, or ask the device.
---

# Making sure it worked

Pressing "Turn on" is satisfying — but did the light actually come on? Sometimes a device is asleep, out of range, or just doesn't get the message. Chirp can check for you, so a command is only marked as done when there's real proof behind it.

You set this up when you create a command, in the fourth step. There are three choices.

## Don't check

Send it and move on. Chirp won't verify anything.

With this option, the command shows as done the moment it's sent on its way — *not* when the device actually does something. It's fine for harmless, everyday actions where it doesn't matter much if one tap is missed, but don't rely on it when you really need to know something changed.

## Wait for the next reading

After the command goes out, Chirp waits for the device's next normal update and checks whether it reflects the change you asked for. When the reading matches, the command is confirmed.

This works nicely for devices that report their status as part of their regular updates — like a plug that tells Chirp whether it's currently on.

## Ask the device

The most thorough choice. After the device confirms it received the command, Chirp sends a quick follow-up question and checks the answer.

* **Follow-up command** — pick a command to use as the question, or create one right there. A follow-up question is a simple kind of command: it just asks the device for its current state, so there's nothing to fill in when it runs, and it needs no checking of its own — the device's answer *is* the check. Once saved, it's kept for reuse with any other command.
* When you create one, you write the short message that asks the device. For sensors on a cloud or external connection, you can send that message exactly as you wrote it, or let Chirp encode it first.
* Chirp matches the device's answer against what you expect to see.

Use this for devices that don't mention their status on their own but will tell you if you ask.

## What "worked" looks like

For both checking options, you tell Chirp what a successful result looks like by adding one or more expected readings:

* **Reading** — choose one of the device's measurements.
* **Expected value** — either a fixed value, or a reference to one of your inputs (so "set brightness to 60" checks that the device now reports brightness 60).

## How long to wait

Chirp waits a little while for the device to catch up before deciding.

* Leave the wait time empty to use the sensible default (about 1.5 times how often the device normally reports).
* If the time runs out without a match, the command is marked **Soft warning** instead of failed — meaning "we couldn't confirm it," not "it definitely didn't work." Often it did; it's just worth a glance.

## Quick guide

| Choice | Confirms | Good for |
| --- | --- | --- |
| Don't check | Only that it was sent | Simple, low-stakes taps |
| Wait for the next reading | The device's next normal update | Devices that report their status regularly |
| Ask the device | A direct answer from the device | Devices that respond when asked |

Next: [Sending a command](executing-commands.md).
