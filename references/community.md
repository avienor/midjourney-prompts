# Community notes (not official)

Tips from blogs and newsletters, gathered 2026-10-02. None of this is in Midjourney's docs. Treat each item as something to try, not a rule, and say so when you use one. Much community material online is older and still recommends `--cref`, which current models don't support; ignore it.

## `--exp` (V7 and later)

Sources: Midjourney's announcement as relayed by several users on X/Threads (2025), geekycuriosity.substack.com.

- Range 0–100, default 0. Suggested values 5, 10, 25, 50; the visible change is mostly between 5 and 50.
- Adds detail, dynamism, texture, a "tone-mapped", punchier look.
- Higher values lower prompt fidelity and grid variety, and above about 50 can overpower `--s` and `--p`.

For flat cel-shaded art, extra texture and tone mapping usually work against the look. Leave it off unless the image feels dull.

## V8.x

Source: blakecrosley.com, "Midjourney V8 Prompting" (Mar 2026, updated Aug 2026). Partly written before the Edit Model shipped.

- Longer, specific prompts work better than in V7; spatial relations in multi-subject scenes hold up.
- Words near the start of the prompt seem to weigh more ("front-loaded"). Put the subject and the must-keep details first.
- Suggested structure: subject and action, environment, specific details to preserve, lighting and atmosphere, then parameters.
- The author recommends `--s 1000` with a trained personalization profile. Without a profile that just means more default Midjourney style.
- Text renders well in double quotes with 2–4 words; full sentences degrade.
- Personalization starts working at about 40 ratings, settles around 200, keeps improving up to about 2,000.

Other guides (vidmuse.ai, gradually.ai): V8.2 looks most "designed" at `--s 500–800`; `--s 100–200` is cleaner and more literal.

## Niji 7

Sources: geekycuriosity.substack.com (Jan–Feb 2026), Medium write-ups.

- Prompt skeleton: subject (age, hair colour and cut, eye colour), outfit and props as named garments, setting and time (a place and a light), drawing style.
- "Describe the thing, not the vibe": mood words ("dreamy", "cinematic") do little until the structure is there.
- Placement words work ("dog on the left, cat on the right").
- Sref codes give cleaner results on Niji 7 than the same codes on V7. Both `--sv 4` and `--sv 6` work. A single code gets `::1` by default.
- The 4 images in a grid look alike because of the strict prompt following; use `--chaos` for range.
- Image reference weight range is narrower than Midjourney's.
- A secondary source says personalization and moodboards arrived on Niji 7 on 26 Feb 2026. The Niji help center does list a "Global Niji V7 Profile".

## Character sheets and turnarounds

Sources: various 2025–2026 guides; mostly written for older versions.

- For a turnaround, keep the wording and parameters identical and change only the view phrase ("front view", "three-quarter view", "side view", "back view"); neutral expression, full body, flat background. On V8.2 the Edit Model's "show this character from behind" is the more reliable route.
- "character reference sheet of …, multiple expressions" is the phrase the Niji team itself used (Niji blog, Mar 2025, Niji 6).
