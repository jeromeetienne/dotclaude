---
description: Generate a LinkedIn-ready slide deck (.slides.md + .slides.pdf) from a .article.md
argument-hint: <path/to/file.article.md>
---

# Generate LinkedIn slide deck from an article

You are converting a long-form `.article.md` into a polished, swipe-friendly **LinkedIn carousel deck** exported as PDF.

## Input

The user passes a path to a `.article.md` file as `$ARGUMENTS`.

If `$ARGUMENTS` is empty:

- Ask the user which article to use.
- Suggest the most recently modified `*.article.md` file under `docs/`.

Derive the basename by stripping `.article.md`.

Write outputs next to the source article:

- `<basename>.slides.md` — Marp slide source
- `<basename>.slides.pdf` — final PDF for LinkedIn carousel upload

Do not leave temp files behind. Only these two outputs should remain.

## Step 1 - Read and extract source signals

Read the full article and extract:

- Title (H1)
- Core promise: one sentence that states what the reader gets
- Audience: who this helps and in which scenario
- 5-9 strongest insights from the article (facts, design choices, tradeoffs, concrete tips)
- Any concrete names/tools/libs/frameworks mentioned
- Any numbers or constraints worth preserving
- A final CTA link (article URL, repo URL, or canonical destination)

Rules:

- Do not invent claims, numbers, or benchmarks.
- Every slide claim must trace back to the article.
- If the article is thin, prefer fewer stronger slides over filler.

## Step 2 - Build a LinkedIn-native slide narrative

Create a clear story arc optimized for mobile swiping:

1. Hook
2. Why this matters
3. Core problem
4. Key insights (multi-slide sequence)
5. Practical application
6. Recap
7. CTA

Target **10-14 slides** total.

Per-slide writing constraints:

- One core idea per slide
- Max ~35 words per slide (except title and CTA)
- Prefer short lines over dense paragraphs
- Use concrete language over abstractions
- Keep an opinionated, technical-but-readable tone

LinkedIn tone:

- No hype words like "game-changer", "revolutionary", "thrilled"
- No hashtag spam inside slides
- Sound like an experienced engineer sharing practical lessons

## Step 3 - Write `<basename>.slides.md` as a Marp deck

Generate a complete Marp markdown file.

Use this structure:

1. YAML frontmatter with Marp enabled
2. A custom inline `<style>` block defining theme variables and slide styling
3. Slide content separated with `---`

Required frontmatter:

```yaml
---
marp: true
paginate: true
size: 4:5
---
```

Design goals (LinkedIn carousel):

- Format: 4:5 portrait (best for LinkedIn feed)
- Visual style: bold, technical, clean
- Strong contrast and mobile readability
- Large typography with generous spacing
- Consistent accent color and visual rhythm

Typography guidance:

- Title slides: very large and punchy
- Body slides: concise text, readable at phone size
- Avoid tiny captions and dense bullet walls

Slide composition guidance:

- Title slide: strong hook + short subtitle
- Insight slides: short headline + 2-4 bullets max
- Occasional emphasis slide with one powerful sentence
- Final slide: clear CTA with link

Recommended section labels in small uppercase:

- CONTEXT
- PROBLEM
- INSIGHT
- TRADEOFF
- APPLY
- RECAP
- NEXT STEP

## Step 4 - Export PDF

Export `<basename>.slides.md` to `<basename>.slides.pdf`.

Preferred method:

1. Use the built-in Marp export capability.
2. If unavailable, run Marp CLI from terminal (for example via `npx @marp-team/marp-cli`).

Example fallback command:

```sh
npx --yes @marp-team/marp-cli "<basename>.slides.md" --pdf --allow-local-files -o "<basename>.slides.pdf"
```

## Step 5 - Validate output quality

Before finishing:

- Confirm both files exist.
- Confirm PDF is non-empty and has the same slide count as the markdown deck.
- Quickly review slide flow for clarity and no obvious truncation.

If export fails, report the exact failure and what was attempted.

## Step 6 - Final response format

In your final response to the user, include:

- Number of slides generated
- Output file paths as clickable markdown links
- 1-2 lines summarizing the narrative angle chosen

Do not paste the full slide deck in chat unless explicitly requested.

## Things to avoid

- Copying long article paragraphs into slides
- More than 14 slides unless the user asks for depth
- Walls of bullets or code-heavy slides
- Weak CTA like "thanks" with no next action
- Decorative visuals that reduce readability
