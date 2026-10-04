# Midjourney and Niji: official facts

Condensed from the official sources on 2026-10-02, re-checked against the docs and release notes on 2026-10-04. Midjourney changes monthly; when something here disagrees with what the user sees in the app, trust the app and update this file (see "Re-checking" at the end).

Sources: docs.midjourney.com (Help Center), updates.midjourney.com (release notes), nijijourney.com/blog and nijijourney.com/help-center.

## Contents

- Versions
- Prompt writing
- Parameters
- Image inputs
- Edit Model and Editor
- After generation: variations, remix, upscale
- Personalization, moodboards, style codes
- Plan limits and GPU cost
- Moderation
- Re-checking

## Versions

| | V8.2 (default) | Niji 7 |
|---|---|---|
| Released | 24 Jul 2026 | 9 Jan 2026 |
| Flag | `--v 8.2` (default, flag optional) | `--niji 7` |
| Character | "More creative, bold, sophisticated, edgy". Strongest when it relies on personalization, srefs and moodboards and on "longer, more specific prompting" (V8 alpha notes). | Anime/illustration model by Spellbrush. Very literal: "draws more of exactly what you want, nothing more, nothing less". Flatter default look, emphasis on clean line and large flat areas, less 3D rendering. "Vibey" prompts work worse than before. |
| Default background | Yes | No: plain or minimal unless you name one |
| Character consistency | Edit Model (up to 4 reference images) | No `--cref` ("won't be supported by niji 7"). Edit Model is documented for V8.1/V8.2 only. |
| Resolution | SD 1024 px square, 2:3 = 896x1344. `--hd` = 2048 px (2:3 = 1792x2688) | Smaller; use Upscale |

- V8.1 (14 Apr 2026) is still selectable. V7 remains for Omni Reference and Retexture.
- V8.x seeds are "99% identical".
- `--q 4` exists for V8 ("a little bit of extra coherence") but costs more; quality only affects the first grid.
- `--preview` runs unreleased test models; results may change over time.

## Prompt writing

General (Prompt Basics):
- Describe what you want to see, as a snapshot, not instructions ("Colored pencil illustration of bright orange California poppies", not "Show me a picture of… make them…").
- Specific words beat vague ones ("enormous" over "big"); numbers beat plurals ("three cats"); collective nouns help ("flock of birds").
- Say what you want, not what you don't: "no cake" in the text can add a cake. Use `--no` for exclusions.
- Fewer details = more variety, less control. Areas worth deciding: subject, medium, environment, lighting, color, mood, composition.
- The docs say "short and simple prompts typically generate the best images", but the V8 release notes say V8 "shines… when you trend towards longer more specific prompting", and Niji 7 needs explicit detail. Use short prompts only when variety is the goal.

Niji 7 (Niji 7 Prompting Guide, Jan 2026):
- Precision: attributes stay bound to their nouns ("red dress with blue frills and a white belt": the belt stays white, the frills blue). "More exciting prompts lead to more exciting pictures."
- Background: none by default. If you don't have one in mind, "indoors" or "outdoors" is enough.
- Full body: name the footwear ("wearing boots").
- Less detail: "minimal", "simple", "flat shading".
- Less flat: a strong light ("golden hour"), a rendered style ("painted"), or a camera word ("depth of field").
- "anime screenshot" shows off the line work; "minimalist graphic logo" for logos.
- Less anime: `--raw`.
- More different images in the grid: raise `--chaos` (web: "Variety"), e.g. `--chaos 40`.
- Older-model look: generate in the older model, then use that image as sref with the same prompt in Niji 7.

Text in images: put it in double quotes, keep it short, add "with the words" / "written" / "sign saying". Raw or lower stylize helps.

Edit Model prompts may be instructions ("make this girl into a real character", "let's see this image from behind"); normal prompts are descriptions.

## Parameters

Rules: parameters go at the very end, one space before `--`, no punctuation after values, no prompt text after them.

Web settings panel (seen 2026-10-02): "House style" is the Stylize slider (10% = `--s 100`; release notes: "House style works without Raw"). "Inspiration only" in the Images panel is the Image Prompt slot, "Reference style" the Style Reference slot. Parameters typed in the prompt override the panel.

| Parameter | Range / default | Notes |
|---|---|---|
| `--ar W:H` | default 1:1 | Max 14:1 (4:1 for HD). Edit Model matches the first image's ratio unless `--ar` is given; edits on alpha keep the base ratio. |
| `--s` / `--stylize` | 0–1000, default 100 | Low = literal, high = more artistic freedom, may drift from prompt. With personalization or moodboards it sets how strongly they apply. |
| `--raw` | on/off | Turns off the default styling "auto-pilot". More literal; with simple prompts more photographic. Recommended with the Edit Model for precision. |
| `--c` / `--chaos` | 0–100, default 0 | Variety between the 4 images. |
| `--w` / `--weird` | 0–3000, default 0 | Experimental strangeness; not fully seed-compatible. |
| `--no a, b` | | Same as weight -0.5. Each word is read separately (see Moderation). |
| `--seed N` | 0–4294967295 | Only fixes the starting noise. Does not keep a character or style across prompts. Unreliable in Turbo. |
| `--sref` | image or code | Style reference. `--sref random` picks a code. Several codes can be mixed. |
| `--sw` | 0–1000, default 100 | Style weight. Not compatible with moodboards. |
| `--sv` | version | Style reference version (Niji 7 accepts `--sv 4` and `--sv 6`). Not with moodboards. |
| `--iw` | V8.1/V7: 0–3, Niji 7: 0–2, default 1 | Image prompt weight. |
| `--p [id/code]` | | Personalization profile or moodboard. Bare `--p` = your defaults. |
| `--hd` / `--sd` | | V8.1+ resolution. HD 1.3 min GPU, SD 0.8 min. |
| `--draft` | | V8.1/V8.2 (web): 24 images at 512 px for 0.4 min. Vary/Remix a draft to render it full size. With `--sref random`, each of the 24 gets a different style code. (The Version page's comparison chart still marks Draft as unsupported on V8.x; the release notes of 16 Jun 2026 and later say otherwise, and the app has it.) |
| `--exp` | V7, V8.1, V8.2 | Marked supported in the Version page's comparison chart; can be pinned as a folder default on the web. Range and effect are not documented; see community notes. |
| `--q` | 1, 2, 4 | GPU time multiplier. |
| `--r` / `--repeat`, `{a, b}` permutations | | Basic plan: max 4 jobs. Permutations need Fast/Turbo. |
| `--tile` | | Seamless patterns; seams fixed for V8.1/V8.2 on 24 Sep 2026. Not with the Edit Model. |
| `--edit` | | Discord form of the Edit Model. |

Multi-prompts with `::` and per-part weights are documented only for versions up to 6.1 and Niji 6. Don't rely on them for V8 or Niji 7 text. (`--sref code::1` style weights on codes are a different thing and do work.)

Legacy, not for current models: `--cref`, `--cw` (V6/Niji 6), `--oref`, `--ow` (V7 only; in V8.x replaced by the Edit Model), `--stop`, `--style` codes.

## Image inputs

On the web the user drops images into slots in the Imagine bar; they are not written into the prompt text (Discord takes URLs). The slots:

| Slot | What it takes from the image | Use for |
|---|---|---|
| Style Reference | Look only: colors, medium, texture, lighting. "Doesn't copy objects or people." | Matching an art style |
| Image Prompt | Content, composition and colors, as inspiration | Composition or color starting point. It copies content, so don't use it for style-only refs. |
| Attach to prompt (Edit Model reference) | The actual subject: a character, object, or the image to edit | Keeping a character, editing an image, combining up to 4 images |
| Moodboard (`--p mID`) | A broader aesthetic from many images | A wider style than one sref; no `--sw` |

Style reference best practice (official):
- Keep the text prompt simple; avoid style words that conflict with the reference.
- If the style is hard to reach, add words that describe the reference's style.
- Describe content, not instructions about the reference: "ballpoint pen sketch of a bunny", not "copy this style and make a bunny".

With the Edit Model, the docs add: describe the style in the prompt when using srefs or moodboards, to "activate" the aesthetic more consistently.

## Edit Model and Editor

The Edit Model (V8.1/V8.2, released 27 Aug 2026) does three things:
1. Edit an existing image from written instructions.
2. Generate new images from up to 4 reference images (replaces Omni Reference and Character Reference). Multiple characters work; if their features mix up, combine the characters into one reference image.
3. Inpaint (change a selected area) and outpaint (extend the canvas) in the Editor.

Also: change the view ("let's see this image from the front / from behind"), retexture into another style (with sref/moodboard/personalization), works with image prompts and `--hd`. Not with `--tile`; Edit results don't work with Remix. `--raw` gives more precise control.

Since 24 Sep 2026: targeted edits change only the selected pixels, so repeated edits don't degrade the image.

Editor (midjourney.com): Erase brush and Smart Select mark the area; Restore brush undoes; Move/Resize changes canvas and ratio; Layers combine images (only transparent areas regenerate). Inpainting or outpainting an HD image returns SD; upscale afterwards.

Inpainting tips (Vary Region page): a larger selection gives more context but may replace things you wanted to keep; keep the area prompt short and direct ("meadow stream", not "please change the trail into a stream"); change one area at a time.

Niji: the niji site has an "Edit" button for region edits with an optional new prompt. The alpha changelog (2 Sep 2026) notes "Niji 7 + inpainting now works correctly".

## After generation: variations, remix, upscale

- Vary Subtle (small changes) / Strong (same idea, new visuals).
- Remix: edit the prompt while varying. Only ar, no, stop and tile change through Remix; changing ratio this way stretches the image (use Pan/Zoom/Editor instead).
- Upscale Subtle keeps the image; Creative adds detail and "can sometimes help correct small issues… like awkward hand positions or odd facial expressions". Upscales cost about twice a generation. HD images can't be upscaled further.

## Personalization, moodboards, style codes

- Personalization learns taste from images the user picks. The V7 Global profile works in V8.1/V8.2; there is no Global V8 profile yet. Niji has its own Global Niji V7 profile (profiles are per model; Midjourney ratings don't affect Niji).
- Moodboards: a set of uploaded images, used as `--p mID`. No `--sw` or `--sv`.
- Style codes: `--sref <number>`. Style Explorer (Explore → Styles) to browse; Style Creator to build a code by picking from grids (on Niji, switch its version to Niji 7 first). Liked codes don't change personalization.
- Style Creator (midjourney.com only; Help Center article "Style Creator", read 2026-10-02): the prompt only makes the preview images, it does not steer the creator; refs and style words in it shape the previews, not the code. You click grid samples by style, not content. It learns from what you pick and what you leave unpicked in a round; scrolling past without picking is a skip and has no effect. The samples move closer to your taste as you pick: early rounds look random, most styles settle after 5–10 rounds, 10–15 add detail, past 15 little changes. Every preview round costs GPU time; `--draft` in the prompt makes previews cheaper. A closed session cannot be reopened; each preview round's code is saved on the Create page. The article says previews use V7, but the app offers V7/V8.1/V8.2 (no Niji). To get the preview look later, use the code with the same refs and prompt words (plus any code the prompt already had).
- With personalization or moodboards, `--s` controls how strongly they apply.
- Style previews (web, Sep 2026): the Styles sidebar can preview the current prompt across liked and featured styles ("Live previews"); clicking a thumbnail generates with that style. Useful for picking a code before spending a full job.

## Plan limits and GPU cost

Basic ($10/month): 200 Fast minutes, no Relax mode, no Stealth (all creations are public on the website), 3 concurrent jobs, max 4 repeat/permutation jobs. Extra time: $4/hour. Standard ($30): 15 h Fast plus unlimited Relax images.

Approximate cost per job: V8.x SD 0.8 min, HD 1.3 min, Draft 0.4 min for 24 images; upscale about 2x a generation; `--q 2`/`--q 4` multiply.

## Moderation

- `--no` reads each word on its own: "--no modern clothing" becomes "no modern" and "no clothing" and can trigger a warning. Never put clothing words in `--no`; describe the clothing you want instead.
- Niji rejects prompts with clothing in negatives, gore or sexual-abuse terms, and "terms that might potentially infringe on well-known copyright holders". A game or studio name in a style phrase can be rejected; if it is, describe the style instead.
- Keep a balance of positive and negative terms; too many negatives can stop generation.

## Re-checking

docs.midjourney.com and nijijourney.com block plain fetches (403); open them in a real browser (a browser-automation tool, if you have one). updates.midjourney.com (release notes) works with `curl`. Useful pages: Version, Parameter List, Edit Model, Style Reference, and the Niji blog (nijijourney.com/blog).
