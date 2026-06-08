---
description: Catch trouble fast with leak, door, garage, and freezer automations that alert the moment something looks wrong.
---

# Safety and Alerting

When it comes to safety, speed matters. These automations are designed to react immediately when something is wrong — a water leak, an unexpected door opening, or a sensor reading that should not be where it is. They use simple, direct logic because in a safety scenario, fewer steps mean faster response.

Each example below uses a **Set Alarm** node that triggers an existing Alarm Definition. If you have not created any alarm definitions yet, head over to the [Alerts](../../alarm/) section first — that is where you configure severity, notification channels, and escalation steps.

---

## Basement Water Leak Detection

**Goal:** Get an immediate alert the moment a water leak sensor detects moisture above the dry baseline.

**Sensors needed:** A water leak sensor (or moisture sensor) in the basement.

Water leak sensors typically report a value near zero when dry and spike sharply when water is present. This automation triggers as soon as the reading crosses the threshold — no waiting, no averaging.

### Workflow

```
Start Event (Basement Leak Sensor)
       |
  Exclusive Gateway
      / \
     /   \
 [Leak]  [Dry - Default]
    |        |
 Set Alarm  End Event
 ("Water    ("No water detected")
  leak!")
    |
 End Event
```

### Gateway Condition

| Flow | Condition | Label |
|---|---|---|
| Flow 1 | `vars.value > 10` | Leak detected |
| Flow 2 | *(default)* | Dry |

Adjust the threshold based on your specific sensor. Some leak sensors report binary (0 or 1), in which case the condition would be `vars.value == 1` or `vars.value > 0`.

### Alarm Motivation Message

```cel
"Water detected in the basement — sensor reading: " + string(vars.value) + ". Check for leaks immediately."
```

### Why This Works

This is the simplest possible automation — sensor reading in, threshold check, alarm out. For water leaks, simplicity is the point. You do not want extra nodes, enrichment steps, or classification logic between the detection and the alert. Every millisecond matters when water is spreading.

### Customization Ideas

- Use a **Critical** severity alarm definition so the notification cuts through any quiet hours
- Place multiple leak sensors (under the water heater, near the washing machine, by the sump pump) and create one automation per sensor with a location-specific message
- Consider adding a second leak sensor as an enrichment check if you want to reduce false positives — but for most home setups, a single sensor with a direct alert is the right approach

---

## Front Door Opened After Midnight

**Goal:** Get notified when the front door opens during nighttime hours, when nobody should be coming or going.

**Sensors needed:** A door open/close sensor on the front door.

This automation uses the **schedule** feature on the Start Event to restrict when it runs, rather than checking the time inside the logic. The automation only evaluates sensor readings during the overnight window — during the day, it does nothing.

### Workflow

```
Start Event (Front Door Sensor, Schedule: 00:00 - 06:00)
       |
  Exclusive Gateway
      / \
     /   \
 [Open]  [Closed - Default]
    |        |
 Set Alarm  End Event
 ("Door     ("Door is closed")
  opened!")
    |
 End Event
```

### Start Event Configuration

| Field | Value |
|---|---|
| **Device** | Front door sensor |
| **Sensor** | Door status sensor |
| **Enable Schedule** | On |
| **Time Range** | `0:00 - 6:00` (or choose the range that fits your household) |
| **Time Zone** | Your local time zone |

### Gateway Condition

| Flow | Condition | Label |
|---|---|---|
| Flow 1 | `vars.value == 1` | Door opened |
| Flow 2 | *(default)* | Door closed |

The exact condition depends on how your door sensor reports. Common patterns:

- `vars.value == 1` — sensor reports 1 for open, 0 for closed
- `vars.value == "open"` — sensor reports a string status
- `vars.value > 0` — any non-zero value means open

Check your sensor's data in the Chirp dashboard to see what values it reports.

### Alarm Motivation Message

```cel
"Front door was opened after midnight — sensor reading at " + string(vars.value)
```

### Customization Ideas

- Extend the schedule to cover your preferred "quiet hours" — for example, `22:00 - 07:00`
- Create similar automations for back doors, garage side doors, or windows
- Use a **High** or **Critical** severity alarm definition so the notification is impossible to miss

---

## Garage Door Left Open

**Goal:** Get alerted when the garage door sensor reports an open state, so you never accidentally leave it open overnight or when you leave the house.

**Sensors needed:** A garage door sensor (open/close or tilt sensor).

### Workflow

```
Start Event (Garage Door Sensor)
       |
  Exclusive Gateway
      / \
     /   \
 [Open]  [Closed - Default]
    |        |
 Set Alarm  End Event
 ("Garage   ("Garage secure")
  door
  open!")
    |
 End Event
```

### Gateway Condition

| Flow | Condition | Label |
|---|---|---|
| Flow 1 | `vars.value == "open"` | Door is open |
| Flow 2 | *(default)* | Door is closed |

Adjust the condition based on your sensor. Tilt sensors might report an angle value, in which case the condition could be `vars.value > 45` (more than 45 degrees from vertical means the door is raised).

### Alarm Motivation Message

```cel
"Garage door is open — current status: " + string(vars.value)
```

### Customization Ideas

- Add a schedule so this automation only alerts during certain hours (nighttime, when you are typically away)
- Use a **Medium** severity alarm for daytime (you might be loading the car) and create a separate automation with **High** severity for nighttime
- If you have a multi-car garage with separate sensors, create one automation per door with clear labels in the motivation message

---

## Freezer Temperature Spike

**Goal:** Catch a freezer malfunction before food spoils by alerting when the temperature rises above the safe range.

**Sensors needed:** A temperature sensor inside the freezer.

Freezers should stay at or below -18 degrees Celsius. A rising temperature could mean the door was left ajar, the compressor is failing, or there was a power interruption.

### Workflow

```
Start Event (Freezer Temp Sensor)
       |
  Exclusive Gateway
      / \
     /   \
 [Warming] [Safe - Default]
    |          |
 Set Alarm   End Event
 ("Freezer   ("Freezer OK")
  warming!")
    |
 End Event
```

### Gateway Condition

| Flow | Condition | Label |
|---|---|---|
| Flow 1 | `vars.value > -15` | Temperature rising |
| Flow 2 | *(default)* | Safe range |

The threshold of -15 gives you a buffer before food reaches the danger zone at -18 — catching the trend while there is still time to act.

### Alarm Motivation Message

```cel
"Freezer temperature is " + string(vars.value) + " degrees — above the -15 degree warning threshold. Check the door and compressor."
```

### Customization Ideas

- Add a second, more urgent threshold at -10 degrees with a Critical alarm definition
- Use the same pattern for a refrigerator (threshold around 7-8 degrees Celsius)
- If you have a standalone chest freezer in the garage, the message can specify the location

---

## Tips for Safety Automations

- **Keep the logic short and direct.** The fewer nodes between the sensor reading and the alarm, the faster the response. Safety automations should not have complex branching or multiple enrichment steps unless absolutely necessary.
- **Use the highest appropriate severity level.** A water leak should be Critical. A garage door left open at 2 PM might be Medium. Match the severity to the urgency so your household knows how to react.
- **Test with a real trigger when possible.** Open the door, splash a little water near the leak sensor, or warm the temperature probe briefly. Seeing the full chain work — sensor to automation to notification — gives you confidence the safety net is real.
- **Do not over-automate safety.** One automation per hazard scenario is usually enough. If you build complex multi-step safety logic, you increase the chance that something in the chain fails silently.
- **Review safety automations periodically.** Check that the sensors are still online, the alarm definitions are active, and the notification channels are working. A safety automation is only as reliable as the weakest link in the chain.
