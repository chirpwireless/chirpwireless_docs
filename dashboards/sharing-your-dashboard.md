---
description: Share a Chirp dashboard with a password-protected link — choose View or Control, then copy, regenerate, or revoke it.
---

# Sharing Your Dashboard

You've built a dashboard that shows exactly what you care about — the hallway temperature, the front door sensor, the lamp in the living room. Now you want it somewhere other than your own laptop. On the tablet by the door. On your partner's phone. In the hands of the house-sitter for the two weeks you're away.

A **share link** does that. It turns one dashboard into a web address you can hand to someone, protected by a password you choose. They don't need a Chirp account, they don't need an invitation, and they never see the rest of your home — just the one dashboard you shared. When you no longer want them to have it, you take it back in two taps.

## Why you'd want one

Without a share link, every person who wants to see your data needs an account in your household. That's the right answer for your family. It's a lot of ceremony for a tablet on the wall, and it's more than you want to hand a house-sitter who's only around for a fortnight.

A share link fits the in-between cases:

- **The wall tablet.** The link opens the dashboard full screen, with no menus around it. Mount a cheap tablet in the hallway, open the link once, and it just sits there showing the house.
- **The house-sitter.** Send a **View** link before you leave. They can see that the boiler is fine and the cat's water bowl sensor is reporting. They can't change a thing.
- **Your partner.** A **Control** link means they can actually flip the switches — turn the porch light on, start the heating — straight from the shared page.
- **Grandparents checking in.** A View link on the holiday home dashboard, so they can see the place hasn't frozen over the winter.

And the moment the house-sitter hands the keys back, you revoke the link. It stops working immediately.

This page is about sharing a dashboard you've already built. If you haven't made one yet, start with [Building a Dashboard](building-a-dashboard.md) and [Adding Widgets](adding-widgets/README.md).

## Opening the sharing dialog

1. Open the dashboard you want to share from the **Dashboards** section of the sidebar.
2. Tap the **actions menu** (three dots) in the top right of the dashboard header.
3. Select **Share dashboard**.

The **Dashboard access** dialog opens. Under the title you'll see the helper text **"Protect the link with a password and choose what visitors can do"** — which is a fair summary of the two decisions ahead of you.

If no link has been created for this dashboard yet, the dialog tells you so: **"No link yet. Set a password and generate one."**

## Decide who can reach the dashboard

The first choice is how open the dashboard is:

- **Only organization users can access** — the default, and the private option. Its description reads **"Organization users can view and edit the dashboard according to the organization's permissions"**. Nothing leaves your household: only people who are already members of your Chirp organization can open it, with whatever access they already have.
- **Anyone with the link, no account needed** — the sharing option. This is what produces a link you can send to someone outside your household. Anyone who has the link *and* the password can open the dashboard in a browser.

Pick **Anyone with the link, no account needed** to carry on with the steps below.

## Decide what visitors can do

Once the link is open to anyone, choose the permission the link carries:

- **View** — described as **"Can view the dashboard, but cannot edit widgets"**. The visitor sees live readings and nothing else. They cannot rearrange the dashboard, change a widget, or touch your devices.
- **Control** — the visitor can operate devices from the dashboard's [Control widgets](adding-widgets/control-widget.md). If there's a switch on the dashboard for the porch light, they can flip it.

**Be deliberate about Control.** Anyone holding the link and the password can switch your devices on and off — a lamp, a heater, a pump, a gate. There is no second identity check behind the password. Give **Control** to your partner or to a tablet you trust in a room only your family walks through. For everyone else — the house-sitter, a guest, the neighbor watering the plants — choose **View**.

You can always create a fresh link with a different permission later.

## Set a password and generate the link

1. In the **Password** field (placeholder **"Enter a password"**), type the password visitors will need.
2. Passwords have a minimum length. If yours is too short, the field shows **"Password must be at least N characters"** — lengthen it and try again.
3. Tap **Generate link**.

You'll see the toast **"Share link created"**, and the link appears in the dialog, ready to hand over.

The address looks something like `/dashboards/{id}/fullscreen?t=...`. That `fullscreen` part is the nice bit: whoever opens it gets the dashboard filling the whole screen, with no sidebar and no navigation around it — exactly what you want on a tablet mounted to a wall.

### Sending it on

Tap **Copy link**. You'll see **"Link copied to clipboard"**, and you can paste it into a message, an email, or the tablet's browser.

Send the password separately, and don't paste both into the same message. A link with its password sitting next to it in a group chat is a link anyone in that chat can use.

## Changing the password

If you'd rather rotate the password without disturbing the link itself:

1. Open the dashboard's actions menu and select **Share dashboard** again.
2. Type the new one into the **Password** box.
3. Tap **Change password**.

The toast **"Password changed"** confirms it. The link stays exactly the same — anyone who has it will simply need the new password from now on. This is the gentle option when you want to cut off one person but keep the wall tablet working (you'll just need to type the new password into the tablet once).

## Regenerating the link

Sometimes you want a brand-new address, not just a new password — the old link went somewhere you didn't intend, or you've simply lost track of who has it.

1. Open the **Dashboard access** dialog.
2. Tap **Regenerate link**.
3. A confirmation appears: **"Regenerate share link?"** with the warning **"The previous link will stop working immediately."**
4. Confirm.

The toast **"Share link regenerated"** appears and a fresh link takes the old one's place. Everyone you want to keep sharing with — including your wall tablet — needs the new link. Anyone still holding the old one gets a dead page.

## Revoking the link

When the house-sitter leaves, or the reason for sharing has simply passed, take the link back.

1. Open the **Dashboard access** dialog.
2. Tap **Revoke**.
3. The confirmation reads **"Revoke share link?"** followed by **"The link will stop working immediately and cannot be restored."**
4. Tap **Yes, revoke**.

You'll see **"Share link revoked"**. That link is finished — it can't be brought back, and knowing the password won't help anyone. Your dashboard is untouched and still yours; only the doorway you'd opened is closed. If you want to share again later, generate a new link.

## What your visitor sees

It's worth knowing what's on the other end, so you can help someone who calls you saying "it's not working."

When they open the link, they get a **"Password required"** screen with the message **"This dashboard is protected. Enter the password to continue."** They type the password, and the dashboard opens full screen with live readings.

The messages they might run into instead:

| What they see | What it means | What to tell them |
|---|---|---|
| **"Wrong password"** | The password doesn't match. | Re-send the password — watch for a trailing space when it's copied and pasted. |
| **"Too many attempts. Please try again later."** | Too many failed password tries in a row. | Wait a bit, then try once with the correct password. |
| **"This share link is no longer valid"** | The link was revoked or regenerated. | Send them the current link, or generate a new one. |
| **"This dashboard session has expired. Please reopen the link you were given."** | Their session has simply timed out. | Reopen the original link and enter the password again. |
| **"Access denied"** or **"You do not have permission to access this dashboard"** | The link doesn't grant them access to this dashboard. | Check the dialog is set to **Anyone with the link, no account needed**, and that they're using the current link. |

That expiry message is the one to remember for a wall tablet: a shared session doesn't run forever, so a tablet left alone for a long stretch may eventually ask for the password again.

## Share to TV — the other option

The same actions menu also offers **Share to TV**, and it solves a different problem. Its helper text explains it: **"Open this dashboard on a TV or tablet with a non-expiring key. Create an API key in Settings → API Keys (with device control scope to operate devices), then paste it here."**

The difference is what's behind the link. A share link is protected by a password, hands out **View** or **Control**, and you can revoke it the day someone stops needing it. **Share to TV** is built from an [API key](../settings/api-keys.md) instead — no password screen, and no expiry — which suits a screen that stays put and never gets handed to anyone. Reach for a share link when you're sharing with a *person*; reach for Share to TV when you're setting up a *screen* that lives in your home permanently.

## Tips

- **Default to View.** Give **Control** only when you actually want that person switching your devices. It's a one-word difference in the dialog and a large difference in your hallway.
- **Share one dashboard, not your home.** A link only ever exposes the dashboard it was made from. If you want a house-sitter to see the boiler and nothing else, build a small dashboard with just those widgets and share that one.
- **Use a password you don't use anywhere else.** It's going into a text message. Treat it as disposable — that's exactly what **Change password** and **Regenerate link** are for.
- **Send the link and the password by different routes.** Link by message, password by phone call, for instance.
- **Revoke on the way back from the airport.** The moment the sharing reason ends, so should the link. It takes two taps and it can't be undone — which is the point.
- **Give the wall tablet its own link.** Then, when you regenerate the link you sent a guest, the tablet in the hallway keeps working.

## What's next

- [Building a Dashboard](building-a-dashboard.md) — Create the dashboard you're going to share.
- [Adding Widgets](adding-widgets/README.md) — Choose what appears on it.
- [Control widget](adding-widgets/control-widget.md) — The switches and sliders a **Control** link can operate.
- [API Keys](../settings/api-keys.md) — The keys behind **Share to TV**.
