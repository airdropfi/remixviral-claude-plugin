---
name: make-a-faceless-short
description: Make a faceless Short on the user's RemixViral account from a topic: agree the topic and options, show the balance and the cost, and call create_video only after an explicit yes. Spends credits. Use when the user wants a faceless or prompt-to-video Short and has no source video.
license: MIT
compatibility: Needs the RemixViral MCP server (https://remixviral.ai/api/mcp) connected and signed in. create_video spends credits from the user's own account.
---

# Make a faceless Short with RemixViral

This is the prompt-to-Short workflow for when there is no source video. It does not cut a long video; for that see `review-my-clips`.

## Ground rules

- `create_video` spends credits and a started render cannot be undone. Never call it without an explicit yes to the exact request in this conversation.
- Quote the cost exactly as the `create_video` tool description states it, and the balance exactly as `get_credit_balance` returns it. Never write a credit number from memory.
- Do not retry a timeout or error: check `list_videos` first. An identical request within 10 minutes returns the existing video; at most 3 recent renders run at once.
- The images and voice are AI-generated: remind the user to switch on the platform's AI-content label when they post. This plugin cannot post.
- No promises about views or earnings.

## Steps

1. Agree the topic (up to 500 characters), and optionally the niche, duration (30, 60 or 90 seconds), art style and language with the user. Call `list_niches` for the valid niche and art style values.
2. Call `get_credit_balance`. Tell the user their balance and the cost exactly as the `create_video` tool description states it. Show the exact request you will send.
3. Ask: "Create this video? It spends credits and cannot be undone." Wait for a clear yes.
4. Call `create_video` once. Do not retry on a timeout or error: call `list_videos` first, because an identical request within 10 minutes returns the existing video. Use `allowDuplicate: true` only for a deliberate repeat the user asked for.
5. Poll `get_video` every 20 to 30 seconds until `COMPLETED` or `FAILED`. Give the `videoUrl` when it completes. On `FAILED`, relay the error and any credit numbers as returned.

## If the balance is short

Say so with the numbers returned. You cannot buy credits from here; the user does that in the RemixViral app.
