---
description: Build automations that keep rooms comfortable — temperature zones, garden moisture, and wine cellar climate alerts.
---

# Home Comfort and Energy

These automations help you keep your living spaces comfortable and catch issues before they become problems. Each example includes the workflow pattern, the CEL expressions, and suggestions for customization.

Every Set Alarm node in these examples triggers an existing Alarm Definition. Create your alarm definitions in the [Alerts](../../alarm/) section before building these automations — that is where you set severity levels, notification channels, and escalation behavior.

---

## Living Room Temperature Comfort Zone

**Goal:** Get notified when your living room temperature drifts outside the comfortable 18-24 degrees Celsius range.

**Sensors needed:** A temperature sensor in the living room.

### Workflow

```
Start Event (Living Room Temp Sensor)
       |
  Script Task ("Check comfort range")
       |
  Exclusive Gateway
     / | \
    /  |  \
[Cold] [Hot] [Comfortable - Default]
  |      |        |
Set    Set     End Event
Alarm  Alarm   ("All good")
("Too  ("Too
 cold") warm")
  |      |
End    End
Event  Event
```

### Script Task Expression

```cel
{"status": vars.value < 18 ? "cold" : vars.value > 24 ? "hot" : "comfortable"}
```

### Gateway Conditions

| Flow | Condition | Label |
|---|---|---|
| Flow 1 | `vars.status == "cold"` | Too cold |
| Flow 2 | `vars.status == "hot"` | Too warm |
| Flow 3 | *(default)* | Comfortable |

### Alarm Motivation Messages

For the "too cold" alarm:
```cel
"Living room is " + string(vars.value) + " degrees — below the 18-degree comfort minimum"
```

For the "too warm" alarm:
```cel
"Living room has reached " + string(vars.value) + " degrees — above the 24-degree comfort maximum"
```

### Customization Ideas

- Change the range to match your family's preferences (some people prefer 20-22 degrees)
- Add a third branch for "borderline" readings (17-18 or 24-25 degrees) that sends a less urgent notification
- Use the same pattern for a bedroom sensor with a narrower range for sleeping comfort

---

## Garden Soil Moisture Alert

**Goal:** Know when your garden soil is getting dry so you can water before plants are stressed.

**Sensors needed:** A soil moisture sensor in your garden bed.

### Workflow

```
Start Event (Garden Moisture Sensor)
       |
  Exclusive Gateway
      / \
     /   \
  [Dry]  [Moist - Default]
    |        |
 Set Alarm  End Event
 ("Water    ("Soil is fine")
  the
  garden")
    |
 End Event
```

### Gateway Condition

| Flow | Condition | Label |
|---|---|---|
| Flow 1 | `vars.value < 30` | Dry soil |
| Flow 2 | *(default)* | Moist enough |

This example skips the Script Task and puts the condition directly on the gateway — perfectly valid when you only need a single threshold check.

### Alarm Motivation Message

```cel
"Garden soil moisture is at " + string(vars.value) + "% — time to water"
```

### Customization Ideas

- Adjust the threshold based on your soil type and plants (succulents need less moisture than tomatoes)
- Add a second threshold at 15% for a more urgent "critical" alert with a different alarm definition
- If you have multiple garden beds, create one automation per sensor and customize the message to include the bed name

---

## Wine Cellar Climate Monitor

**Goal:** Monitor both temperature and humidity in your wine cellar and alert when either drifts outside the ideal range. Wine stores best at 12-14 degrees Celsius and 60-70% humidity.

**Sensors needed:** A temperature sensor (trigger) and a humidity sensor (enrichment) in the wine cellar.

### Workflow

```
Start Event (Wine Cellar Temp Sensor)
       |
  Enrichment ("Get cellar humidity")
       |                \
       |           [Error] Boundary Error Event
       |                         |
  Script Task              Set Alarm ("Humidity sensor offline")
  ("Evaluate                     |
   conditions")              End Event
       |
  Exclusive Gateway
      / \
     /   \
 [Problem] [Ideal - Default]
    |          |
 Set Alarm   End Event
 ("Wine       ("Cellar is perfect")
  cellar
  alert")
    |
 End Event
```

### Enrichment Configuration

| Field | Value |
|---|---|
| **Name** | Get cellar humidity |
| **Device** | *(select your wine cellar device)* |
| **Sensor** | *(select the humidity sensor on that device)* |
| **Variable name** | `cellar_humidity` |

### Script Task Expression

```cel
{
  "temp_ok": vars.value >= 12 && vars.value <= 14,
  "humidity_ok": vars.cellar_humidity.value >= 60 && vars.cellar_humidity.value <= 70,
  "all_ok": (vars.value >= 12 && vars.value <= 14) && (vars.cellar_humidity.value >= 60 && vars.cellar_humidity.value <= 70)
}
```

### Gateway Condition

| Flow | Condition | Label |
|---|---|---|
| Flow 1 | `vars.all_ok == false` | Problem detected |
| Flow 2 | *(default)* | Ideal conditions |

### Alarm Motivation Message

```cel
"Wine cellar check — Temperature: " + string(vars.value) + " degrees (ideal: 12-14), Humidity: " + string(vars.cellar_humidity.value) + "% (ideal: 60-70%)"
```

This message includes both readings so you know exactly what drifted, even if only one is out of range.

### Customization Ideas

- Split into separate alarm definitions for temperature and humidity so you can set different severity levels
- Widen the acceptable range slightly (11-15 degrees, 55-75% humidity) if your cellar fluctuates naturally
- Use the same enrichment pattern for any room where two environmental factors matter together — a nursery (temperature + humidity), a server closet, or a greenhouse

---

## Tips for Comfort Automations

- **Start with generous thresholds** and tighten them over time. It is better to get too few alerts initially than to be overwhelmed with notifications for readings that are borderline.
- **Use different alarm definitions for different severity levels.** A living room at 17 degrees is mildly uncomfortable; a wine cellar at 25 degrees could damage your collection. Set the severity accordingly.
- **Give your automations descriptive names.** When you have five or six comfort automations running, "Living room — comfort zone" is much easier to manage than "Automation 3."
- **Check the History tab after adjusting thresholds.** If you change a threshold and start getting more alerts than expected, you can restore the previous version while you reconsider.
