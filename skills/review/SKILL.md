---
name: review
description: Give the Personify owner the link to review a draft and approve its render inside Personify, without spending anything from the chat. Use when a draft is ready, when the user wants to approve, check casting or price in the app, or when this connection has no render permission.
argument-hint: "<video id or ids>"
allowed-tools: mcp__plugin_personify_personify__prepare_generation_approval mcp__plugin_personify_personify__list_videos
---

# Send the owner the review link

This is the default way a reel gets made: the owner opens the draft in Personify, checks the script, presenter, supporting footage and price, and confirms the render there. Nothing here spends credits.

## Steps

1. Take the video ids from `$ARGUMENTS`. If there are none, call `list_videos` and offer the drafts (status `draft` or `ready_to_render`) to choose from.
2. For each id, call `prepare_generation_approval` and collect its `review_url`.
3. Give the links as a short list, title and link per draft, followed by what the owner checks on that page: the script, the presenter, any supporting footage and the price shown before they confirm.
4. Say that the render starts only when the owner confirms in Personify, and that the `status` skill shows its progress afterwards.
