# VectorLab UI/UX Skills

[![skills.sh](https://skills.sh/b/VectorLabAU/skills)](https://skills.sh/VectorLabAU/skills)

Binary, testable skills for AI coding agents. They push low-friction, high-taste interfaces — layout, interaction, microcopy, and feedback — across any frontend stack.

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

It writes `.ux-profile.md` at the project root and adds a short pointer in `CLAUDE.md` or `AGENTS.md`.

### 3. Build UI

Other skills load when the task fits (forms, dialogs, empty states, loaders, copy). Each one reads `.ux-profile.md` first when that file exists.

## Skills

### User-invoked

Reachable only when you ask for them (`disable-model-invocation: true`).

| Skill | Purpose |
| --- | --- |
| [setup-ui-ux-skills](./skills/setup/setup-ui-ux-skills/SKILL.md) | Configure taste, bans, a11y, and voice. Run once per project. |

### Model-invoked

Rich descriptions so the agent can reach for them when the task fits.

**Visual taste**

- [layout-geometry-and-grids](./skills/visual-taste/layout-geometry-and-grids/SKILL.md) — 4/8pt rhythm, optical alignment, line length
- [typography-and-hierarchy](./skills/visual-taste/typography-and-hierarchy/SKILL.md) — weights, scale steps, line-height
- [restrained-color-and-depth](./skills/visual-taste/restrained-color-and-depth/SKILL.md) — 60-30-10, borders before shadows
- [anti-ai-slop](./skills/visual-taste/anti-ai-slop/SKILL.md) — bans glassmorphism, rainbow CTAs, cartoon empties

**Interaction friction**

- [surface-routing-and-dialogs](./skills/interaction-friction/surface-routing-and-dialogs/SKILL.md) — slide-over vs page vs inline; destructive confirm
- [form-mechanics-and-validation](./skills/interaction-friction/form-mechanics-and-validation/SKILL.md) — blur validation, clickable submit
- [keyboard-and-focus-parity](./skills/interaction-friction/keyboard-and-focus-parity/SKILL.md) — full keyboard paths, focus rings, traps
- [smart-defaults-and-inference](./skills/interaction-friction/smart-defaults-and-inference/SKILL.md) — defaults and draft persistence

**Microcopy voice**

- [verb-first-actions](./skills/microcopy-voice/verb-first-actions/SKILL.md) — imperative CTAs, no OK/Submit
- [blameless-system-recovery](./skills/microcopy-voice/blameless-system-recovery/SKILL.md) — errors without blame
- [label-and-placeholder-discipline](./skills/microcopy-voice/label-and-placeholder-discipline/SKILL.md) — labels stay; placeholders are format hints

**State feedback**

- [latency-masking-and-loaders](./skills/state-feedback/latency-masking-and-loaders/SKILL.md) — 100ms / 1s thresholds, skeletons
- [empty-states-and-activation](./skills/state-feedback/empty-states-and-activation/SKILL.md) — actionable zero states

## Pre-flight taste audit

Before finishing UI work, check:

1. Anything on the banned anti-aesthetic list?
2. Modal where a slide-over or inline edit was required (&lt;10s rule)?
3. Destructive actions have explicit confirmation (entity named, destructive verb)?
4. Copy verb-first and free of user blame?
5. Validation fires on blur and clears on focus/edit?
