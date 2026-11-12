---
description: List your latest RemixViral videos with status and links (read-only)
argument-hint: "[how many, default 10]"
---

List the user's latest RemixViral videos. This is read-only: do not create or change anything.

1. Call `list_videos` with `limit` set to $ARGUMENTS when that is a number from 1 to 100, otherwise 10.
2. Show a table with title, status, created date and the `videoUrl` of each COMPLETED video, as returned.
3. For a video still rendering, say its status; call `get_video` with its id for details.
