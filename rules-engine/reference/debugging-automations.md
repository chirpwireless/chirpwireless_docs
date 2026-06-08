---
description: Step through an automation with debug mode — feed it a test reading, set breakpoints, and watch the values change.
---

# Debugging Automations

You built an automation, turned it on, and it didn't do what you expected — it fired when it shouldn't have, or stayed quiet when it should have alerted. Debug mode helps you figure out *why*. Instead of guessing, you run the automation step by step and watch exactly what it does at each point.

Debug mode is a step-through tester built right into the visual editor. You give the automation a pretend sensor reading, then walk through it one node at a time — pausing where you like, watching the values change, and checking your logic. It's the best way to be sure an automation works before you rely on it.

## Starting a debug session

1. Open the automation in the [visual editor](visual-editor.md).
2. In the editor's top bar, click **Set context** to open the **Start Debug Session** panel. (The top bar also has a **Start Debug** button, shortcut **F12**.)
3. The panel asks you for some **initial context** — the pretend reading the automation will run against. It starts with one value row, and each row has a **Name** and a **Value**:
   * **Name** is the variable your automation expects — often `value`, or something like `temperature` or `status`.
   * **Value** is the test reading. It can be a number, `true` / `false`, `null`, or text — the panel works out what you mean.
4. Click **Add metric** to add more, and remove any extra row you don't need.
5. Click **Load and Start**. The automation loads and pauses, ready for its first step.

This initial context stands in for what your sensor would really send. Set it to the situation you want to test — the moment the door opens, the temperature that should trigger the alert, the reading you think is causing trouble.

## The debug controls

Once a session is running, a small toolbar appears at the bottom of the editor with five buttons:

* **Run (F10)** — run the automation until it hits a breakpoint or finishes.
* **Step over (F9)** — do the next node and stop, showing what it produced.
* **Step into (F8)** — go *inside* the next node to see its inner workings — its inputs, scripts, and outputs — not just the result.
* **Run ignore breakpoints (F11)** — run all the way through without stopping at any breakpoint.
* **Stop (F12)** — end the debug session.

As the automation runs, the node it's currently on is highlighted on the canvas, so you always know where you are.

## Breakpoints

A breakpoint is a "pause here" marker. It stops the automation at one node so you can see what's going on at exactly that point.

* **Add a breakpoint** — click a node on the canvas. The **Breakpoints** tab in the debug panel lists them all, with a count in the tab.
* **Turn one on or off** — each breakpoint has a little red dot. Click it to switch the breakpoint off for now, and on again later, without deleting it.
* **Conditional breakpoints** — click **Set condition** on a breakpoint and type a CEL expression. The automation will then pause there *only* when your condition is true — for example, only when `value > 25`. A breakpoint with a condition gets a **Conditional** label. See [CEL for Home Automations](cel-for-home-automations.md) for how to write expressions.

Conditional breakpoints are great for a problem that only happens sometimes — let the automation run normally and have it stop only on the reading that causes the trouble.

## Watching the values

The **Variable** tab of the debug panel shows the automation's state at the current step, in two parts:

* **Changes** — the variables that were just added or changed, highlighted so you can instantly see what the last node did. Anything that was removed shows with a line through it.
* **All variables** — the full list of every variable and its current value.

While the automation is paused, you can also **change** the state yourself — edit a value, add a variable, or remove one. That lets you nudge the automation down a particular path you want to test without starting over with different input.

When you use **Step into** on a node, the Variable tab also shows a detail card with that node's **Inputs**, **Scripts**, and **Outputs** — what's happening inside the step.

## Watch expressions and Evaluate

The **Watch** tab keeps an eye on expressions while the automation runs:

* **Add watch** — type a CEL expression and it's re-checked at every step, so you can follow a value (like `value - 20`) without scanning the whole variable list.
* **Evaluate** — type a one-off CEL expression and check it against the current state right away — handy for trying out a piece of logic before you commit to it.

## Side effects

Some nodes don't just shuffle data around — they actually *do* something, like sending you a notification or raising an alarm. When debug reaches a node like that, a **Side Effect** dialog pops up and asks how to handle it. You get three choices:

* **Execute — run the real handler.** The action really happens, just like it would in a live automation.
* **Skip — variables unchanged.** The action is skipped and the variables are left alone.
* **Mock — provide a mock response.** You supply a pretend response as JSON and the automation carries on as if the action had returned it. It needs to be valid JSON — if it isn't, the mock just isn't used.

This is what lets you test an automation that sends alerts without actually buzzing everyone's phone. Choose **Skip** or **Mock** while you're working on the logic, and **Execute** only when you want to check that the real notification goes out.

## When a node fails

If a node hits an error while running, the node that failed is highlighted on the canvas and a notification tells you what went wrong — so you can see exactly where the problem is without hunting through a big automation. If the error is one you can recover from, the debug session stays paused and loaded so you can take a look, adjust, and carry on; if it's not recoverable, the session ends.

## When a session ends

A debug session doesn't run forever. You'll get a heads-up just before it expires, and a message if it times out, closes (with the reason), or loses its connection — just start a fresh session to keep going. Breakpoints can also be cleared when the editor reloads; if any go missing, a note tells you how many, so you can set them again.

## Tips

* Test the tricky cases, not the easy one — set the initial context to the exact temperature, the missing value, the odd reading.
* Use a conditional breakpoint to catch a problem that only happens now and then.
* Change a variable mid-session to send the automation down a specific branch, instead of restarting with new input.
* Keep side effects on **Skip** or **Mock** while you're experimenting; switch to **Execute** only when you want a real end-to-end test.
* Once the automation behaves the way you want, publish it — see [Publish and Run an Automation](../going-deeper/publish-and-run-an-automation.md).

## See also

* [Visual Editor](visual-editor.md) — The canvas debug mode runs on
* [CEL for Home Automations](cel-for-home-automations.md) — Writing expressions for conditions and watches
* [Publish and Run an Automation](../going-deeper/publish-and-run-an-automation.md) — Turn on an automation once it works
* [Fixing Builds and Runtime Stops](fixing-builds-and-runtime-stops.md) — Build errors and force-stops
