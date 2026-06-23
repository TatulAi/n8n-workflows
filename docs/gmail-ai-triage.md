# Gmail AI Triage — Automatic Email Sorting

An AI agent that reads incoming Gmail, classifies each message, and acts on it automatically — labeling, archiving, trashing junk, and deciding what to mark as read — so the inbox stays clean without manual sorting.

## Problem it solves
A busy inbox mixes real human messages, client work, bills, security alerts, newsletters, and outright spam. Sorting it by hand wastes time every day and important emails get buried. This workflow does the triage automatically using an LLM, while being deliberately cautious about never trashing anything that might matter.

## How it works
1. **Gmail Trigger** fires when new email arrives.
2. **Extract Content** pulls out the parts of each message the AI needs.
3. **Loop Over Items** processes emails one at a time.
4. **AI Triage Agent** (OpenAI) makes two decisions per email:
   - **Action** — one of: spam, newsletter, notification, administrative, business, personal, or unknown.
   - **Read state** — mark as read, or keep unread because it needs attention.
5. **Output Parser** forces the AI's answer into a strict, predictable structure.
6. **Route Action** sends each email down the right path: apply the matching Gmail label, trash clear junk, or mark routine confirmations as read.
7. **Error Logger** captures anything that fails so nothing is silently lost.

## Design decisions worth noting
- **Safety first:** when the AI is unsure between a trash category and a real one, it always chooses the safe option. Nothing real gets trashed on a guess.
- **Security alerts** about *suspicious* activity are always kept unread and treated as administrative — never auto-dismissed as routine notifications.
- **Structured output parsing** means the downstream routing never breaks on a malformed AI response.
- **Error handling** is built in, not an afterthought.

## Setup
- Connect your own Gmail account in the Gmail nodes.
- Connect your own OpenAI API key in the Chat Model node.
- Create the Gmail labels referenced (Spam, Newsletter, Notification, Administrative, Business, Personal) or adjust to your own.
- No credentials are included in this file — add your own after importing.

## Apps used
Gmail, OpenAI
