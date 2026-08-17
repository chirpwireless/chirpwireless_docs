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

### Give each row the name your automation looks for

Your automation finds these values through `vars`, so the names have to line up. If a condition says `vars.temperature > 25`, the row has to be called **`temperature`** — `temp` or `value` won't do, and the automation will stop at that node when it can't find what it's looking for.

The easiest way to get this right is to open your conditions and copy the names out of them.

You don't have to fill in everything yourself:

* The panel starts you off with a row called `value`, which is what plenty of automations read straight from the sensor. Rename it if yours uses something else.
* `sensor_id` is filled in from the sensor on your Start node, and turns up in the Variables tab by itself.

## Nothing happens until you press a button

Loading a session doesn't run your automation. It opens it up, puts the marker on the Start node, and waits for you — **nothing moves until you press Run or one of the Step buttons**.

You'll see the canvas go read-only, a toolbar appear at the bottom, the debug panel open on the right with your values in it, and a blue ring around the Start node. That blue ring means the session is ready and waiting for you.

So if the diagram just sits there, that's why. Press **Run (F10)** to go until the first breakpoint or the end, or **Step over (F9)** to move one node at a time.

## The debug controls

Once a session is loaded, a small toolbar appears over the bottom of the canvas with five buttons. It sits on the diagram itself, not up in the top bar with Save and Build.

* **Run (F10)** — run the automation until it hits a breakpoint or finishes.
* **Step over (F9)** — do the next node and stop, showing what it produced.
* **Step into (F8)** — go *inside* the next node to see its inner workings — its inputs, scripts, and outputs — not just the result.
* **Run ignore breakpoints (F11)** — run all the way through without stopping. It does that by turning all your breakpoints off, and they stay off for the rest of the session — switch them back on in the Breakpoints tab when you want them.
* **Stop (F12)** — end the debug session.

**F12 is the same button at both ends:** press it while you're editing to start debugging, and again while you're debugging to stop.

The Step buttons only work while things are paused. They go grey while the automation is running, while a Side Effect box is waiting for your answer, and if an automation failed to load. Stop always works.

## What the rings and dots mean

Nodes can pick up three different marks while you're debugging:

| Mark | What it means |
| --- | --- |
| **Blue ring** | Where you are right now. The next step happens here. |
| **Small red dot** on top | A breakpoint. Solid means it's on, a hollow ring means you've switched it off. |
| **Red ring** | The node that just hit an error. It clears as soon as a step works. |

A red ring isn't a breakpoint and isn't where you are — it's the node that went wrong, and the expression on it is the place to look. See [When a node fails](#when-a-node-fails).

## Breakpoints

A breakpoint is a "pause here" marker. It stops the automation at one node so you can see what's going on at exactly that point.

* **Add a breakpoint** — click a node on the canvas. The **Breakpoints** tab in the debug panel lists them all, with a count in the tab. Any click on the canvas during a session adds or removes one, so if you spot a breakpoint you didn't mean to set, click that node again to clear it.
* **Turn one on or off** — each breakpoint has a little red dot. Click it to switch the breakpoint off for now, and on again later, without deleting it.
* **Conditional breakpoints** — add an ordinary breakpoint first, then click **Set condition** on it and type a CEL expression. The automation will then pause there *only* when your condition is true — for example, only when `vars.value > 25`. A breakpoint with a condition gets a **Conditional** label. See [CEL for Home Automations](cel-for-home-automations.md) for how to write expressions.

Conditional breakpoints are great for a problem that only happens sometimes — let the automation run normally and have it stop only on the reading that causes the trouble.

## Watching the values

The **Variable** tab of the debug panel shows the automation's state at the current step, in two parts:

* **Changes** — the variables that were just added or changed, highlighted so you can instantly see what the last node did. Anything that was removed shows with a line through it.
* **All variables** — the full list of every variable and its current value.

While the automation is paused, you can also **change** the state yourself — edit a value, add a variable, or remove one. That lets you nudge the automation down a particular path you want to test without starting over with different input.

When you use **Step into** on a node, the Variable tab also shows a detail card with that node's **Inputs**, **Scripts**, and **Outputs** — what's happening inside the step.

## Watch expressions and Evaluate

The **Watch** tab keeps an eye on expressions while the automation runs:

* **Add watch** — type a CEL expression and it's re-checked at every step, so you can follow a value (like `vars.value - 20`) without scanning the whole variable list.
* **Evaluate** — type a one-off CEL expression and check it against the current state right away — handy for trying out a piece of logic before you commit to it.

Both reach your values through `vars`, so a watch on a variable called `temperature` is written `vars.temperature`. If an expression won't work, it's turned away as you type it in — which makes this a quick way to try a condition out before putting it on a branch.

## Side effects

Some nodes don't just shuffle data around — they actually *do* something, like sending you a notification or raising an alarm. When debug reaches a node like that, a **Side Effect** dialog pops up and asks how to handle it. You get three choices:

* **Execute — run the real handler.** The action really happens, just like it would in a live automation: the alarm goes off, everyone on the list is notified, and a command really reaches the device.
* **Skip — variables unchanged.** The action is skipped and the variables are left alone.
* **Mock — provide a mock response.** You supply a pretend response as JSON and the automation carries on as if the action had returned it. It needs to be valid JSON — if it isn't, the mock just isn't used.

**Execute is already ticked when the box opens**, so change it before you hit Apply if you'd rather nothing really happened. This is what lets you test an automation that sends alerts without actually buzzing everyone's phone. Choose **Skip** or **Mock** while you're working on the logic, and **Execute** only when you want to check that the real notification goes out.

Two things happen after you answer:

* **The same answer gets used again.** If the automation comes back round to that node later in the session, the box doesn't reappear — your first answer is used. So an **Execute** keeps really sending every time after that. Start a fresh session if you want to be asked again.
* **Closing the box steps back.** If you close it without picking anything, you end up just before that node with it not done. Step again and the box comes back.

## When a node fails

If a node hits an error while running, it gets a red ring on the canvas — so you can see exactly where the problem is without hunting through a big automation. If the error is one you can recover from, the debug session stays paused and loaded so you can take a look, adjust, and carry on; if it's not recoverable, the session ends.

Nearly always it's the expression on that node. Open it and check three things:

1. **Everything it mentions is in the Variables tab.** `vars.temperature > 25` falls over if nothing called `temperature` was set at the start or made by an earlier node. On a branch point this stops the automation right there — it does *not* carry on down the fallback branch.
2. **The `vars.` is there.** `temperature > 25` isn't the same as `vars.temperature > 25`.
3. **It gives back a yes or no.** A branch condition has to come out as `true` or `false`.

Drop the expression into **Evaluate** on the Watch tab to try it against what you've got right now.

## When a session ends

A debug session lasts **30 minutes** from the moment it starts, and stepping through doesn't buy you more time. You'll get a heads-up just before it expires, and a message if it times out, closes (with the reason), or loses its connection — just start a fresh session to keep going.

Breakpoints belong to the diagram you loaded, so reloading the editor can clear them. A note tells you how many went, so you can set them again.

If a session won't start at all, the platform is running as many debug sessions as it can at that moment. Give it a minute and try again.

## Tips

* Test the tricky cases, not the easy one — set the initial context to the exact temperature, the missing value, the odd reading.
* Copy variable names out of your conditions instead of typing them from memory.
* Use a conditional breakpoint to catch a problem that only happens now and then.
* Change a variable mid-session to send the automation down a specific branch, instead of restarting with new input.
* Keep side effects on **Skip** or **Mock** while you're experimenting; switch to **Execute** only when you want a real end-to-end test.
* Once the automation behaves the way you want, publish it — see [Publish and Run an Automation](../going-deeper/publish-and-run-an-automation.md).

## See also

* [Visual Editor](visual-editor.md) — The canvas debug mode runs on
* [CEL for Home Automations](cel-for-home-automations.md) — Writing expressions for conditions and watches
* [Publish and Run an Automation](../going-deeper/publish-and-run-an-automation.md) — Turn on an automation once it works
* [Fixing Builds and Runtime Stops](fixing-builds-and-runtime-stops.md) — Build errors and force-stops
