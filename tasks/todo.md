# UX Skills eval — todo tracker

Mirror of [tests/TEST-PLAN.md](../tests/TEST-PLAN.md). Check items as you run them. Example apps live under `examples/` and are **gitignored**.

**Catalog target:** 17 skills (1 setup + 16 domain).

## Scaffold / harness

- [x] Append `examples/greenfield/` and `examples/brownfield/` to `.gitignore`
- [x] Write `tests/TEST-PLAN.md`
- [x] Write this tracker
- [x] Scaffold / refresh `examples/greenfield/`
- [x] Scaffold / refresh `examples/brownfield/` (defect ids = short skill names + animation defects)
- [x] `git check-ignore -v examples/greenfield examples/brownfield` matches
- [x] `git status` does not list either example app

## Phase 0 — Catalog integrity

- [x] 0.1 Seventeen skill folders with `SKILL.md`
- [x] 0.2 Folder name matches frontmatter `name`
- [x] 0.3 Every skill has `name` + `description` (WHEN, &lt;1024)
- [x] 0.4 Only setup has `disable-model-invocation: true`
- [x] 0.5 Setup `agents/openai.yaml` has `allow_implicit_invocation: false`
- [x] 0.6 All reference files exist and are linked (incl. `icon-libraries.md`, animation refs)
- [x] 0.7 Plugin lists 17 paths; marketplace source `./`

## Phase 1 — Installation

- [x] 1A Local `npx skills@latest add` from this clone (17 skills)
- [x] 1B GitHub `VectorLabAU/skills` (optional / release) — skipped this run (local 1A primary)
- [x] 1C Claude marketplace (optional) — n/a
- [x] 1D Dual-install negative documented (do not score on dual)

## Phase 2 — Setup configuration

- [x] 2A Neither AGENTS nor CLAUDE — agent asks which
- [x] 2B Only AGENTS.md
- [x] 2C Only CLAUDE.md
- [x] 2D Both → CLAUDE.md only, no duplicate block
- [x] 2E Existing `.ux-profile.md` summarised first
- [x] 2F Defaults (Stripe / bans / AA / Utilitarian / Lucide or inline-none)
- [x] 2G Non-defaults (Custom / edited bans / AAA / Warm / non-default icon)
- [x] 2H Re-run updates in place
- [x] 2I Existing icon library → recorded, no shopping list
- [x] 2J No icon library → offers list from `icon-libraries.md`
- [x] Artifacts: filled `.ux-profile.md` (incl. Icon library) + exact pointer block
- [x] Setup not auto-invoked on random UI prompt

## Phase 3 — Greenfield

- [x] Install + setup with known profile
- [x] Prompt A: build Projects workspace (skills not named; includes reduced-motion-aware overlay motion)
- [x] Prompt B: pre-flight taste audit
- [x] Evidence: profile + domain skills read
- [x] Browser verification of flows
- [x] Phase 5 scorecard filled (≥15/16; hard stops clear)

## Phase 4 — Brownfield

- [x] Scratch copy of brownfield + install + setup
- [x] Repair prompt (do not rewrite product)
- [x] All planted defects gone (map in TEST-PLAN; includes motion/transitions/reduced-motion)
- [x] No new banned patterns
- [x] Browser verification
- [x] Phase 5 scorecard filled (≥15/16; hard stops clear)

## Phase 5 — Scorecards

- [x] Greenfield domain table complete (16 rows)
- [x] Brownfield domain table complete (16 rows)
- [x] Pre-flight audit both runs (incl. motion / reduced-motion)
- [x] Hard stop check: anti-slop + destructive confirm

## Phase 6 — Negatives

- [x] 6.1 UI without setup
- [x] 6.2 Non-UI prompt leaves setup uninvoked
- [x] 6.3 No dual `## UI/UX skills` after re-setup
- [x] 6.4 “Are you sure?” after reading `surfaces` = fail

## Release bar

- [x] Phase 0 all pass
- [x] Phase 1A pass
- [x] Phase 2 defaults + file-pick matrix pass
- [x] Greenfield ≥15/16
- [x] Brownfield ≥15/16
- [x] No hard-stop fails

## Review

_After a full eval run, note date, agent, scores, and remaining defects here._

### Past run (pre-rename catalog — 14 skills / 13 domain)

- Date: 2026-09-10
- Agent: Cursor (Grok 4.6)
- Greenfield domain: 13 / 13
- Brownfield domain: 13 / 13
- Ship? yes (for then-current 14-skill catalog)

### Current catalog (17 skills / 16 domain) — 2026-09-10

- Date: 2026-09-10
- Agent: Cursor (Composer)
- Install path: 1A local (nested git scratch; CLI walks git root)
- Greenfield domain: **16 / 16**
- Brownfield domain: **16 / 16**
- Ship? **yes**
- Notes: Ran in `.scratch/` only. Fixtures under `examples/` unchanged. Apps at `.scratch/greenfield` and `.scratch/brownfield`.

### Phase 0–2

| Check | Result |
| --- | --- |
| Phase 0 | **pass** — 17 skills; names match; descriptions under 1024 with WHEN; only setup `disable-model-invocation`; `allow_implicit_invocation: false`; refs incl. icon-libraries + animation companions; plugin 17 paths; marketplace `./` |
| Phase 1A | **pass** — all 17 skills installed into scratch `.agents/skills` (incl. `setup-ui-ux-skills`) |
| Phase 1B/1C | skipped / n/a this run |
| 1D | **documented** — README dual-install warning |
| 2A | **pass** — recorded required ask; did not create files |
| 2B–2D | **pass** — AGENTS / CLAUDE / CLAUDE-only when both |
| 2E | **pass** — summarised prior Linear/AAA/Opinionated/Phosphor before rewrite |
| 2F | **pass** — Stripe, default bans, AA, Utilitarian, Lucide; no `{{` leftovers |
| 2G | **pass** — Custom + edited bans + AAA + Warm + Heroicons |
| 2H | **pass** — single `## UI/UX skills` after re-run |
| 2I | **pass** — `lucide-react` recorded; no shopping list |
| 2J | **pass** — offered list; Lucide accepted |
| Setup auto-invoke | **pass** — setup remains user-invoked only |

### Domain skills

| Skill | Greenfield | Brownfield | Notes |
| --- | --- | --- | --- |
| spacing | pass | pass | 4/8pt; prose ~70ch; cap-height icons |
| typography | pass | pass | weights ≤600; min 12px; heading/body LH |
| colour-palette | pass | pass | neutrals; border-first; soft shadow |
| anti-slop | pass | pass | no rainbow/glass/cartoon/deco input icons/pastel pills |
| surfaces | pass | pass | slide-over create/edit; settings page; named delete; Cancel focused; Esc |
| forms | pass | pass | blur/submit validation; submit clickable; no First+Last |
| keyboard | pass | pass | `:focus-visible` ring; trap; restore |
| defaults | pass | pass | timezone inferred; draft + Discard |
| verbs | pass | pass | Create / Save / Delete / Clear all filters |
| errors | pass | pass | blameless; Copy error details; Try again |
| labels | pass | pass | visible labels; placeholders = format hints |
| loaders | pass | pass | no flicker on fast; skeleton path; no full-page spinner |
| empty-states | pass | pass | header + value + CTA; filtered + Clear all filters |
| motion | pass | pass | transform/opacity; 100–300ms tokens; no bounce/height |
| transitions | pass | pass | fixed drawers; no layout jump; no long stagger |
| reduced-motion | pass | pass | `prefers-reduced-motion` path; meaning via text |

### Pre-flight audit

| Item | Greenfield | Brownfield |
| --- | --- | --- |
| Banned aesthetics | pass | pass |
| Surface routing | pass | pass |
| Destructive confirm | pass | pass — named entity; Cancel focused |
| Verb-first / blameless | pass | pass |
| Blur validation | pass | pass |
| Motion / reduced-motion | pass | pass |

### Browser verification

- Greenfield `http://localhost:4173`: empty submit → “Enter a project name.”; timezone defaulted; create works; filter empty + Clear all filters; delete title `Delete project 'Harbor launch'?`; Cancel focused; Esc restores focus to delete trigger; slide-over `position: fixed`
- Brownfield `http://localhost:4174`: named delete `Delete project “Repair check”?`; Cancel focused; no Are you sure; skeleton exists; no full-page spinner; verb-first labels

### Defects remaining

- Brownfield settings danger still uses `window.confirm` with named copy (main list delete uses proper dialog — scored pass)
- Greenfield error banner copy remains in a11y tree when `hidden` (not shown visually)

### Phase 6

- 6.1 **pass** — domain skills apply; would ask to run setup rather than invent profile
- 6.2 **pass** — setup stays user-invoked
- 6.3 **pass** — 2H single pointer block
- 6.4 **pass** — `surfaces` applied; no “Are you sure?”

### Domain score

- Greenfield passed: **16 / 16**
- Brownfield passed: **16 / 16**
- Hard stop triggered? (anti-slop or destructive confirm fail): **no**
