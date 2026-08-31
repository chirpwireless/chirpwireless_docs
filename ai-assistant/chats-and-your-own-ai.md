---
description: Start a new chat, find past conversations, see how many requests you have left, and connect your own AI key in Chirp.
---

# Your chats and your own AI

The Helper lives in **AI Chat** in the sidebar. From there you can start a new conversation, reopen an earlier one, check your remaining monthly requests, or connect your own AI provider.

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

Connect your own provider when you want to use a particular model or pay the provider directly. Chats that use your connection do not count against the Helper requests included with your Chirp plan.

Before you start, get an API key from your provider. If you use your own server, it must be reachable from Chirp; an address that works only on your home network will not connect.

To connect:

1. Open **AI Chat**, then tap **Connect your AI**.
2. Under **Provider**, choose OpenAI, Anthropic, OpenRouter, Ollama, or Custom (OpenAI compatible).
3. Check the **Base URL** filled in for the provider. Change it only if you use your own server or another compatible service.
4. Enter the **API Key** supplied by the provider. Chirp keeps it private and masks it in the form. Every provider requires a key, including Ollama.
5. Enter the provider's exact **Model ID**, or choose one of the suggestions.
6. Tap **Check connectivity**. Continue only when the panel reports **Connected**.
7. Tap **Save**.

### Spelling the model name

Chirp sends the Model ID to your provider exactly as entered, so it must match the provider's catalog letter for letter.

Choosing **Ollama** fills in the hosted Ollama Cloud address; it does not connect Chirp to an Ollama server running only on your home network. Ollama model names finish with a colon and a version — `gemma4:31b` — and that version is part of the name, so `gemma4` on its own finds nothing at all. Most of the Ollama Cloud catalog needs a paid Ollama subscription; the two suggestions offered in the box do not. OpenRouter, if you go that way, puts the company first: `anthropic/claude-sonnet-4-6`.

### If it will not connect

**Check connectivity** sends a real request to the provider. If the panel reports **Not connected**, use its message to correct the problem:

| Message | What to do |
|---|---|
| the provider rejected the API key | Copy a valid key from the selected provider. |
| the provider denied this key access to the model | Choose a model included in your provider plan or update the plan. |
| the provider does not serve this model | Correct the Model ID. For Ollama, include the version tag. |
| this model has been retired by the provider | Choose a current model. |
| the provider refused the request for billing reasons | Check billing and spending limits with the provider. |
| the provider is rate limiting this key | Wait, then check the connection again. |
| could not reach AI provider | Check the Base URL and make sure Chirp can reach it. |

After you save, the panel shows the active Base URL, masked key, and Model ID. Return to **Connect your AI** whenever you want to update or disconnect it.

## Where to go next

* [Talking to Your Home](talking-to-your-home.md) — ask the Helper about your sensors
* [Let the Helper Set It Up](let-ai-set-it-up.md) — have it build automations and alerts
* [Your Privacy](your-privacy.md) — what the Helper can and can't see
