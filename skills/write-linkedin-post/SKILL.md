---
name: write-linkedin-post
description: Write, rewrite or tighten a LinkedIn post in the user's own voice with Flypost, grounded in their Brain (their blog posts, videos, documents and notes). Use when the user asks for a LinkedIn post, a draft, a caption, a rewrite of an existing Flypost draft, or "a post about X", and the Flypost connector is available.
---

# Write a LinkedIn post in the user's voice

You write the words yourself, in the conversation, and save them to Flypost. You can iterate with
the user quickly, and it does not spend their Flypost AI allowance. Use Flypost's own writer
(`flypost_generate_post_draft`) only when the user asks for it by name or wants Flypost's built-in
web research.

## 1. Pick the project

Everything in Flypost belongs to a project. If none is active yet, call `flypost_list_projects`. With
one project, use it; with several, ask which, then call `flypost_use_project`.

## 2. Learn who they are and how they write

Call `flypost_get_brand_kit` and `flypost_get_writing_voice` before writing a word.

- The writing voice is the user's own rulebook: tone, sentence length, words to avoid, formatting
  rules (emoji, hashtags, line breaks, lists). Follow it exactly. If it bans a word, the word does
  not appear, even in a hook.
- The brand kit says who the audience is and what the business sells. Write for that audience.

## 3. Make sure it is not a repeat

If the post is on a new topic (not a rewrite of an existing draft), pass the working title and the
one-line argument to `flypost_check_coverage`. A post the user already published outside Flypost
only shows up there. On `duplicate`, tell the user and pick a different angle together. On
`related`, read the neighbours and make sure this post says something they don't.

## 4. Ground it in their material

Search the Brain with `flypost_search_source_docs` for the facts, stories, examples and figures the
post needs. Run a few focused queries rather than one broad one. `flypost_search_brain` is slower and
billed: use it only when the documents came back thin.

- **Never invent a statistic, quote, client name or result.** Every number in the post comes from a
  source you found or from the user. If you cannot support a claim, say so and either drop it or
  ask the user for the real figure.
- First-hand detail beats general advice. If the post needs a story only the user knows (what
  happened, what they said, what it cost), ask them for it rather than making one up.
- `flypost_get_post_analytics` shows which of their posts earned reach. Glance at the top few when
  choosing a hook or format, so the new post looks like what already works for them.

## 5. Write it

Write the full post text: a hook that earns the "see more" click, a body that delivers on it, and an
ending that fits their voice (a question, a takeaway or a soft call to action). Keep to LinkedIn's
plain-text format: line breaks, no markdown, no bold.

Show the draft in the conversation and let the user react before saving if they are still shaping
it. If they asked you to just write and save it, save it.

## 6. Save it to Flypost

- New post: `flypost_create_draft` with `text`. To draft from an idea or concept already in Flypost,
  pass its `content_bank_item_id`, then set the text with `flypost_update_draft`.
- Existing draft: `flypost_get_draft` first, then `flypost_update_draft` with the full new text.
- Always pass `agent_name: "Claude"` and an `authoring_note` of one or two sentences on where the
  material came from (which Brain documents, what the user told you). The post editor shows both
  in its Sources panel, so the user can see who wrote it and from what.

The result shows a preview of the post as it will look on LinkedIn. Give the user its `editor_url`
too.

## 7. Score it

Run `flypost_score_authenticity` on the draft with `include_fixes: true`. If it flags the post as
generic, apply the rewrites that fit, and when a fix is a question for a missing first-hand detail,
ask the user that question instead of inventing the answer. Save the revision with
`flypost_update_draft`.

## Then

If the user wants a carousel, infographic or stat image to go with it, use the
`design-linkedin-visual` skill. To post it, use `schedule-linkedin-post`.

If a tool returns a plan error (no plan, or a plan that does not cover the action), tell the user
what it says, including the pricing link and the 7-day free trial when it mentions one. Do not retry
or work around it.
