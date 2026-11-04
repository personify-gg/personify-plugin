---
name: download
description: Get the mp4 of a finished, owner-approved Personify reel. Use when the user wants to download, save, export or post a finished video.
argument-hint: "<video id>"
allowed-tools: mcp__plugin_personify_personify__get_video_download mcp__plugin_personify_personify__list_assets
---

# Download a finished reel

## Steps

1. Take the video id from `$ARGUMENTS`. If there is none, call `list_assets` and offer the finished reels in `reels` (number, title, format) to choose from.
2. Call `get_video_download` with the id.
   - "not finished yet": the reel is still rendering; suggest the `status` skill.
   - "Approve this export in the final review": the owner approves the final cut in Personify first.
3. If `requires_owner_session` is `false`, the `download_url` works for one hour (`expires_at`). Give the link. In a terminal session, offer to save it, for example `curl -L -o reel.mp4 "<download_url>"`, and run that only if the user agrees.
4. If `requires_owner_session` is `true`, the link is the owner's download page in Personify and only opens while they are signed in. Give it to them as such.
5. Remind the user that posting is theirs: download and post, or use publishing inside Personify. This connection cannot publish or schedule posts.
