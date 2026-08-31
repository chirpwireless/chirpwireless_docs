---
description: Set up a Chirp Line chart to follow a sensor trend with a current reading, average, and colored ranges.
---

# Line Chart

Line is one of the two types inside a **Chart** widget. It joins the sensor reports into one trace, which makes the direction and shape of a change easy to follow.

Choose it for room temperature, humidity, energy use, soil moisture, or any reading where you care about the journey between “then” and “now.”

<figure><img src="../../../.gitbook/assets/chart-widget-line.jpg" alt="Chirp Chart settings with Line selected and a continuous history shown in the preview"><figcaption></figcaption></figure>

## Make a Line chart

1. Edit the dashboard and choose **Chart**.
2. On **Datasource**, add one device and one number reading.
3. Tap **Next**, then choose **line** for **Widget type**.
4. Pick how far back to look: Last hour, Last day, Last week, or Last month, depending on your plan's data retention.
5. Set **From** and **To** so the up-and-down scale fits the reading.
6. Add any colored threshold bands, average line, grid lines, or legend that will make the history easier to understand.
7. Use **Show metrics below** if you want the reading name and latest value repeated beneath the graph.
8. Save the widget and the dashboard.

You will not see **Display value on bar** while Line is selected. That option belongs only to the Bar type.

## Example: bedroom temperature

Choose Last day and a range of 10–30°C. Add a comfortable band from 17–21°C. The line shows whether the room stayed inside that range through the night or gradually cooled before morning; the large number still tells you the temperature right now.

## See also

- [Chart Widget](../chart-widget.md) — settings shared by both Chart types
- [Bar Chart](bar-chart.md) — keep reports visually separate
- [Last Data Widget](../last-data-widget.md) — show the latest reading without its history
