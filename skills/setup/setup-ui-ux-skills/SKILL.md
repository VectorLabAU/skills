---
name: setup-ui-ux-skills
description: "Configure this repo for VectorLab UI/UX skills: aesthetic reference, banned anti-patterns, accessibility target, and microcopy voice. Run once before first use of the other UX skills."
title: UI/UX & Taste System Setup Wizard
category: setup
severity: hard-rule
disable-model-invocation: true
---

# Setup UI/UX Skills

Scaffold the per-project profile that the UI/UX skills assume:

- **Aesthetic reference** — Linear, Stripe, Apple Native, Raycast, or Custom
- **Banned anti-aesthetics** — glassmorphism, rainbow CTAs, cartoon empties, and related slop
- **Accessibility target** — WCAG 2.1 AA or AAA
- **Brand tone** — Utilitarian, Warm Humancentric, or Opinionated Direct

This is a prompt-driven skill, not a deterministic script. Explore, present what you found, confirm with the user, then write.

See [taste-archetypes.md](./reference/taste-archetypes.md) and [anti-patterns.md](./reference/anti-patterns.md) when explaining options.

## Process

### 1. Explore

Look at the current repo. Read whatever exists; don't assume:

- `.ux-profile.md` at the repo root (prior setup output)
- `AGENTS.md` and `CLAUDE.md` at the repo root — does either exist? Is there already a `## UI/UX skills` section?
- Design tokens, brand docs, `DESIGN.md`, `docs/brand/`, theme CSS variables
- Existing UI libraries or design-system folders

### 2. Present findings and ask

Summarise what's present and what's missing. Then take the four sections in order. One section, one answer, then the next.

Lead each section with the recommended answer so the user can accept it in a word.

**Section A: Aesthetic reference standard**

> Explainer: Downstream skills use this as the visual baseline for density, borders, spacing, and motion restraint.

Offer:

1. **Linear** — Monochrome, high density, sharp 1px borders, technical speed
2. **Stripe** — Refined typography, balanced depth, elegant data tables, high clarity (recommended default for most product UIs)
3. **Apple Native** — Generous spacing, unified radii, fluid transitions, neutral palettes
4. **Raycast** — Keyboard-first, ultra-compact, high contrast, pure utility
5. **Custom** — User provides reference URLs or principles

**Section B: Visual anti-aesthetic (things to aggressively ban)**

Propose this default ban list (from [anti-patterns.md](./reference/anti-patterns.md)):

- Gratuitous glassmorphism / `backdrop-filter` without a high-contrast boundary
- Floating pastel pill badges for ordinary metadata
- Arbitrary decorative gradients and neon glowing borders
- Multi-color radial rainbow gradients on standard CTAs
- Cartoon empty-state illustrations (people waving / high-fiving)
- Nested scrollbars and icon bloat inside inputs

Prompt: "Confirm this ban list or add/remove specific patterns."

**Section C: Accessibility target**

- **A — Strict WCAG 2.1 AAA:** Contrast > 7:1 for normal text, larger minimum touch targets (48×48px), prominent focus outlines
- **B — WCAG 2.1 AA (Balanced Taste):** Contrast > 4.5:1 for normal text, 3:1 for large text/borders, refined focus rings (44×44px targets) — recommended default unless the user asks for AAA

**Section D: Brand tone and microcopy voice**

1. **Utilitarian & Minimal** — Cold, precise, invisible (Linear / Stripe)
2. **Warm & Humancentric** — Clear, empathetic, supportive (Notion / Slack)
3. **Opinionated & Direct** — Punchy, editorial, concise (Basecamp)

### 3. Confirm and edit

Show a draft of:

- `.ux-profile.md` filled from [product-profile.template.md](../../config/product-profile.template.md)
- The `## UI/UX skills` block to add to `CLAUDE.md` or `AGENTS.md` (see step 4)

Let the user edit before writing.

### 4. Write

**Pick the file to edit for the pointer block:**

- If `CLAUDE.md` exists, edit it.
- Else if `AGENTS.md` exists, edit it.
- If neither exists, ask which one to create; don't pick for them.

Never create `AGENTS.md` when `CLAUDE.md` already exists (or vice versa); always edit the one that's already there.

If a `## UI/UX skills` block already exists, update it in place rather than appending a duplicate.

The block:

```markdown
## UI/UX skills

Taste, a11y, bans, and voice for this project live in `.ux-profile.md`.
Run `setup-ui-ux-skills` again only to change those defaults.
Before UI or microcopy work, read `.ux-profile.md`, then the matching domain skill (forms, dialogs, loaders, empty states, copy).
```

Then write `.ux-profile.md` at the project root using the template and the user's answers.

### 5. Done

Tell the user setup is complete. Summarise the active aesthetic, a11y level, voice, and ban list. Mention they can edit `.ux-profile.md` directly later; re-running this skill is only needed to restart the interview or switch standards.
