---
name: ux-audit
description: "Audits the current UI working set against every installed VectorLab UX skill. Use before finishing UI work, when the user asks for a UX audit, pre-flight, or taste audit, or when reviewing a screen for skill compliance."
title: Pre-flight taste audit
category: audit
severity: hard-rule
---

# Pre-flight taste audit

Orchestrate a compliance pass over the current UI working set. Do **not** rewrite domain hard rules here — discover installed skills, read each matching `SKILL.md` Agent Checklist, score them, fix hard-rule fails, then report.

## When to run

- Before declaring UI work done (layout, styles, copy, overlays, forms, motion)
- When the user asks for a UX audit, pre-flight, or taste audit

## Process

### 1. Profile

If `.ux-profile.md` exists at the project root, read it.

If missing, continue with catalog defaults: Stripe aesthetic, default ban list from the setup skill’s anti-patterns reference, WCAG 2.1 AA, Utilitarian & Minimal voice. Note `profile missing — catalog defaults` in the report. Do **not** run `setup-ui-ux-skills`.

### 2. Working set

Name the scope: files changed this turn, plus any screen or path the user named. Unmentioned areas are out of scope for scoring (domain skills that only apply there → `n/a`).

### 3. Detect install root and discover domain skills

**Install root** (first match wins):

1. `.skills/`
2. `.agents/skills/` (or `.agents/` if `SKILL.md` files already live there)
3. `.cursor/skills/`
4. `.claude/skills/`

Rules:

- Reuse an existing tree. Never create a sibling `.skills/` next to an existing `.agents/skills/` (or the reverse).
- If more than one exists, prefer the first in the list that already contains VectorLab UX skills (`setup-ui-ux-skills` or `ux-audit`). Otherwise use the first existing root.
- If none exist, treat `.skills/` as the default consumer root (never a top-level `skills/` folder for installs).

**Discover skills:**

- Inside this catalog repo: use `.claude-plugin/plugin.json` as the canonical list (do not raw-walk `skills/` — leftover old-name folders may exist).
- In a consumer project: walk the detected install root; dedupe by frontmatter `name`.
- Always skip `setup-ui-ux-skills` and `ux-audit`.

### 4. Hard gate (always)

Score these seven checks against the working set (code-first; browser when tools exist for interactive/visual items):

1. Anything on the banned anti-aesthetic list?
2. Modal where a slide-over or inline edit was required (<10s rule)?
3. Single-field rename in a reserved box (next row does not move)?
4. Destructive actions have explicit confirmation (entity named, destructive verb)?
5. Copy verb-first and free of user blame?
6. Validation fires on blur and clears on focus/edit?
7. Motion uses only transform/opacity tokens, and reduced-motion is honored?

### 5. Domain skills

For every discovered domain skill:

- **Applicable** — working set touches that domain → read that skill’s Agent Checklist; score hard rules `pass` / `fail`; heuristics are notes only.
- **Not applicable** — mark `n/a` with a one-line reason. Never skip a skill silently.

### 6. Evidence

- Code-first for every check (read, grep, diff).
- Browser only when tools exist and the check is visual or interactive (0-shift rename, focus trap/restore, overlay routing, motion, reduced-motion).
- If there is no browser, list those rows under **Unproven** — do not mark them `pass`.

### 7. Fix and re-check

Hard-rule fails: fix in the same turn, then re-check those rows. Do **not** declare UI work done until hard-rule rows that were applicable and proven pass.

Heuristics and taste nits: report only; do not auto-fix unless the user asks.

### 8. Report (chat only — no file on disk)

```text
# UX audit
Scope: …
Profile: .ux-profile.md | missing — catalog defaults
Install root: .skills/ | .agents/skills/ | …

## Hard gate
1–7 pass/fail + evidence

## Domain skills
skill | pass/fail/n/a | evidence or reason

## Fixes applied
…

## Unproven
… (e.g. focus trap — no browser)
```
