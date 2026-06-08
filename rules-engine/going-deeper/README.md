---
description: Go beyond single-sensor rules — pull in other sensors, do the math, and publish automations that run live.
---

# More Powerful Automations

Your first automation watches a single sensor and reacts to a simple threshold. That covers a lot of useful scenarios — but sometimes you need your home to be smarter than that.

What if you want to compare the temperature inside your home with the temperature outside before deciding whether something is wrong? Or check the humidity in your wine cellar against a recommended range that depends on the season? These situations call for automations that pull data from more than one source and do a bit of math before making a decision.

This section covers the tools that make that possible:

- **[Data Enrichment and Expressions](data-enrichment-and-expressions.md)** — Fetch readings from other sensors inside the same automation, transform data with CEL expressions, and handle what happens when a sensor is offline. This is how you build automations that consider the full picture, not just one number.

- **[Publish and Run an Automation](publish-and-run-an-automation.md)** — Your automation does not go live until you build and deploy it. This page walks through the entire publish lifecycle — building, deploying, stopping, and understanding what the Artifacts tab shows you.

Through CEL expressions, the logic you can model is very flexible — nested conditions, computed values, severity classifications, and dynamic alert messages that include live sensor readings. Once you are comfortable with these concepts, you will be able to build automations that handle real-world home situations with confidence, even when one sensor reading alone is not enough to tell the full story.
