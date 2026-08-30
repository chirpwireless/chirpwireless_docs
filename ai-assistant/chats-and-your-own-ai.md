---
description: Start a new chat, find past conversations, see how many requests you have left, and connect your own AI key in Chirp.
---

# Your chats and your own AI

The Helper lives in **AI Chat** in the sidebar. Beyond the conversation itself, there are a few handy things around it: starting fresh chats, finding old ones, keeping an eye on how many requests you have left, and — if you'd like — bringing your own AI.

## Starting a fresh chat

Tap **New Chat** at the top of AI Chat to begin a clean conversation. The Helper remembers what you've been talking about *within* a chat, which is great for refining ("make that 10 minutes instead") — so when you switch to something unrelated, like asking about the garden after sorting out the bedroom, start a new chat so it doesn't mix the two up.

## Finding past chats

**Chat history**, also at the top, lists your previous conversations with the newest first. Each one is named after what you talked about; a brand-new one shows as **Untitled chat**. Tap any entry to reopen it and carry on. Your chats are saved between visits and are only ever yours. Haven't chatted yet? You'll see **No conversations yet**.

## Deleting a chat

In Chat history, **Delete conversation** clears a chat for good. There's no undo, so only remove the ones you don't want to keep.

## How many requests you have

Your Chirp plan includes a set number of Helper requests each month, and higher plans include more. You'll always see how many you have left right above the message box.

When you run out, the Helper lets you know you've reached your limit — but everything else in Chirp keeps working exactly as before. You can still check on your home, get your alerts, and control your devices as usual. To keep chatting with the Helper, move up to a plan with more requests, or connect your own AI key (below), which doesn't count against the monthly number.

## Using your own AI key

Prefer to bring your own? Open **Connect your AI** at the top of AI Chat. There are four boxes, and the last one is the only fiddly bit.

* **Provider** — OpenAI, Anthropic, OpenRouter, Ollama, or Custom (OpenAI compatible).
* **Base URL** — fills itself in once you choose a provider. Only change it if you are pointing at your own server or at a service that is not on the list, and make sure it is an address reachable from outside your house — something that only answers on your home network will not work.
* **API Key** — the key from that provider. It is kept private and hidden like a password. You need one whichever provider you choose, Ollama included.
* **Model ID** — the model's name, spelled the way your provider spells it. Type it, or tap one of the suggestions.

### Spelling the model name

This is where it usually goes wrong. The name is handed straight to your provider, so it has to match theirs letter for letter.

Ollama is the one to watch. Its names finish with a colon and a version — `gemma4:31b` — and that version is part of the name, so `gemma4` on its own finds nothing at all. Ollama's suggestions point at Ollama Cloud, where most models want a paid Ollama subscription; the two offered in the box do not. OpenRouter, if you go that way, puts the company first: `anthropic/claude-sonnet-4-6`.

### If it will not connect

Tap **Check connectivity** before you save and it genuinely tries, so you find out now instead of halfway through a conversation next week. You will see **Connected**, or a line naming the problem:

* *the provider rejected the API key* — mistyped, cancelled, or belonging to a different account.
* *the provider denied this key access to the model* — the key is fine, the plan behind it is not. Almost always Ollama Cloud asking for a subscription.
* *the provider does not serve this model* — check the spelling, and on Ollama check the version on the end.
* *this model has been retired by the provider* — it existed once; pick a current one.
* *the provider refused the request for billing reasons* — worth logging in to that provider and looking at the account.
* *the provider is rate limiting this key* — you have asked too much too quickly. Wait a moment.
* *could not reach AI provider* — whatever is in Base URL is not answering.

Then **Save**. From then on your own AI runs your chats, the monthly limit stops applying, and the panel goes on showing which model you are using so you are not guessing about it later. You can change or remove the key anytime from the same place.

## Where to go next

* [Talking to Your Home](talking-to-your-home.md) — ask the Helper about your sensors
* [Let the Helper Set It Up](let-ai-set-it-up.md) — have it build automations and alerts
* [Your Privacy](your-privacy.md) — what the Helper can and can't see
