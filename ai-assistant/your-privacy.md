---
description: Understand Chirp AI Assistant access, confirmation prompts, saved conversations, and the data sent to your configured model provider.
---

# Your Privacy

The AI Assistant can work on your home setup using the same account permissions you have. Adding sensors, changing automations, and reading their results stay within the home selected in Chirp. Here is how access, confirmation prompts, and saved conversations work while you delegate those tasks.

Your messages and the information retrieved to answer them can reach the configured AI model provider. Conversations remain available in chat history, so keep passwords and unrelated secrets out of your messages. Use [Your Chats and Your Own AI](chats-and-your-own-ai.md) to review your chat and provider choices.

## It works only within your access

The assistant uses your active login session to decide what it can do. If you can view a sensor on your dashboard, the assistant can answer questions about it; if you can change an automation, the assistant can help you change it. If you can't do something yourself, neither can the assistant. There is no special elevated access.

## It asks before anything big

When you ask the assistant to set something up, the small, safe steps just happen — but before anything important or permanent, like removing a device or an automation, it shows a clear **Confirm Action** / **Cancel** prompt and waits for you. Read the confirmation before approving it. Routine setup steps can run without a separate prompt.

## Your home is isolated

The assistant is walled off from every other household on the platform. It cannot access data from other homes, and no one else's assistant can access yours — even if you belong to more than one home in Chirp.

## What gets saved

Your questions and the assistant's answers are stored so you can scroll back through previous conversations. This chat history is private to your individual account. Other members of your household cannot see what you asked or what the assistant replied.

## What does not get saved

The chat is not a full archive of sensor history. Readings included in an answer or a tool result can still appear in the conversation, and anything you type becomes conversation content. Keep passwords, payment details, and unrelated API keys out of chat; use the dedicated settings for your model key.

## How a question gets answered

1. You describe a task or ask a question.
2. The assistant works out which information and operations it needs.
3. It can read your setup and make authorized changes, using confirmation prompts for consequential actions.
4. It uses the operation results to explain what happened, ask for a missing detail, or continue the setup. The response streams back into the conversation.

## A simple guideline

Keep account passwords and unrelated API keys out of chat. Device onboarding may require the device identifiers and network keys supplied by its manufacturer; share those only for the intended setup, remembering that conversation content can be retained. Enter your model-provider key in the dedicated AI settings.
