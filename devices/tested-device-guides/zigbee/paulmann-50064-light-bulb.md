# Paulmann 50064 light bulb

This is a hardware-specific walkthrough for the **Paulmann SmartHome LED spot, model 50064** — a Zigbee 3.0 CCT (tunable-white) bulb we tested end-to-end with Zigbee2MQTT and Chirp's MQTT connector. If you have this exact bulb, follow these steps to pair it, register it in Chirp, and map its readings.

If you have a **different Zigbee bulb or device**, you don't need this page — the generic flow applies. Pair the device through Z2M following your manufacturer's instructions, then [register it in Chirp](../../../connectors/mqtt/topics-and-device-routing.md) the same way as any other Z2M-bridged device. The Paulmann 50064 happens to be the bulb we had in hand for the testing — the procedure transfers cleanly to other Zigbee devices.

## What this bulb is

- **Type:** CCT (correlated color temperature) tunable-white LED. Adjusts brightness and color temperature, but not color (no RGB).
- **Color temperature range:** 150–500 mired (about 6667K daylight to 2000K candle-warm).
- **Power:** mains, screw-in fitting (varies by region — E14, E27, GU10 versions exist).
- **Zigbee profile:** Zigbee 3.0, identifies as `Paulmann SmartHome led spot (50064)` in Z2M.
- **Z2M auto-identifies it** — once paired, Z2M shows the brand and model in the Devices tab without manual selection.

What works:
- Brightness and color-temperature control via the Z2M web UI, MQTT `/set` commands, or any home-automation system that publishes to MQTT.
- State changes initiated via MQTT or the Z2M web UI generate confirmation publishes that flow through Chirp into the Mapping tab and Logs tab.

Behavioral quirk to know up front: **physical wall-switch toggles do not generate MQTT publishes** on this bulb. The bulb's firmware only reports state changes that arrived over Zigbee, not changes caused by mains power-cycling. If you flip a wall switch and then check the Logs tab, expect to see nothing new — that's the bulb's design, not a Chirp or Z2M bug. To verify state in Chirp during setup, drag the brightness slider in the Z2M web UI or send a `/get` poll. See [Troubleshooting](../../../connectors/mqtt/troubleshooting.md) for the full list of "what counts as a publish."

## Prerequisites

- Z2M is installed and running. If not, follow [Setting up Zigbee2MQTT](../../../connectors/mqtt/zigbee2mqtt.md) and the [Sonoff ZBDongle-E coordinator walkthrough](../../../gateways/zigbee2mqtt-hubs/sonoff-zbdongle-e-coordinator.md) (or the equivalent for your coordinator) before continuing here.
- The bulb is screwed in and the wall switch is in the **on** position. It's powered, even if it's currently lit on factory-default settings.
- The bulb is within ~2 meters of the coordinator for initial pairing. After joining, you can move it anywhere — Zigbee mesh routing handles range.

## Pairing

The Paulmann 50064 uses a 5-cycle reset pattern.

1. **Open Permit join in Z2M first.** In the Z2M web UI at `http://localhost:8080`, click the green shield icon at the top labeled **Permit join (All)**. The Zigbee network is now open for 180 seconds.
2. **Power-cycle the bulb 5 times.** Use the wall switch:
   - on → off → on → off → on → off → on → off → on → off
   - About 2 seconds in each state. Don't rush — too fast and the bulb may not register the cycle.
3. **On the 5th on-cycle, the bulb blinks rapidly.** This is the factory-reset confirmation. Pairing mode is now active.
4. **Stop. Leave the bulb on. Don't touch the switch.** This is the most common mistake — people see the blink and immediately do another off/on cycle, which restarts the reset sequence and aborts the join attempt.
5. **Wait 10–30 seconds.** The bulb joins the Zigbee network and appears in Z2M's Devices tab, identified by its IEEE address (`0x...`).
6. Z2M auto-identifies the model. The Devices tab shows `Paulmann SmartHome led spot (50064)` next to the device.

If pairing doesn't happen within ~60 seconds:

- The 180-second Permit join window may have closed. Click Permit join again.
- The bulb may already be paired to a previous Zigbee network (rare for new bulbs but possible if you bought it second-hand). Repeat the 5-cycle reset to factory-default it again.
- Some Paulmann firmware revisions require 10 cycles instead of 5. Try 10 if 5 doesn't trigger the blink.
- Move the bulb closer to the coordinator. 1–2 meters is the safest range for first pairing.

## Renaming the device

When the bulb pairs, its initial friendly name is its IEEE address. Rename it to something readable — that name will become the device-level MQTT topic Z2M publishes to AND the Device ID you'll use in Chirp.

In the Z2M web UI:
1. Click the bulb's row in the Devices tab.
2. Click the pencil icon next to the name at the top of the detail panel.
3. Type a new name. **Avoid spaces** — Chirp's Device ID input strips whitespace, which causes silent topic-match failures. Use CamelCase (`TableLampLivingRoom`) or snake_case (`table_lamp_living_room`).
4. Press Enter or click the checkmark.

The example friendly name we'll use in this page: **`TableLampLivingRoom`**.

After renaming, Z2M publishes to:
```
zigbee2mqtt/TableLampLivingRoom        (External MQTT)
{Topic prefix}/zigbee2mqtt/TableLampLivingRoom   (Cloud MQTT)
```

## What the bulb publishes

When the Paulmann 50064 sends a state update, the payload looks like this:

```json
{
  "brightness": 255,
  "color_mode": "color_temp",
  "color_temp": 392,
  "color_temp_startup": 65535,
  "linkquality": 212,
  "state": "ON"
}
```

Full field reference:

| Field | Type | Range | Notes |
|-------|------|-------|-------|
| `state` | string | `"ON"`, `"OFF"`, `"TOGGLE"` | **String, not boolean.** Map to a String-typed metric in Chirp. |
| `brightness` | integer | 0–254 | 0 turns the bulb off on some firmware versions. Note: 0–254, not 0–255 or 0–100. |
| `color_temp` | integer | 150–500 mired | See the Mirek-scale table below. |
| `color_temp_startup` | integer | 150–500, or 65535 | Color temperature applied on cold power-on. `65535` = "restore previous." |
| `power_on_behavior` | enum | `off`, `on`, `toggle`, `previous` | Behavior after a power loss. Send via `/set` to configure. |
| `effect` | enum | `blink`, `breathe`, `okay`, `channel_change`, `finish_effect`, `stop_effect` | One-shot effects. Send via `/set` to trigger. |
| `linkquality` | integer | 0–255 | Zigbee link quality. Diagnostic only — not user-facing. |
| `color_mode` | string | `"color_temp"` | **Always present in payloads even though it's not on the [zigbee2mqtt.io device page](https://www.zigbee2mqtt.io/devices/50064.html).** Trust the actual payload over the device page when they disagree. |

### Mirek scale (`color_temp` values)

The Mirek (or "mired") scale is the inverse of Kelvin: lower Mirek = cooler/bluer light, higher Mirek = warmer/more amber. The formula is mired = 1,000,000 / Kelvin.

Z2M ships named presets for the Paulmann 50064:

| Preset name | Mired | Approximate Kelvin | Description |
|-------------|-------|-------------------|-------------|
| coolest | 150 | 6667K | Daylight / blue-white |
| cool | 250 | 4000K | Natural white |
| neutral | 370 | 2703K | Warm white |
| warm | 454 | 2203K | Candle-like |
| warmest | 500 | 2000K | Very warm amber |

When you map `color_temp` in Chirp, choose a Number-typed metric. The unit is mired (lower = cooler).

## Registering the bulb in Chirp

Once Z2M is publishing to a topic Chirp can see (verify via the connector's **Last data received**), register the device:

1. **Connectors → your MQTT connector → Add device.**
2. **Device ID:** `TableLampLivingRoom` (or whatever whitespace-free friendly name you chose). It must match the Z2M friendly name byte-for-byte.
3. Open the **Mapping** tab. You land on the **Topic** sub-tab first.
4. **Topic sub-tab:**
   - **Device ID Topic:** `zigbee2mqtt/{{deviceId}}`
   - **Where to get the device ID:** `Topic` (default).
   - **Telemetry topics:** leave empty. The Paulmann publishes a flat JSON payload — Chirp parses all keys automatically.
5. Click **Next** or the inner **Mapping** sub-tab to reach the per-key rows.
6. **Mapping sub-tab — Pass 1:** add a row per metric you want, but **leave Connector key empty**. Recommended initial set:

   | Normalized key | Type | Data type |
   |---------------|------|-----------|
   | State | String | Reported State |
   | Brightness | Number | Reported State |
   | Color Temperature | Number | Reported State |
   | Color Mode | String | Telemetry |
   | Link Quality | Number | Telemetry |

   If a normalized key you want doesn't exist, use **+ Add new metric** and create one. The modal handles both the normalized name and the underlying sensor template.

7. Click **Save**.
8. **Generate a publish.** Open the bulb in the Z2M web UI and drag the brightness slider, or use the on/off toggle. Z2M sends a `/set` command, the bulb confirms the new state, and Z2M publishes the confirmed payload — that's the publish Chirp needs.
9. **Mapping sub-tab — Pass 2:** reopen the device record. The **Connector key** dropdowns now list the keys received from the bulb (`state`, `brightness`, `color_temp`, `color_mode`, `linkquality`). Match each row:

   | Mapping row | Connector key |
   |------------|--------------|
   | State | `state` |
   | Brightness | `brightness` |
   | Color Temperature | `color_temp` |
   | Color Mode | `color_mode` |
   | Link Quality | `linkquality` |

10. Click **Save** again.

After step 10, the **Value** column on the Mapping tab populates with the bulb's current state. Generate one more publish (drag the Z2M slider) to confirm a record arrives in the **Logs** tab — that's your end-to-end verification.

## Things that look like problems but aren't

- **Mapping tab Value column updates but Logs tab is empty.** Normal after Pass 2 if you saved Connector keys after the most recent publish. Generate a fresh publish from the Z2M web UI.
- **`color_mode` always shows `"color_temp"`.** This bulb has no RGB capability. The field is always `color_temp` for CCT bulbs.
- **`color_temp_startup` shows `65535`.** That's the "restore previous color temperature on power-on" sentinel value. Set a specific number via `/set` if you want a fixed color on cold power-on.
- **Multiple publishes from one `/get` request.** Z2M polls Zigbee attribute clusters separately, so one `/get` produces 2–4 publishes back as the cluster responses arrive. Normal — not an error.
- **Wall-switch toggle produces no Logs entry.** As covered above — this bulb doesn't publish on physical power-cycle. Use the Z2M web UI to generate publishes for setup-time verification.

## Where to go next

- [MQTT Troubleshooting](../../../connectors/mqtt/troubleshooting.md) — when something isn't working.
- [Topics and device routing](../../../connectors/mqtt/topics-and-device-routing.md) — the protocol-level reference for the registration concepts above.
- [Zigbee2MQTT setup](../../../connectors/mqtt/zigbee2mqtt.md) — to recheck the Z2M install or to pair another device.
