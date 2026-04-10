---
name: animate-old-photos
description: >
  Animate old photos into AI-generated videos using the Animate Old Photos MCP tools.
  Use when the user wants to animate a photo, bring an old photo to life,
  turn old photos into videos, create a video from a still image,
  or convert a photo to video.
  Requires a paid API key from https://animateoldphotos.org
---

# Animate Old Photos

Animate old photos into AI-generated videos via MCP tools.

## Prerequisites

> **This is a paid service.** You need an API key and credits.
>
> - Official Website: [Animate Old Photos](https://animateoldphotos.org/)
> - Get your API key: [Profile > API Key](https://animateoldphotos.org/profile/interface-key)
> - Purchase credits: [Buy Credits](https://animateoldphotos.org/pricing)
>
> Each animation costs **3 credits**. [View pricing plans](https://animateoldphotos.org/pricing)

## Available MCP Tools

This plugin provides three tools via the `animate-old-photos` MCP server:

- **`check_credits`** — Check your credit balance
- **`animate_photo`** — Submit a photo for animation (returns a task ID)
- **`get_task_status`** — Poll task progress until the video is ready

## Workflow

1. If the user has not provided an API key, ask for it. The key can also be stored in environment variable `AOP_API_KEY`.
2. Call `check_credits` with the API key to verify it works and check the balance.
3. The user must provide a **publicly accessible image URL** (JPEG or PNG, max 10MB, min 300x300px). If the user has a local file, help them upload it to a public host first.
4. Confirm with the user: "This will cost 3 credits. You have {N} credits. Proceed?"
5. Call `animate_photo` with the API key, image URL, and optional prompt.
6. Call `get_task_status` every 30 seconds until status is "completed".
7. Present the video URL to the user.

## Prompt Tips

The `prompt` parameter is optional. When provided, describe the desired motion in 1-2 short sentences:
- "grandmother smiling and waving"
- "two children playing and laughing"
- "slight head movement, looking into camera"

If omitted, the AI will auto-generate appropriate motion.

## Error Handling

- **Invalid API key** — Direct user to: https://animateoldphotos.org/profile/interface-key
- **Insufficient credits** — Direct user to: https://animateoldphotos.org/pricing
- **Task failed** — Suggest retrying with a different prompt or image. Credits are refunded on failure.

## Constraints

- Supported formats: JPEG, PNG
- Max file size: 10 MB
- Min image dimension: 300 x 300 px
- Cost per animation: 3 credits
- Video duration: 5 seconds
- Typical processing time: 2-5 minutes
