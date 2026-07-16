---
description: Added a sensor but no readings appear? Read the Connection tab and get your data flowing.
---

# Connection Diagnostics

You unboxed the sensor, stuck it on the wall, typed in its numbers, hit **Save** — and the readings are still blank. It's the moment every home setup runs into at least once, and it used to leave you guessing whether the problem was the battery, the gateway, the keys, or Chirp itself.

Connection diagnostics answers that question for you. Open any sensor, go to its **Connection** tab, and Chirp tells you in plain words where your sensor's data is right now: whether anything has arrived at all, whether Chirp understood it, and whether it's being saved to your history. Every state comes with a short list of things to try — so you always know what to do next, not just what went wrong.

## Why this is worth two minutes of your time

Without it, a silent sensor is a mystery with a dozen possible causes. Is the wine cellar monitor out of range? Did you mistype one character of a 16-character code? Is it sending fine and just not being recorded? Those are wildly different problems with wildly different fixes, and hunting through them one at a time is how a fifteen-minute setup turns into a lost evening.

The Connection tab collapses all of that into one screen. It tells you which of those three things is actually happening, and then it tells you which one to fix. Most of the time you'll be done before you've finished your coffee.

## Where to find it

1. Click **Devices** in the sidebar.
2. Click the sensor you're worried about to open its detail dialog.
3. Click the **Connection** tab.

Diagnostics appear right there alongside the sensor's connection settings. Three blocks stack down the tab:

- **Reception status** — the headline: is data arriving, and is it being kept?
- **Pipeline** — the counts, showing how many messages made it through each stage recently.
- **Event feed** — the message-by-message diary, newest first.

## Block 1 — Reception status

This is the one to read first. It's a single sentence that names your situation, with a supporting line underneath and a couple of numbers for context.

You'll see one of these headlines:

| Headline | What's actually happening |
|---|---|
| **Receiving & storing** | The happy ending. Data is arriving, Chirp understands it, and your history is filling up. The line beside it reads `{{count}} sensors mapped · last value {{last}}`. |
| **Sending data — set up mapping to keep it** | Your sensor is alive and talking — Chirp just doesn't know what its readings mean yet, so nothing is being saved. Shown as `{{count}} keys decoded · none mapped yet`. |
| **Data arrives but nothing is stored** | "Data is arriving but nothing is stored yet." Messages are landing, but none of them are turning into readings you can chart. |
| **Hasn't reported — device looks offline** | "Device was reporting but has gone quiet." It used to work. Something changed. |
| **Waiting for first data** | Nothing has come in yet. You may also see **Waiting for the first uplink** or **No uplinks received yet** — same meaning. If it never moves off this state, the sensor may still be joined to a network it used before Chirp — see [First things first: joining the network](#first-things-first-joining-the-network). |
| **Reached network — waiting for data** | "Joined the network · no uplinks yet" — a LoRaWAN sensor that has successfully introduced itself to your gateway but hasn't sent an actual reading yet. Genuinely good news. |

Around the headline you'll also spot a few supporting details:

- **Expected every {{interval}} {{unit}} · last seen {{last}}** — the schedule you told Chirp this sensor is on, next to when it actually last showed up. If those two disagree badly, the schedule in your settings is probably wrong, not the sensor.
- **{{count}} sensors configured · 0 receiving values** — you've set up readings, but none of them are being filled in.
- **{{count}} more keys available, unmapped** — your sensor is sending extra readings you haven't claimed yet. Often a pleasant surprise: a leak detector quietly reporting its battery level too.
- **LIVE**, **NO DATA**, **Live**, **Idle**, **RECEPTION** — small indicators marking whether things are moving right now.
- **Loading reception status…** — just fetching. Give it a second.
- **Diagnostics unavailable** — the check itself couldn't run. Close the dialog, reopen the sensor, and try the Connection tab again.

### The two guidance blocks

Right beside the status you'll find **WHAT TO CHECK** and **WHILE YOU WAIT** — short, concrete checklists that change depending on what's going on. They're the whole point of the page, so don't skim past them.

For a sensor that hasn't shown up, they'll suggest things like:

- Confirm the device is powered on and transmitting
- Check the device power or battery
- Make sure it is within range of a gateway
- Check that AppKey and DevEUI match the device
- Give it one reporting interval to transmit

For a sensor that has gone quiet after working fine:

- Check the device power or battery
- Confirm it is still within range of a gateway
- Confirm the device is sending on its schedule
- Make sure the sending schedule has not changed

For data arriving that isn't turning into readings:

- Check the payload decoder matches this device
- Map at least one incoming key to a sensor
- Check that the connection settings are correct

### If your sensor connects over MQTT

MQTT sensors have their own set of messages, because there's a broker in the middle:

| Message | What it means and what to do |
|---|---|
| **Broker connected** — "Your broker is reachable and Chirp is subscribed" | All good on the broker side. |
| **Connecting to your broker…** | Chirp is dialing in. Wait a moment. |
| **Chirp can't reach your broker** | "Check the broker URL and credentials in the connector settings." Open the connector and re-copy the address, username, and password — a stray space at the end of a pasted password is the classic culprit. |
| **Waiting for the device to publish to the Chirp broker…** | Connection's fine, the device just hasn't said anything yet. It is connected with its generated MQTT credentials. |
| **A message arrived on a topic this device isn't set up for** | "Update the topic above, or change where the device publishes." Compare the **Expected topic** field with **Published to** — they need to line up. |
| **No publish topic is configured yet — set one above.** | Fill in the topic field on this tab, save, and the messages will start matching. |

When things are working, MQTT diagnostics confirm all three of these: the device publishes to the expected topic, the payload is valid JSON, and the device ID resolves as configured.

## First things first: joining the network

There's a step people miss because nothing in the setup form hints at it. A LoRaWAN sensor doesn't simply start broadcasting readings the moment it has power. It has to **join** a network first.

Here's how that goes. When the sensor wakes up, it sends out a **join request** — a little "hello, may I?" message carrying its identity. Your gateway passes it along, Chirp checks it against the Device EUI and AppKey you typed into the sensor form, and if those match, Chirp sends back a join accept. Only *after* that handshake does the sensor start sending actual readings.

Which is why the states at the top of this tab read the way they do. They're that handshake, in order:

1. **Waiting for first data** — the handshake hasn't happened. Chirp has heard nothing from this sensor at all.
2. **Reached network — waiting for data** (shown as "Joined the network · no uplinks yet") — the handshake worked. The sensor is on your network, it just hasn't reached its next scheduled report.
3. **Receiving & storing** — readings are flowing in and going into your history.

### A sensor can only belong to one network at a time

Here's the part that trips people up. Once a sensor joins a network, it settles in and stops asking. Its firmware is satisfied: it has a network, thank you, no need to knock on any more doors.

So if your sensor has had a previous life — you found it on eBay, it was already screwed to the wall when you bought the house, it came off a different app or platform, or it's a returned or demo unit that someone else set up first — it is still, as far as it's concerned, joined to that old network. Adding it to Chirp doesn't undo that. You've told Chirp all about the sensor, but nobody has told the sensor about Chirp, and it isn't going to ask.

The symptom is unmistakable once you know it: **Waiting for first data**, indefinitely, while every single thing you can check looks right. EUI correct. AppKey correct. Battery in. Sitting a meter from the gateway. Three reporting intervals have come and gone. Nothing. That's not a mistake you can find by checking harder — the sensor is simply talking to somewhere else.

Worth saying plainly: Chirp can only report on what reaches it. It has no way to see that your sensor is quietly still attached to a previous owner's network, so it can't warn you about this one. That's what this section is for.

### The fix: make it ask again

Reset the sensor. A reset clears the old session and puts the sensor back to square one, where it sends a fresh join request — and this time your Device EUI and AppKey are waiting for it in Chirp.

How you do that depends entirely on who made it. There's no universal button. Depending on the model it might be:

- a magnet swiped past a specific spot on the casing
- a button held down for a set number of seconds
- a reed switch or a pinhole reset under the cover
- a power cycle of a particular length, or repeated a particular number of times

Look up the reset procedure for your exact model in the manufacturer's instructions — it's usually in the quick-start leaflet or on the maker's support page. One detail worth watching for: plenty of sensors treat "restart" and "rejoin" as two different things. Pulling the battery for a second may just restart it, leaving the old network session intact, and it'll come back exactly as silent as before. You want the full reset that clears the session.

Once it's done, watch the Connection tab. You should see the status move to **Reached network — waiting for data** within a minute or two — that's the join accept landing. From there it's just waiting for the sensor's next report.

### Two lookalikes that aren't this

- **A sensor that worked for a while and then went quiet** is a different problem. Sensors don't quietly un-join a network on their own, so this isn't it. That case shows up as **Hasn't reported — device looks offline**, and it's almost always the battery, something new blocking the signal, or a schedule that's changed. Don't reset it — you'll just make more work for yourself.
- **A sensor that joins, then drops back to "Waiting for first data" again and again** usually has a typo in its identifiers. One wrong character in the Device EUI or AppKey and the handshake can't complete. Re-enter both with **Scan QR code** on the sensor form rather than retyping — then reset the sensor once more so it tries again with the corrected values.

## Block 2 — Pipeline

The Pipeline block counts how many messages made it through each stage: **Routed**, **Mapped**, and **Stored**. Reading it left to right shows you exactly where things stop.

If Routed is climbing but Stored is stuck at zero, your sensor is talking and Chirp is listening — the readings just aren't being recorded, which almost always means mapping. If Routed itself is zero, nothing is reaching Chirp at all, and the problem is out at the sensor, the battery, or the gateway.

One thing worth knowing: these counts are labeled **Stats over the last {{days}} days**. They cover a recent rolling window — the number of days shown in that label — not everything the sensor has ever sent. A brand-new zero doesn't mean the sensor never worked; it means it hasn't done anything within that window.

## Block 3 — Event feed

Where the Pipeline gives you totals, the event feed gives you the individual messages. It's a table:

| Column | What it shows |
|---|---|
| **Time** | When the message arrived |
| **Stage** | Which step of the journey this row describes |
| **Outcome** | How that step turned out |
| **Detail** | The specifics — helpful when the outcome isn't OK |

Below the table, a legend titled **What these statuses mean** spells out every term. Here it is:

| Term | Meaning |
|---|---|
| **Routed** | the message reached the platform and was matched to this device. |
| **Mapped** | incoming keys were matched to your configured sensors. |
| **Stored** | sensor values were saved to history. |
| **OK** | this step completed successfully. |
| **Skipped** | intentionally not processed (for example, no matching mapping or an unexpected topic). Not necessarily an error. |
| **Error** | this step failed and needs attention. |

That **Skipped** row deserves a moment. Seeing it doesn't mean anything is broken — it usually just means a reading arrived that you haven't asked Chirp to keep. If you'd like to keep it, map it (see below). If you don't care about it, leave it alone; Skipped is a perfectly healthy thing to see.

If the sensor is brand new you'll see **No events yet** with "Events will appear here once the device sends data." — nothing to fix, just nothing to show.

The feed loads a chunk at a time. Click **Load more** to fetch older entries; you'll see **Loading…** briefly and **All records loaded** once you've reached the end. **No pipeline data** means there's nothing recorded for this sensor in the window at all.

## What "mapping" actually means

Half the messages on this page mention mapping, so it's worth a plain-language explanation.

Your sensor doesn't send tidy labels. A garden soil probe might send something like `sm` and `bat` — not "Soil Moisture" and "Battery." Mapping is you telling Chirp: *that `sm` number is the soil moisture reading, in percent.* Once you've done that, Chirp knows what the number is, stores it in your history, draws it on your dashboard, and lets your automations react to it.

Until you map at least one reading, Chirp receives your sensor's messages and politely sets them aside, because it has no idea what they represent. That's exactly the **Sending data — set up mapping to keep it** state — and it's the single most common reason a healthy sensor shows no readings.

Good news: **Connector keys appear here automatically once the device transmits.** You don't have to know your sensor's field names in advance. Let it send once, and the list fills itself in.

## Fixing things without leaving the tab

Diagnostics don't just describe problems — they hand you the button. Depending on the situation you'll see:

- **Fix** / **Fix mapping** / **Set up mapping** / **Map a key** — jump straight to where you match your sensor's readings to what you want to see. This is the fix for anything mapping-related.
- **Details** — expand a row to see the full story behind an outcome.
- **Hide** — collapse a block once you've read it, to get the Connection tab back to a working size.
- **See reception status** — jump back up to the headline from further down the tab.

## What to do when it says…

**"Waiting for first data" / "No uplinks received yet"** — Give it one full reporting interval before doing anything; a sensor set to report once an hour will look silent for an hour, and that's correct. If it stays silent past that, check the battery is in the right way round, confirm the sensor is within range of your gateway, and double-check the Device EUI and AppKey character by character against the sensor's label. If typing them was the risky part, re-enter them with **Scan QR code** on the sensor form — see [Adding Sensors](adding-sensors.md). And if all of that checks out and it's *still* silent, stop checking and reset the sensor so it sends a fresh join request — this is the usual ending for any sensor that had an owner before you. See [First things first: joining the network](#first-things-first-joining-the-network).

**"Reached network — waiting for data"** — Relax. Your LoRaWAN sensor found the gateway and joined successfully, which is the hard part. It's simply waiting for its next scheduled report. Come back after one interval.

**"Sending data — set up mapping to keep it"** — This is the best kind of problem: everything works, you just need to claim the readings. Click **Set up mapping** (or **Map a key**), pick the readings you want from the list that's now populated, save, and your history starts filling from the next report onward.

**"Data arrives but nothing is stored"** — Messages are landing but not becoming readings. Check the payload decoder matches this device — a template meant for a different model will produce nothing useful — and make sure at least one incoming key is mapped to a sensor. Both live on this same dialog.

**"Hasn't reported — device looks offline"** — It worked before, so start with the physical world: battery first, then range. A wine cellar monitor that stopped reporting the same week you rearranged the shelves is probably behind something now. Also confirm the sending schedule hasn't changed — if you reconfigured the sensor to report daily but Chirp still expects hourly, it'll look offline while being perfectly fine. Fix the **Data sending interval** on this tab to match reality.

**"Chirp can't reach your broker"** — MQTT only. Open the connector settings and recheck the broker URL and credentials. See [MQTT Troubleshooting](../connectors/mqtt/troubleshooting.md).

**"A message arrived on a topic this device isn't set up for"** — MQTT only. Compare **Expected topic** with **Published to**. Either update the topic here to match what your device actually sends, or reconfigure the device to publish where Chirp is listening. Either works — pick whichever is easier to change.

**"Diagnostics unavailable"** — The check couldn't complete. Reopen the sensor and try again. Your data isn't affected either way — this only concerns the diagnostic view.

## Checking the connector, not just the sensor

Sometimes the sensor is fine and the connection itself is the issue. MQTT connectors have their own **Connector diagnostics** area with **Source health**, **Incoming**, and **Activity** tabs, showing whether the connector is receiving anything at all ("{{count}} seen", or **No activity yet** when it isn't), a **Connect device** shortcut, and its own **Diagnostics unavailable** state when the check can't run. Other connection types simply show their settings.

If every one of your MQTT sensors looks silent, start at the connector rather than the sensors. See [MQTT Troubleshooting](../connectors/mqtt/troubleshooting.md).

## Tips

- **Read top to bottom, fix bottom to top.** The reception status names the problem, the pipeline shows where it stops, the event feed proves it. But the fix almost always sits at the earliest stage that isn't OK.
- **Get the reporting interval right first.** More "offline" sensors are misconfigured schedules than dead batteries. A monthly water meter set to an hourly interval will look broken 720 times a month.
- **Don't panic at Skipped.** It's informational. Errors are the ones that want attention.
- **Take the free readings.** When you see "{{count}} more keys available, unmapped", have a look — battery level is often sitting there unclaimed, and it's the reading that warns you before a sensor goes quiet.
- **Check here before replacing hardware.** A sensor that says "Sending data — set up mapping to keep it" is a working sensor. Nothing on it needs replacing.

## What's next

- [Adding Sensors](adding-sensors.md) — register a sensor and map its readings.
- [Sensor Details](sensor-details.md) — the rest of the sensor dialog, including Logs.
- [MQTT Troubleshooting](../connectors/mqtt/troubleshooting.md) — broker-side problems in depth.
