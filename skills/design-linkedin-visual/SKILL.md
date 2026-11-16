---
name: design-linkedin-visual
description: Make a branded LinkedIn carousel, infographic, striking stat image or before-and-after comparison image with Flypost Designer, from words you write and the user's own figures, screenshots and images. Use when the user asks for a carousel, slides, a PDF post, an infographic, a stat graphic, a comparison image, or to turn a post or idea into a visual, or to change one.
---

# Design a carousel, infographic or stat post with Flypost Designer

The split of work: **you write every word** on the visual, and **Flypost Designer lays it out** in the
user's brand (colours, fonts, logo or LinkedIn profile in the footer). Designs here are layouts of
text, charts, logos, the user's own images, product and website screenshots and stock photos.

## 1. Pick the format

| The post is... | Format | What you write |
|---|---|---|
| a list, a how-to, a framework, a story in steps | `carousel` | 5 to 10 slides: hook, body slides, recap, call to action |
| several figures, a numbered list or ordered steps on one page | `infographic` | `infographic_style` (`stats`, `list` or `how_to`) and the matching `infographic_copy` |
| one number that is the whole point | `striking_stat` | `image_copy.stat` (a one-line claim with the number in it) and an optional `label` |
| an old way against a new way | `comparison` | `image_copy.before`, `image_copy.after`, optional `header` |

Memes, product scenes and "Let AI decide" image posts are not made through this connection. If the
user wants one, save the concept and give them its `editor_url` to finish it in the Flypost app.

## 2. Gather the words and the facts

If no project is active, call `flypost_list_projects` and `flypost_use_project`. Then
`flypost_get_writing_voice` and `flypost_get_brand_kit`, and `flypost_search_source_docs` for the
figures and examples the visual needs.

**Every figure on a visual must come from a source or from the user.** A number on a slide is read
as fact. If you cannot support one, leave it out or ask.

Write for the format: short lines, one idea per slide, the hook slide a promise the deck keeps. A
`striking_stat` hero line is a complete claim, such as "92% of buyers stop replying after the
first call", never a bare figure, and its number is your conclusion, never a figure you are
arguing against.

## 3. Save the concept

`flypost_save_concept` with `target_format` (`carousel`, `infographic` or `single_image`), a `title`,
an `angle`, and the words:

- carousel: `slides`, each with a `role` (`hook`, `rehook`, `body`, `recap`, `cta`) and a `title`,
  plus `body`, `example`, `points` (recap) or `actions` (cta) as the slide needs.
- infographic: `infographic_style` and `infographic_copy`. Every figure and line the graphic shows
  goes in the copy. The angle is not drawn on the visual, so a number left only there is lost.
- single image: `image_substyle` (`striking_stat` or `comparison`) and `image_copy`.

Pass `content_bank_item_id` to fill in an idea that already exists (from the idea board); leave it
out to create a new one. Pass `agent_name: "Claude"` and an `authoring_note`, and `sources` for
the material you used.

## 4. Design it

`flypost_design_visual` with the concept's `content_bank_item_id` and `format` (`carousel`,
`infographic`, `striking_stat` or `comparison`). It takes one to five minutes and comes back
finished; a carousel comes back as a whole deck with its PDF. The result renders in Claude.

- `direction`: only when the user gave art direction ("dark background, lots of space around the
  number").
- `options`, only when the user wants them: `more_visual`, `big_number`, `product_screenshot`,
  `website_screenshot` (name the page in `direction`), `stock_photo`, `logos`.
- **The user's own screenshot or image.** It must be in Flypost storage first: a product screenshot
  already in the brand kit (`flypost_get_brand_kit`, `product_screenshots`), an image from
  `flypost_list_media`, or a new one filed with `flypost_upload_logo` and `asset_type`
  `product_reference`. Pass up to three in `images`, and add the `product_screenshot` option for a
  laptop or phone frame ("in a phone" in `direction` for a phone). With the option and no images,
  Designer picks a brand-kit screenshot itself, which can be one showing a client's work, so check
  which one it used.
- Only ever put an image on a visual that the user actually gave you or that is already in their
  project.

Each design is a run on the user's image allowance. Designing again replaces the design, so do not
re-design to fix something.

## 5. Check it, then change it in small steps

Look at the result with `flypost_view_visuals` (seconds, nothing renders). Check: on brand,
readable, no cut-off or garbled text, numbers exactly as written, the logo shown once, the right
screenshot. Never render a PDF just to look.

To change it, `flypost_revise_design` with one clear change per call ("make the 11% much bigger",
"change slide 3's headline to ..."). `flypost_undo_design_revision` brings the previous version
back. Look again with `flypost_view_visuals` after each change.

## 6. Hand it over

Give the user the `editor_url`. To post it, the visual needs a draft with a caption:
`flypost_create_draft` with the concept's `content_bank_item_id`, then `flypost_update_draft` with
caption text you wrote in their voice (see the `write-linkedin-post` skill for grounding and
scoring). Then use `schedule-linkedin-post`. A carousel's PDF re-renders by itself when the post is
scheduled.

## Template carousels

Only when the user asks for Flypost's carousel templates rather than a designed deck: save the
concept with `slides`, then use `flypost_switch_carousel_template`, `flypost_edit_slides` for the
words, `flypost_upload_slide_image` for the user's images, and `flypost_carousel_logo` for the logo.
`flypost_build_carousel` makes the PDF, which is needed only to schedule it or when the user wants the
file. `flypost_guide` with topic `images` is the full reference for these tools.
