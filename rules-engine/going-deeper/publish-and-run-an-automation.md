# Publish and Run an Automation

Saving an automation keeps your design safe — but it does not make it live. For your automation to start reacting to sensor data, you need to **build** it and then **deploy** it. This two-step process is deliberate: it lets you work on your automations freely, knowing nothing will run until you are ready.

## The Lifecycle at a Glance

```
Design and save  -->  Build  -->  Deploy  -->  Running
                                                  |
                                               Stop (when needed)
```

- **Design and save** — You work in the editor, adding nodes and expressions. Saving preserves your work but does not affect anything running in your home.
- **Build** — Chirp validates your automation (checks the diagram structure, verifies expressions, confirms all paths are complete) and creates a deployable package called an **artifact**.
- **Deploy** — You activate the artifact so it starts processing live sensor data.
- **Stop** — You can pause a running automation at any time.

## Building Your Automation

When you are satisfied with your automation design:

1. Open the automation in the editor (you need to be in **Edit** mode).
2. Click the **Build** button in the toolbar.
3. A **Build sidebar** opens on the right side. This is a form with the following fields:

| Field | What to enter |
|---|---|
| **Name** | A name for this build artifact. Give it something recognizable — for example, "Basement humidity v1" or "First working version." |
| **Comment** | An optional note about what this build contains or why you are building it. |

4. Click **Save and Build**.

Chirp validates your automation. If everything checks out, the build succeeds and an artifact is created. If there are problems — a missing connection, an invalid expression, an End Event that is not reachable — the build will tell you what needs fixing.

### What Can Go Wrong During a Build

Common issues that prevent a successful build:

- A node has no outgoing connection (dead end that is not an End Event)
- An Exclusive Gateway has a flow without a condition and it is not set as the default
- A CEL expression has a syntax error
- The Start Event has no device or sensor selected

Fix the issue in the editor, save, and build again.

## The Artifacts Tab

Every successful build produces an **artifact** — a snapshot of your automation that can be deployed. You can view all artifacts from the **Artifacts** tab on the main Rules Engine page at `/rules`.

The Artifacts tab shows:

| Column | What it means |
|---|---|
| **Name** | The name you gave the build artifact |
| **Rule** | Which automation this artifact was built from |
| **Status** | Whether the artifact is Running, Stopped, or Force Stopped |
| **Created** | When the build was created |
| **Comment** | The note you added during the build |

### Artifact Statuses

| Status | Color | Meaning |
|---|---|---|
| **Running** | Green | The artifact is live and processing sensor data |
| **Stopped** | Orange | The artifact was stopped by you or another household member |
| **Force Stopped** | Red | The system automatically stopped the artifact due to sustained errors during execution |

Each artifact also has an **Artifact Source** link that opens a **read-only** view of the automation — you can inspect every node and expression exactly as they were when the artifact was built, but you cannot make changes. This is useful for comparing what is running against your current working version.

Comments are **inline editable** — click any comment in the Artifacts table to update it without rebuilding. This makes it easy to add notes after the fact, like "caused false alarms, replaced by v3."

## Deploying an Artifact

From the Artifacts tab:

1. Find the artifact you want to run.
2. Click the **Deploy** action.
3. The artifact status changes to **Running** (green).

Your automation is now live. Every time the trigger sensor sends a new reading, Chirp evaluates it against your automation logic.

You can also deploy right after a successful build — the option is available in the build flow.

## Stopping a Running Automation

If you need to pause an automation — maybe you are doing maintenance, adjusting sensor placement, or just want some quiet:

1. Go to the **Artifacts** tab.
2. Find the running artifact (green status).
3. Click **Stop**.
4. The status changes to **Stopped** (orange).

Stopping is immediate. The automation will not process any new readings until you deploy it again. Sensor data is not lost — it is still recorded — but the automation will not evaluate it while stopped.

## Emergency Auto-Stop

Chirp monitors the health of running automations. If an automation encounters repeated errors over a sustained period — for example, a referenced alarm definition was deleted, or an enrichment sensor was removed — the system automatically stops the artifact to prevent cascading problems.

When this happens, the artifact status changes to **Force Stopped** (red). You will want to open the automation, investigate the issue, fix it, rebuild, and deploy a new artifact.

## Redeploying After Changes

When you edit an automation that already has a running artifact:

1. Make your changes in the editor and save.
2. Build a new artifact (this does not affect the currently running one).
3. Deploy the new artifact.

The old artifact is replaced by the new one. There is no need to stop the old artifact first — deploying a new build handles the transition.

## Tips

- **Give your artifacts meaningful names.** When you have several automations, names like "v1 — basic threshold" and "v2 — added enrichment" help you keep track of what changed.
- **Use comments to note why you built.** Future-you will appreciate knowing "Raised threshold from 60% to 70% after false alarms" when reviewing builds weeks later.
- **Stop before troubleshooting.** If an automation is misbehaving, stop it first, then investigate. You can always redeploy once you have fixed the issue.
- **Check the Artifacts tab regularly.** It gives you a clear picture of what is running across all your automations — a quick way to confirm everything is as expected.
