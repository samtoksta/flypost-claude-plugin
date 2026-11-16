---
name: plan-post-ideas
description: Plan LinkedIn post ideas with Flypost that fit what has worked for the user and never repeat what they have already published. Use when the user asks for post ideas, topics, a content plan, next week's posts, a content calendar, or wants to fill or review their Flypost idea board.
---

# Plan post ideas without repeating what's published

You have no memory of what this user has already posted. Flypost does. The order below makes sure
every idea you pitch is new to them and modelled on evidence, not guesses.

## 1. Pick the project

If no project is active, call `flypost_list_projects`, ask which one when there are several, then
`flypost_use_project`.

## 2. Learn what works before pitching anything

- `flypost_get_post_analytics`: the user's own LinkedIn posts with their real numbers, plus the
  median impressions per format. Note the topics, hooks and formats that earned the most reach, and
  the ones that fell flat.
- `flypost_search_inspiration`: what the creators this project monitors are posting, ranked by how
  far each post beat that creator's usual. Sort by `recent` for what is being talked about this
  week. Use it to learn what resonates, never to copy someone's wording or pass off their claims.
- `flypost_get_brand_kit` and `flypost_get_writing_voice`: who the audience is, what the business
  sells, and the words and formats the user avoids.
- `flypost_search_source_docs`: what the user's own material can actually support. An idea the
  Brain has nothing on is an idea you would have to invent the substance for.

`flypost_list_ideas` shows the idea board as it stands (it renders as a board in Claude), so you can
see what is already queued.

## 3. Draft candidates, then check coverage on all of them at once

Write more candidates than the user asked for (about one and a half times as many), each with a
short title and a one-line angle: the argument the post makes.

Send every candidate to `flypost_check_coverage` in **one call**, with its angle. It compares them
against existing ideas, drafts, and the posts the user has already published, including posts
written outside Flypost, which nothing else can see.

- `duplicate`: drop it, or change the angle so it makes a different argument.
- `related`: read the neighbours it lists (body matches carry an excerpt) and re-angle so the idea
  says something they don't.
- `clear`: no overlap found. That is word overlap, not meaning, so still use judgement.

Do this before you develop or save anything. `flypost_save_idea` refuses duplicates anyway, so
skipping the check only wastes the writing.

## 4. Pitch them

Show the user the surviving ideas: title, angle, suggested format (text post, carousel,
infographic, stat image), and the evidence behind each (the post of theirs it builds on, the Brain
source it draws from). Let them pick, cut and change before you save.

## 5. Save the ones they keep

`flypost_save_idea` for each, matching Flypost's own idea format:

- `title`: a short, punchy headline, at most 90 characters, with no quotation marks or em dashes.
- `angle`: one or two sentences, as it would read on the idea card.
- `development_notes`: everything you found and want the post to use: the sources, figures, dates,
  quotes, the opener you have in mind and how to structure it. Flypost uses these notes as the
  idea's own research when it is developed.
- `agent_name: "Claude"` and an `authoring_note`, so the idea is filed and credited under your name.

Never put a statistic in an idea that you did not find in a source or get from the user.

## Using Flypost's own brainstorm

If the user asks for Flypost's brainstorm by name, call `flypost_brainstorm_ideas` (it takes a
minute or more). Its ideas start developing in the background as soon as they land; pass
`auto_develop: false` if you will write the concepts yourself. Run `flypost_check_coverage` on what it
returns too, passing each idea's `content_bank_item_id` so it is not reported as its own duplicate.

## Then

To write one of the ideas up, use the `write-linkedin-post` skill. For a carousel or infographic
idea, use `design-linkedin-visual`. Unwanted ideas can be removed with `flypost_discard_idea` when the
user asks.
