# midjourney-prompts

An agent skill for writing, reviewing and fixing prompts for Midjourney V8.x and Niji 7.

It helps the agent:

- pick between V8.2 and Niji 7 for the job
- write prompts you can paste as-is, with each reference image assigned to the right slot (Style Reference, Image Prompt, Attach to prompt)
- read a result and change as little as possible for the next round
- pick the cheapest edit route (Vary, Editor inpainting, Edit Model, Upscale)
- avoid parameters that no longer work (`--cref`, `--oref` on V8, `::` weights) and `--no` words that get prompts blocked

You still run Midjourney yourself; the skill never generates images.

## Install

```
npx skills add avienor/midjourney-prompts
```

Or copy this folder into your agent's skills directory (for Claude Code: `~/.claude/skills/midjourney-prompts/`).

## Files

- `SKILL.md`: the workflow
- `references/official.md`: facts from Midjourney's docs and release notes (checked 2026-10-04)
- `references/community.md`: unverified community tips, marked as such

Midjourney changes often. If something here is out of date, open an issue or a PR.
