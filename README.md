# VectorLab UI/UX Skills

[![skills.sh](https://skills.sh/b/VectorLabAU/skills)](https://skills.sh/VectorLabAU/skills)

Binary, testable skills for AI coding agents. They push low-friction, high-taste interfaces — layout, interaction, microcopy, feedback, and motion — across any frontend stack.

Modeled after the packaging and setup flow of [mattpocock/skills](https://github.com/mattpocock/skills). Content is framework-agnostic: CSS primitives, DOM state, and visual geometry — not React-, Vue-, or Svelte-specific APIs.

## Installation (30-second setup)

Pick **one** path. Installing both the Claude Code plugin and skills.sh copies leaves you with every skill twice.

### 1. Get the skills

<details>
<summary><strong>skills.sh (Cursor, Codex, and other agents)</strong></summary>

```bash
npx skills@latest add VectorLabAU/skills
```

Or from a local clone of this folder:

```bash
npx skills@latest add ./path/to/UX-Skills
```

Pick the skills you want, and which coding agents to install them on. **Make sure `setup-ui-ux-skills` is one of them.**

</details>

<details>
<summary><strong>Claude Code plugin (when published)</strong></summary>

```bash
# After the marketplace listing exists:
claude plugins install vectorlab-ux-skills
```

Or install from this repo as a local marketplace via `.claude-plugin/marketplace.json`.

</details>

### 2. Run `setup-ui-ux-skills`

In your agent, run it once per project. It will:

- Ask for an aesthetic reference (Linear, Stripe, Apple, Raycast, or Custom)
- Confirm a banned anti-aesthetic list
- Set an accessibility target (WCAG AA or AAA)
- Set brand tone for microcopy
- Detect an existing icon library, or help you pick one (Lucide recommended)

It writes `.ux-profile.md` at the project root and adds a short pointer in `CLAUDE.md` or `AGENTS.md`.

### 3. Build UI

Other skills load when the task fits (forms, surfaces, empty states, loaders, copy, motion). Each one reads `.ux-profile.md` first when that file exists.

## Skills

### User-invoked

Reachable only when you ask for them (`disable-model-invocation: true`).

| Skill | Purpose |
| --- | --- |
| [setup-ui-ux-skills](./skills/setup/setup-ui-ux-skills/SKILL.md) | Configure taste, bans, a11y, voice, and icons. Run once per project. |

### Model-invoked

Rich descriptions so the agent can reach for them when the task fits.

**Visual taste**

- [spacing](./skills/visual-taste/spacing/SKILL.md) — 4/8pt rhythm, optical alignment, line length
- [typography](./skills/visual-taste/typography/SKILL.md) — weights, scale steps, line-height
- [colour-palette](./skills/visual-taste/colour-palette/SKILL.md) — 60-30-10, borders before shadows
- [anti-slop](./skills/visual-taste/anti-slop/SKILL.md) — bans glassmorphism, rainbow CTAs, cartoon empties

**Interaction**

- [surfaces](./skills/interaction/surfaces/SKILL.md) — slide-over vs page vs inline; destructive confirm
- [forms](./skills/interaction/forms/SKILL.md) — blur validation, clickable submit
- [keyboard](./skills/interaction/keyboard/SKILL.md) — full keyboard paths, focus rings, traps
- [defaults](./skills/interaction/defaults/SKILL.md) — defaults and draft persistence

**Voice**

- [verbs](./skills/voice/verbs/SKILL.md) — imperative CTAs, no OK/Submit
- [errors](./skills/voice/errors/SKILL.md) — errors without blame
- [labels](./skills/voice/labels/SKILL.md) — labels stay; placeholders are format hints

**Feedback**

- [loaders](./skills/feedback/loaders/SKILL.md) — 100ms / 1s thresholds, skeletons
- [empty-states](./skills/feedback/empty-states/SKILL.md) — actionable zero states

**Animation**

- [motion](./skills/animation/motion/SKILL.md) — duration tokens, easing, property whitelist
- [transitions](./skills/animation/transitions/SKILL.md) — enter/exit for overlays and lists
- [reduced-motion](./skills/animation/reduced-motion/SKILL.md) — `prefers-reduced-motion` fallbacks

## Pre-flight taste audit

Before finishing UI work, check:

1. Anything on the banned anti-aesthetic list?
2. Modal where a slide-over or inline edit was required (&lt;10s rule)?
3. Single-field rename in a reserved box (next row does not move)?
4. Destructive actions have explicit confirmation (entity named, destructive verb)?
5. Copy verb-first and free of user blame?
6. Validation fires on blur and clears on focus/edit?
7. Motion uses only transform/opacity tokens, and reduced-motion is honored?
