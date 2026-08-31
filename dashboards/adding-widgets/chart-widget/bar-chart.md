---
description: Build a Chirp Bar chart and show the exact sensor value on every bar for easier report-by-report comparison.
---

# Bar Chart

Bar is the other type available inside the **Chart** widget. Every sensor report becomes its own bar instead of joining the next point. Pick it when the difference between individual readings is more useful than one continuous curve.

Bar is not part of Last Data and it does not appear as a separate tile in the widget picker. Start with **Chart**, then select **bar** on Appearance.

<figure><img src="../../../.gitbook/assets/chart-widget.jpg" alt="A Chirp dashboard Bar chart with exact values printed above the bars and the current reading below"><figcaption></figcaption></figure>

## Make a Bar chart

1. Choose **Chart** and add one device with one numeric reading.
2. On **Appearance**, set **Widget type** to **bar**.
3. Choose the timeframe and the vertical value range.
4. Add color bands, an average, grid lines, or a legend if they help explain the bars.
5. Turn on **Show metrics below** to keep the reading name and latest value below the plot.
6. Turn on **Display value on bar** to write each value directly on its bar.
7. Save the widget, then save the dashboard layout.

Chirp hides **Display value on bar** when you switch back to Line.

## Example: daily energy readings

Use Bar when a smart meter reports one total for each interval and you want to compare them side by side. With values printed on the bars, a jump from 3.8 kWh to 5.1 kWh is visible without estimating against the scale.

Labels need room. If the chart is narrow or contains many bars, enlarge the dashboard tile or turn the labels off so they do not crowd the history.

## See also

- [Chart Widget](../chart-widget.md) — configure the shared Chart options
- [Line Chart](line-chart.md) — follow the direction of a changing reading
- [Last Data Widget](../last-data-widget.md) — see only the most recent sensor state
