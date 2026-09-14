# UX Skills eval — todo tracker

Mirror of [tests/TEST-PLAN.md](../tests/TEST-PLAN.md). Product build contract: [tests/WORKSPACE-SPEC.md](../tests/WORKSPACE-SPEC.md). Check items as you run them. Example apps live under `examples/` and are **gitignored**.

**Catalog target:** 20 skills (1 setup + 1 audit + 18 domain). `viewports` landed. Harbor scratch wiped 2026-09-14 — retest next eval.

## Viewports skill (2026-09-14)

- [x] Add `skills/visual-taste/viewports` (hard rules + `breakpoint-tokens.md`)
- [x] Narrow line on each `page-patterns` catalog pattern + marketing
- [x] Wire `ux-audit` hard gate, setup pointer, profile agent rules
- [x] Register in plugin.json + README + brief.md
- [x] Update TEST-PLAN counts (20 / 18 domain), Phase 6.7, Harbor plants + 375px verify

### Review

Agents were shipping desktop-only shells. `viewports` is the global contract (overflow, chrome, hit targets, tap-first). Per-pattern stacking stays in the catalog. Harbor eval not re-run in this change.

---

## Notion taste profile (2026-09-14)

- [x] Add Notion first-class profile + collapse map to `taste-archetypes.md`
- [x] Wire Section A in setup `SKILL.md` (Notion = 5, Custom = 6)
- [x] Template enum, motion timings, type-scale mapping
- [x] README, brief.md, TEST-PLAN (2K/2L)

### Review

Profiles stay product vibes. Notion is the only new peer. Famous lookalikes and design systems collapse via the agent-only map — not extra Section A options.

---

## Harbor fixture spec (2026-09-14)

- [x] Write `tests/WORKSPACE-SPEC.md` (IA, data, 10 patterns + auth, overlays, skill contracts, prompts, brownfield plants, browser script)
- [x] Point `tests/TEST-PLAN.md` Phase 3/4/5, recreation specs, and browser verification at Harbor
- [x] Rebuild `examples/greenfield/` from `WORKSPACE-SPEC.md` §9 (empty shell only)
- [x] Rebuild `examples/brownfield/` from `WORKSPACE-SPEC.md` §10 (all routes + skill + pattern plants)
- [x] Re-score `page-patterns` on next greenfield + brownfield eval (was `—` / not scored)
- [x] Full Harbor browser verify script (`WORKSPACE-SPEC.md` §11) on both apps

### Review

Harbor expands the eval product so every domain skill is applicable, including all ten page patterns via separate record types (projects list, tasks board, calendar events, etc.). Spec is tracked; example app trees stay gitignored until rebuilt for a run.

**Eval run 2026-09-14:** fixtures rebuilt; scored builds under `.scratch/harbor-*`. Domain **17/17** both sides. Ship for then-current 19-skill catalog.

---

## Harbor reset for `viewports` (2026-09-14)

- [x] Wipe `.scratch/harbor-greenfield`, `.scratch/harbor-brownfield`, `.scratch/install-1a-harbor`
- [x] Restore `examples/greenfield/` empty shell (README + index + stubs)
- [x] Keep `examples/brownfield/` planted fixture (do not use repaired scratch)
- [ ] After `viewports` skill lands: bump catalog counts (20 skills / 18 domain) in TEST-PLAN, WORKSPACE-SPEC, plugin, README
- [ ] Add `viewports` hard-rule checks + brownfield plant(s) to WORKSPACE-SPEC
- [ ] Fresh Phase 0–1 + Harbor greenfield build + brownfield repair + browser verify
- [ ] Scorecard: __ / 18 domain both sides

### Review

Scored Harbor apps cleared so the next eval starts from fixtures only. Do not re-score until `viewports` is in the catalog and the workspace spec includes it.


---

## Page patterns skill (2026-09-11)

- [x] Study shadcnstudio-blocks screenshots (app pages vs chrome vs marketing sections)
- [x] Keep the ten locked product patterns; auth → Form; marketing → composed sections
- [x] Add `skills/interaction/page-patterns` (decision tree + catalog + marketing refs)
- [x] Hard rule: name the pattern before any page markup
- [x] Wire into setup pointer, profile template, `surfaces`, `ux-audit` hard gate
- [x] Register in plugin.json + README
- [x] Update TEST-PLAN counts (19 / 17 domain) and Phase 6.6

### Review

Screenshot folders informed the catalog. Product pages map to the ten patterns. Shells, widgets, dialogs, and empty blocks are not pages. Public marketing is a route type plus stacked sections — not an eleventh product pattern. Auth is Form (auth). Images were not copied into this repo (copyright + size).

---

## Eval tracker

## Scaffold / harness

- [x] Append `examples/greenfield/` and `examples/brownfield/` to `.gitignore`
- [x] Write `tests/TEST-PLAN.md`
- [x] Write `tests/WORKSPACE-SPEC.md` (Harbor product contract)
- [x] Write this tracker
- [x] Scaffold / refresh `examples/greenfield/` *(pre-Harbor thin shell — rebuild from WORKSPACE-SPEC)*
- [x] Scaffold / refresh `examples/brownfield/` *(pre-Harbor — rebuild from WORKSPACE-SPEC)*
- [x] Rebuild both example apps from Harbor `WORKSPACE-SPEC.md`
- [x] `git check-ignore -v examples/greenfield examples/brownfield` matches
- [x] `git status` does not list either example app

## Phase 0 — Catalog integrity

- [x] 0.1 Twenty skill folders with `SKILL.md`
- [x] 0.2 Folder name matches frontmatter `name`
- [x] 0.3 Every skill has `name` + `description` (WHEN, &lt;1024)
- [x] 0.4 Only setup has `disable-model-invocation: true`
- [x] 0.5 Setup `agents/openai.yaml` has `allow_implicit_invocation: false`
- [x] 0.6 All reference files exist and are linked (incl. `breakpoint-tokens.md`)
- [x] 0.7 Plugin lists **20** paths (incl. `viewports`); marketplace source `./`

## Phase 1 — Installation

- [x] 1A Local `npx skills@latest add` from this clone (19 skills; Cursor agent → `.agents/skills/`; nested git scratch; lockfile present; no second tree)
- [ ] 1B GitHub `VectorLabAU/skills` (optional / release)
- [ ] 1C Claude marketplace (optional)
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
- [ ] 2K Collapse map (Vercel → Linear; Material → Custom; never invent standard names)
- [ ] 2L Notion as valid Section A pick
- [x] Artifacts: filled `.ux-profile.md` (incl. Icon library) + exact pointer block
- [x] Setup not auto-invoked on random UI prompt

## Phase 3 — Greenfield

- [ ] Install + setup with known profile *(Harbor / WORKSPACE-SPEC — retest after `viewports`)*
- [ ] Prompt A: build Harbor from jobs (all 11 routes; skills/patterns not named)
- [ ] Prompt B: run `ux-audit`
- [ ] Evidence: profile + domain skills read; pattern names before each page’s markup
- [ ] Browser verification (`WORKSPACE-SPEC.md` §11)
- [ ] Phase 5 scorecard filled (≥ release bar; hard stops clear; incl. `viewports`)

## Phase 4 — Brownfield

- [ ] Scratch copy of Harbor brownfield + install + setup
- [ ] Repair prompt (do not rewrite product; keep routes/flows)
- [ ] All planted defects gone (skill + pattern maps in WORKSPACE-SPEC §10; incl. `viewports`)
- [ ] No new banned patterns
- [ ] Browser verification (`WORKSPACE-SPEC.md` §11)
- [ ] Phase 5 scorecard filled (≥ release bar; hard stops clear; incl. `viewports`)

## Phase 5 — Scorecards

- [ ] Greenfield domain table complete (18 rows incl. `viewports`)
- [ ] Brownfield domain table complete (18 rows incl. `viewports`)
- [ ] Pre-flight audit both runs via `ux-audit`
- [ ] Hard stop check: anti-slop + destructive confirm

## Phase 6 — Negatives

- [x] 6.1 UI without setup
- [x] 6.2 Non-UI prompt leaves setup uninvoked
- [x] 6.3 No dual `## UI/UX skills` after re-setup
- [x] 6.4 “Are you sure?” after reading `surfaces` = fail
- [ ] 6.7 Overflow / persistent sidebar / hover-only primary at 375px = fail `viewports`

## Release bar

- [x] Phase 0 all pass (20 skills incl. `viewports`)
- [ ] Phase 1A pass (20 skills into scratch)
- [x] Phase 2 defaults + file-pick matrix pass *(prior run; pointer block copy changed — re-spot 2H if needed)*
- [ ] Greenfield ≥17 / 18
- [ ] Brownfield ≥17 / 18
- [ ] No hard-stop fails
- [ ] Prompt B / finishing UI runs `ux-audit`

## Review

### Pending catalog (20 skills / 1 audit + 18 domain) — `viewports`

- Date:
- Agent:
- Install path:
- Product: Harbor (`tests/WORKSPACE-SPEC.md`)
- Greenfield domain: __ / 18
- Brownfield domain: __ / 18
- `viewports`: __ (375 overflow, chrome menu, 44px hits, tap-first)
- Ship?
- Notes: Skill landed 2026-09-14. Replant brownfield `viewports` defects on next fixture rebuild. Do not reuse wiped `.scratch/harbor-*`.

### Harbor catalog (19 skills / 1 audit + 17 domain) — 2026-09-14

- Date: 2026-09-14
- Agent: Cursor (Composer) + subagents for fixture/build/repair
- Install path: 1A local nested-git scratch → `.agents/skills/` (19 skills + lockfile)
- Product: Harbor (`tests/WORKSPACE-SPEC.md`)
- Apps: `.scratch/harbor-greenfield` (built), `.scratch/harbor-brownfield` (repaired); fixtures under `examples/`
- Greenfield domain: **17 / 17**
- Brownfield domain: **17 / 17**
- `page-patterns`: **pass** (all ten anatomies present; GF named patterns before markup)
- Ship? **yes**
- Notes: Serve GF `http://localhost:4173`, BF `http://localhost:4174`. BF list still uses a single status `<select>` in the toolbar (prefer one Filters panel — anatomy nit, not hard-stop). Task delete on GF briefly closes drawer before confirm (~160ms) to avoid stacked modals.

### Domain skills (Harbor)

| Skill | Greenfield | Brownfield | Notes |
| --- | --- | --- | --- |
| spacing | pass | pass | 4/8pt; ~70ch |
| typography | pass | pass | weights 400/500/600 only; ≥12px |
| colour-palette | pass | pass | neutrals; soft shadow |
| anti-slop | pass | pass | no rainbow/glass/cartoon/deco icons/pastel pills |
| page-patterns | pass | pass | all 10 routes; BF toolbar status select = minor anatomy drift |
| surfaces | pass | pass | 0-shift rename; named delete; Cancel focused |
| forms | pass | pass | blur-first; clickable submit |
| keyboard | pass | pass | focus-visible; trap+restore on delete |
| defaults | pass | pass | timezone; drafts |
| verbs | pass | pass | no OK/Submit/Proceed |
| errors | pass | pass | blameless + Copy error details |
| labels | pass | pass | visible labels |
| loaders | pass | pass | fast/medium/slow demo; skeletons; no full-page spinner |
| empty-states | pass | pass | CTA + Clear all filters |
| motion | pass | pass | token durations; no bounce |
| transitions | pass | pass | overlays; no layout jump on rename |
| reduced-motion | pass | pass | media query present |

### Browser verification (Harbor)

- GF login: centered, no sidebar; projects empty CTA; load sample; inline rename Δtop=0; delete `Delete project 'Harbor launch'?` Cancel focused; filtered empty + Clear all filters; board Todo/Doing/Done + Add; messages split pane; reports date range + Export
- BF login: no sidebar; dashboard no mash-up; projects named delete; tasks single URL with Board/List; reports From/To + Export in header

### Past run (pre-rename catalog — 14 skills / 13 domain)

- Date: 2026-09-10
- Agent: Cursor (Grok 4.6)
- Greenfield domain: 13 / 13
- Brownfield domain: 13 / 13
- Ship? yes (for then-current 14-skill catalog)

### Current catalog (17 skills / 16 domain) — 2026-09-10

Kept for history. Re-run against the **18-skill** catalog (setup + `ux-audit` + 16 domain) before shipping.

- Date: 2026-09-10
- Agent: Cursor (Composer)
- Install path: 1A local (nested git scratch; CLI walks git root)
- Greenfield domain: **16 / 16**
- Brownfield domain: **16 / 16**
- Ship? **yes** (for then-current 17-skill catalog)
- Notes: Ran in `.scratch/` only. Fixtures under `examples/` unchanged. Apps at `.scratch/greenfield` and `.scratch/brownfield`.

### Pending catalog (19 skills / 1 audit + 17 domain) — Harbor fixture

- Date: 2026-09-14
- Agent: Cursor (Composer)
- Install path: empty → `.agents/skills/` (Cursor `-a cursor`); existing → reuse
- Product: Harbor (`tests/WORKSPACE-SPEC.md`)
- Greenfield domain: **17 / 17**
- Brownfield domain: **17 / 17**
- `page-patterns`: **pass** (all ten anatomies)
- Ship? **yes**
- Notes: Results under `.scratch/harbor-*`. Fixtures rebuilt in `examples/` (gitignored).

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
| page-patterns | pass | pass | Harbor 2026-09-14; all 10 patterns scored |
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
