---
name: schedule-linkedin-post
description: Schedule, publish now, reschedule or cancel a Flypost post on LinkedIn using Flypost's schedule card, where the user picks who to post as, the day and the time. Use when the user says schedule it, post it, publish this, put it out on Tuesday, when should I post this, cancel or move a scheduled post, or asks what is already scheduled.
---

# Schedule a post with the schedule card

Publishing puts the user's name on LinkedIn, so the user makes the final choice. In Claude the
choice is made on Flypost's schedule card: you open it, the user picks, the card's button schedules.

## 1. Find the draft

Use the draft you just wrote or designed. Otherwise `flypost_list_drafts` and confirm with the user
which one. If it is a carousel or an image post, make sure it has its caption text
(`flypost_get_draft`); a visual with an empty caption is rarely what they want.

## 2. Check LinkedIn is connected

`flypost_get_linkedin_connection` lists who the project can post as (the user's profile, company
pages, teammates). If nothing is connected, call `flypost_connect_linkedin` and give the user the
link it returns to open in their browser. Never open or complete it yourself. Check the connection
again once they say it's done.

## 3. Open the schedule card

Call `flypost_prepare_schedule` with the `draft_id`. If the user named a day or time, pass them in
the user's own time zone: `date` as `YYYY-MM-DD` and `time` as 24-hour `HH:MM`. Work out relative
days ("Tuesday", "tomorrow") from today's date. Without a time the card opens on 09:00; without a
day, on the next free day.

The card shows the post, who it can go out as, and what is already scheduled, so the user can
avoid stacking two posts on one day.

**Then stop.** Tell the user the card is ready and that its button schedules the post. Do not call
`flypost_schedule_post` yourself after opening the card: the card does it, with the identity, day
and time the user chose. Scheduling it yourself as well can post at the wrong time or as the wrong
identity.

If the user asks for advice on timing, use `flypost_get_post_analytics` to see when their best posts
went out, and suggest a slot before opening the card.

## When there is no card

Some Claude apps do not show cards. If the user cannot see it, or they have spelled out everything
in chat, confirm the three choices in one sentence: the post (its first line), who it goes out as,
and the exact day and time with their time zone. Only after they say yes, call
`flypost_schedule_post` with:

- `draft_id`
- `scheduled_at`: an ISO 8601 timestamp with the time zone offset, for example
  `2026-11-17T09:00:00+00:00`. Leave it out only when they want it published **now**, and confirm
  that explicitly, since it goes live straight away.
- `post_as`: `me`, `company`, or the name of a page or person exactly as
  `flypost_get_linkedin_connection` lists it (or `connection_id` from the same list).

A carousel needs no separate render: if its PDF is missing or older than the slides, the status
comes back as `deferred` and the post goes out as soon as the render finishes. Say so, so the user
does not think it failed.

## Moving or cancelling

- To cancel, confirm which post, then `flypost_cancel_scheduled_post`. The draft goes back to
  editable.
- To move a post, cancel it and open the card again for the new time.
- `flypost_list_drafts` with `publish_status: ["scheduled"]` lists what is already scheduled.

Never delete a post (`flypost_delete_post`) unless the user asks for that in so many words.
