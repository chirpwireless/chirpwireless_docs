# Add Conditions and Branches

Your automation has a Start Event that listens for sensor readings. Now you need to tell it what to do with those readings. In this step, you will add a decision point that checks the humidity value and sends the automation down different paths depending on the result.

## Add a Script Task to Prepare the Data

Before branching, it helps to classify the incoming reading so the decision logic stays clean and readable.

1. From the palette on the left, drag a **Script Task** node onto the canvas (it looks like a rounded rectangle with a document icon).
2. Draw a connection (arrow) from the **Start Event** to the Script Task — hover over the Start Event until the connection handle appears, then drag to the Script Task.
3. Click the Script Task to open its properties panel.
4. Set the **Name** to something descriptive, like "Classify reading."
5. In the **Script** field, enter this CEL expression:

```cel
{"level": vars.value > 70 ? "high" : "normal"}
```

6. Click **Save** in the properties panel.

This expression looks at the sensor's reading (`vars.value`) and creates a variable called `level`. If the humidity is above 70%, `level` is set to `"high"`. Otherwise, it is `"normal"`. Every node after this one can use `vars.level` to make decisions.

### What Is CEL?

[CEL](https://cel.dev) (Common Expression Language) is a simple, safe expression language that Chirp uses for conditions and data transformation. You do not need to be a programmer to use it — if you have ever written a spreadsheet formula, CEL will feel familiar. Chirp still stays visual-first: you build the automation on the canvas, then use CEL only in the places where you need exact logic.

A few things CEL can do:

- Compare values: `vars.value > 70`
- Combine conditions: `vars.value > 70 && vars.level == "high"`
- Do basic math: `vars.value - 20`
- Build text: `"Reading is " + string(vars.value)`
- Use ternary logic: `vars.value > 70 ? "high" : "normal"`

Because CEL supports nested logic, computed values, and multi-sensor comparisons, the automations you can build go well beyond simple thresholds. You will see more examples as you explore the [Going Deeper](../going-deeper/) section.

## Add an Exclusive Gateway

An Exclusive Gateway is a decision diamond that routes the automation down exactly one path based on conditions you define.

1. Drag an **Exclusive Gateway** from the palette (it looks like a diamond shape).
2. Draw a connection from the **Script Task** to the Exclusive Gateway.
3. Now draw **two outgoing connections** from the gateway — one going to where you will put your alarm action (we will add that node in the next step), and one going to an **End Event** (drag an End Event from the palette first — it is a circle with a bold border).

You should now have two paths leaving the gateway: one for "humidity is high" and one for "everything is fine."

## Configure the Gateway Conditions

1. Click the **Exclusive Gateway** to open its properties panel.
2. You will see a list of **Flows** — one for each outgoing connection you drew. Each flow has fields for a label, a color, and a condition expression.

Set them up like this:

| Flow | Label | Color | Condition |
|---|---|---|---|
| Flow 1 | High humidity | Red or orange | `vars.level == "high"` |
| Flow 2 | Normal | Green | *(set as default)* |

3. For Flow 2, click **Set as default**. This makes it the fallback path — it runs when no other condition matches.
4. Click **Save** in the properties panel.

### How Conditions Are Evaluated

The gateway checks conditions **from top to bottom**. The first condition that evaluates to `true` wins, and the automation follows that path. All other paths are skipped.

The default flow has no condition — it catches everything that did not match the conditions above it. Always include a default flow so your automation has somewhere to go even when readings are normal.

You can reorder flows by grabbing the **drag handle** on each flow row and moving it up or down in the properties panel. This matters because the first match wins. For example, if you had both `vars.value > 50` and `vars.value > 70`, putting the > 70 check first ensures critical readings are caught before the less urgent condition.

### Labels and Colors

Labels appear on the arrows in your visual diagram, and colors help you see at a glance which path is which. Using a red or orange arrow for the alert path and a green arrow for the normal path makes the automation easy to read weeks or months later.

## What Your Automation Looks Like Now

```
Start Event (Basement Sensor)
       |
  Script Task ("Classify reading")
       |
  Exclusive Gateway
      / \
     /   \
  [High]  [Normal - Default]
    |         |
   ???     End Event
```

The "High humidity" path does not lead anywhere useful yet — it needs an alarm action. That is exactly what you will add next.

**Next:** [Trigger Alarms and Actions](trigger-alarms-and-actions.md)
