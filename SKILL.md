---
name: midjourney-prompts
description: Write, review and fix prompts for Midjourney V8.x and Niji 7, which the user runs themselves on midjourney.com, nijijourney.com or Discord. Also reads a Midjourney result and says what to change, and picks the right edit route (Edit Model, Editor inpainting, Vary, Upscale). Use whenever an image is to be made in Midjourney or Niji (character art, a new pose or view of a character, a scene, a background, a style exploration), when the user shares a Midjourney image or prompt to improve, asks why a result came out wrong, asks which model, parameters or reference slots to use, or mentions MJ, Niji, --niji, --v 8, --sref, --sw, moodboard, stylize or style codes, even if they don't say "prompt".
---

# Midjourney prompts

The user runs Midjourney; you write the prompts, read the results, and decide the next step. You never generate the image yourself. A good prompt here is one the user can paste unchanged, with every reference already assigned to the right slot, and with a clear note about what to look for in the result.

Facts about models and parameters: `references/official.md`. Unverified tips: `references/community.md`. Read the official file the first time in a session you write a prompt; it is short, and Midjourney changes often enough that memory from training is likely out of date.

Before starting, check whether the project already has notes on this work: character facts, a style guide, earlier prompts and what they produced. Use them. Character facts come from the user or those notes. If a fact the image needs is not set (skin tone, hair length, an outfit colour), ask; don't invent it, because the model will draw whatever you write and it then looks decided. If the user wants prompts right away, fill the gaps with plain, neutral choices, list every one as an assumption to confirm, and leave out distinctive marks (scars, tattoos, eye colour quirks) nobody asked for.

## Talking to the user

Plain, short language, in the user's language, without jargon. Name a parameter only alongside what it does ("`--sw 300`: the reference's style is applied more strongly"). The user picks the references; you may propose candidates, labelled as suggestions.

## 1. Pick the model

| | Niji 7 | V8.2 |
|---|---|---|
| Looks like | Clean line, flat colour areas, illustration/anime. | Bolder, more rendered; can drift towards western comic or painterly. |
| Reads prompts | Very literally. Draws only what is written: no background unless named, mood words do little. | Fills gaps with its own taste; long, specific prompts work. |
| Same character again | No character reference. Repeat the same character block word for word, and use the same srefs. | Edit Model: attach up to 4 images of the character and describe the new scene or view. |
| Fixing parts | Region edit (Edit) on the niji site | Editor inpainting changes only the selected pixels |

Default to V8.2 when prompt adherence or a recurring character matters: it has the Edit Model for new views, outfit changes and scenes. Use Niji 7 for a flatter, cleaner anime or cel-shaded look. When unsure, run the same prompt on both, changing only the version flag, and let the user compare.

## 2. Write the prompt

### Niji 7

Order: framing and subject, then the fixed character block, then outfit, then pose and props, then setting, then light, then style words, then parameters.

```
full body character design of a <subject>, <character block>, <outfit as concrete nouns with their colours>, <pose and props>, <setting or "plain light grey background">, <light>, <style words> --niji 7 --ar 2:3 --s 100
```

- **Character block:** age, hair (colour, length, cut), eyes, expression, distinctive marks. Paste it unchanged into every prompt of a series; Niji 7 has no character reference, so the identical wording is what keeps the character recognisable.
- **Bind each colour to its object** ("crimson coat with gold trim, black gloves"). Niji 7 keeps them apart; a loose colour list gets spread over everything.
- **Name things, not moods:** "high-collared coat, brass buttons" works; "elegant, mysterious vibe" does almost nothing.
- **Full body:** name the footwear. **Background:** name it, or write "plain light grey background" for a cutout.
- **Fewer details:** "simple", "minimal", "flat shading". **More depth:** one light ("golden hour", "strong rim light from the left"), "painted", or "depth of field".

### V8.2

Write a natural description. The subject and the details that must survive go first; light and atmosphere go last.

```
<subject and action>, <setting>, <details that must stay exactly so>, <light and mood>, <style words> --v 8.2 --ar 2:3 --s 100
```

- Add `--raw` when it ignores details or adds its own flourishes.
- With the Edit Model, an instruction is fine: "show this character from behind, same outfit". Attach the image under "Attach to prompt". Use `--raw` for precision. If two characters' features mix up, put both in one reference image.
- To explore cheaply, use Draft mode (web): 24 small images for half the cost of one normal job; add `--sref random` to get 24 different styles. Then Vary the good ones.

### References

Tell the user which slot each image goes in; on the web they are dropped into the Imagine bar, not typed (Discord takes URLs).

- **Style Reference:** for art style only. With style refs, keep the prompt's style words few and in agreement with the refs ("bold black ink outlines, flat cel shading"). Words that pull another way get blended in. `--sw` 100 is the default; 200–400 applies the style more strongly.
- **Image Prompt:** copies content and composition. Don't use it for a style-only ref, or the ref's characters and outfits leak into the result.
- **Attach to prompt (Edit Model, V8.x):** the character or image to keep or edit.
- Few refs that agree beat many refs that conflict. Refs with headwear or props leak them.

### Parameters at a glance

`--ar 2:3` (portrait, full body) · `--s` 0–1000, lower = more literal · `--sw` 0–1000 · `--chaos 20–40` when the 4 images look the same · `--raw` = less house style · `--no a, b` for objects only · `--seed` only for A/B tests of one change, it does not keep a character · `--hd` for keepers only on V8.x.

Don't use `::` text weights (not supported on V8/Niji 7), `--cref`/`--cw` (gone), or `--oref` (V7 only). Never put clothing words in `--no`: each word is read separately, so "--no modern clothing" reads as "no clothing" and gets blocked. Describe the clothing you want instead.

## 3. Hand it over

For each prompt, give:
1. A short name and one line on what this variant tries.
2. The prompt in its own code block, ready to paste.
3. Model, which reference goes in which slot, and any setting to check (e.g. whether Personalization is on: when it is, the web silently adds `--p` to every prompt and shifts the style).
4. What to look for in the result.

If the project keeps prompts on disk, save them with the refs used, and when results come back add one line per prompt on what happened. Those notes are how the next round improves.

Mind the budget: GPU minutes are limited on every plan (Basic has 200 fast minutes a month, no Relax mode, and every image is public). A normal V8.x job costs about 0.8 min, HD 1.3, a Draft batch 0.4, an upscale about twice a job. Offer 3–5 prompts per round, not 20, and save HD and upscales for the keepers.

## 4. Read the result

When the user brings an image, a screenshot or a pasted prompt, look at the image and compare it with what was intended. Name what worked before what didn't. Then change as little as possible: one or two edits per round, so it stays clear what caused what. The exception is a prompt that is broken in several places at once (loose colours, a high `--s`, vague mood words): rewrite it in one go, list each change and the problem it targets, and go back to small steps from the next round.

| What you see | Likely cause | Change |
|---|---|---|
| Extra things nobody asked for (props, creatures, blood and grime on an "epic" prompt) | Model filling gaps (V8.2), or a high `--s` | Remove loose words, add "simple", lower `--s`, try `--raw` |
| A detail ignored or a colour on the wrong item | Detail buried late, or a loose colour list | Move it earlier, bind the colour to its noun, `--raw` (V8.2) |
| Style drifts from the refs | Conflicting style words, `--sw` too low, too many refs | Remove the conflicting words, `--sw 300`, fewer refs |
| Ref's character or outfit copied | Ref was in the Image Prompt slot | Move it to Style Reference |
| Not full body, or feet cropped | No footwear named, square ratio | Name the footwear, write "full body", `--ar 2:3` |
| Flat and lifeless (Niji 7) | Niji 7's flat default | One named light, "painted", or "depth of field" |
| Unwanted gradients or colours | Model's default palette | Name the palette ("limited palette of crimson, gold and black"), add the unwanted colour to `--no` |
| All 4 images nearly identical | Literal prompt following | `--chaos 30` |
| Wrong grip, extra fingers, a broken hand | Generation error, not the prompt | Fix it in place (section 5); rerolling wastes minutes |
| Prompt rejected | A clothing word in `--no`, gore words, or a brand, game or studio name | Remove the word, or describe the style instead of naming it |

If the problem is the design itself (the outfit isn't right for the character, the face reads wrong), say so and ask the user. That is a design decision, not something to fix with prompt tricks.

## 5. Pick the edit route

Start with the smallest tool that can do the job:

- **Nearly right, wants another take:** Vary (Subtle) on that image.
- **One spot is wrong** (a hand, a buckle, a sword grip): Editor on midjourney.com, or Edit on the niji site. Mark a bit more than the spot, so the model sees the surroundings. Write a short prompt naming only what should be there ("gloved hand gripping the sword hilt"). One spot per round. On V8.x only the marked pixels change, and the whole marked area gets filled: its outline becomes the new thing's outline (erasing old hair along its edge brings the same hair back). An HD image comes back as SD, so upscale it afterwards.
- **Same image, new view, pose, hairstyle or outfit change:** V8.2 Edit Model with the image attached and an instruction prompt, plus `--raw`; no mask. Add "Keep the face, … exactly the same" for what must stay.
- **Same character in a new scene:** V8.2 Edit Model with up to 4 images of the character, describing the scene.
- **Small hand or face glitch on a keeper:** try Upscale (Creative) first; it often cleans these up.
- **A precise change Midjourney keeps missing:** say so, and suggest finishing it in an image editor rather than burning more minutes on rerolls.

## Keeping this skill current

Midjourney ships changes every few weeks. When the user reports something that contradicts `references/official.md` (a parameter error, a missing slot, a new feature), believe the app, check the release notes (updates.midjourney.com, readable with a plain fetch), and tell the user which fact looks outdated.
