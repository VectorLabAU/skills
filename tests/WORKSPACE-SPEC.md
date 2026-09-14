# Harbor — Workspace Fixture Spec

Build contract for the greenfield and brownfield eval apps. Soft taste notes are out of scope. Hard rules from each `SKILL.md` are pass/fail.

**Eval protocol** (install, setup, scorecard, release bar): [`TEST-PLAN.md`](TEST-PLAN.md).  
**This file** defines the product the agent must build or repair.

Do **not** commit `examples/greenfield/` or `examples/brownfield/` (gitignored). Recreate them from this spec when an eval runs.

---

## 1. Purpose

Harbor is one small team projects workspace used to harden the **entire** skill library:

| Starting state | Folder | Job |
| --- | --- | --- |
| Greenfield | `examples/greenfield/` | Empty shell. Agent builds every route from job descriptions (no pattern names in the prompt). |
| Brownfield | `examples/brownfield/` | Same routes and data, already working, with planted fails. Agent repairs without rewriting the product. |

Both finished apps must exercise **all 18 domain skills** on a full run. No silent `n/a` for a skill that this product covers.

**Reset (2026-09-14):** scored `.scratch/harbor-*` apps wiped. Next eval starts from `examples/` fixtures and must score `viewports`.

Shared profile for scored runs: Stripe / default bans / WCAG 2.1 AA / Utilitarian & Minimal / Lucide.

---

## 2. Stack, serve, scratch

| Item | Rule |
| --- | --- |
| Stack | Vanilla HTML / CSS / JS. Multi-page. Framework-agnostic. |
| Serve | `npx --yes serve .` from the example folder |
| Skills install | Scratch copy only. Never install into the catalog repo root. |
| Install path | One path per scratch: skills.sh **or** Claude plugin — not both |
| Profile | Run `setup-ui-ux-skills` before build/repair on scored runs |
| Finish | Run `ux-audit` before declaring UI done |

```bash
cd examples/greenfield   # or examples/brownfield
npx --yes serve .
# open the printed local URL
```

---

## 3. Information architecture

`page-patterns` says List / Board / Calendar of the **same** records is one page with a toggle. Harbor uses **different jobs and record types** so all ten product patterns are real pages.

| Route | User’s job | Locked pattern | Records |
| --- | --- | --- | --- |
| `/login.html` | Sign in | 3 Form (auth) | session only |
| `/index.html` | Glance, then leave | 4 Dashboard | derived counts |
| `/projects.html` | Scan and manage projects | 1 List | projects |
| `/project-new.html` | Multi-step create | 3 Form (wizard) | one new project |
| `/project.html?id=` | Inspect one project | 2 Detail | one project |
| `/tasks.html` | Move work through stages | 6 Board (List toggle allowed) | tasks |
| `/calendar.html` | Work by date | 7 Calendar | events (not tasks) |
| `/inbox.html` | Work a time-ordered queue | 10 Inbox (standalone) | notifications |
| `/messages.html` | Triage threads without leaving | 8 Split Pane | threads |
| `/reports.html` | Change range, read, export | 9 Analytics (Analytical) | report view |
| `/settings.html` | Configure the workspace | 5 Settings | workspace prefs |

**Chrome** (sidebar + top header) frames signed-in pages. Chrome is **not** a page pattern.  
On `viewports` narrow (<768px) the sidebar is **not** a persistent rail — the same links live in a menu.  
**Auth** (`login.html`) has **no** app sidebar at any width.

**Out of scope:** marketing routes, React/Svelte ports, committing example trees, LLM CI.

---

## 4. Data model (localStorage only)

No secrets in storage (`defaults`).

### Entities

| Entity | Fields |
| --- | --- |
| workspace | name, timezone |
| projects | id, name, status, timezone, notes |
| tasks | id, projectId, title, stage (`todo` / `doing` / `done`) |
| events | id, title, date, projectId |
| notifications | id, title, unread, createdAt |
| threads | id, from, subject, snippet, body, time |

### Seed rules

| App | Seed |
| --- | --- |
| Greenfield | Zero projects, tasks, events, notifications, threads so empty-states fire. Optional “Load sample data” after first create is allowed. |
| Brownfield | Populated seed so happy-path verify is never empty. Must still reach first-use empty and filtered-zero (e.g. clear store / clear filters). |

Brownfield seed minimum (illustrative counts): ≥3 projects, ≥6 tasks across all three stages, ≥4 events on different dates, ≥4 notifications (mix read/unread), ≥3 threads.

---

## 5. Chrome vs pages

### Signed-in chrome

- Left sidebar: links to Dashboard, Projects, Tasks, Calendar, Inbox, Messages, Reports, Settings
- Top header: workspace name, optional account affordance
- Chrome spans the viewport. `max-width: 1280px` belongs on `main` / the page only (`viewports`)
- Narrow (<768px): sidebar rail hidden; same destinations from a menu button (`viewports`)
- Does **not** replace a page pattern. Does **not** appear on `login.html`.

### Pattern naming (greenfield)

Before writing markup for each page route, the agent states the locked pattern name in chat (e.g. “Pattern 1 — List / Index”). Naming is the `page-patterns` test. The build prompt must **not** leak pattern names.

---

## 6. Per-route anatomy

Plain-language must / must-not. Full catalog: [`skills/interaction/page-patterns/reference/catalog.md`](../skills/interaction/page-patterns/reference/catalog.md).

### `/login.html` — Form (auth)

**Must**

- Centered card: logo/title, email + password (or equivalent), one primary action, escape link
- No app sidebar
- Blur-first validation; submit always clickable (`forms`)
- Visible labels; placeholders are format hints only (`labels`)

**Must not**

- Full-bleed form on wide screens
- App chrome on auth
- Cards around every field group

### `/index.html` — Dashboard

**Must**

- Heading + one sentence
- KPI strip (max 5), one primary chart (or chart stub), supporting list (recent / upcoming)
- Read-only. Actions link out to other modules

**Must not**

- Date-range filters, drill-down, or live ops console (that is Analytics)
- Six or more metric tiles
- Editable records on the dashboard
- Projects table or settings toggles on this page

### `/projects.html` — List

**Must**

- Heading, one-sentence description, Create in header, search, one Filters control, table, pagination
- Active filters as chips; **Clear all filters**
- Empty / populated / filtered-zero states
- Row click → Detail
- Inline rename on project name (see overlays)
- Quick-add slide-over (name + timezone only); full intake via wizard link

**Must not**

- KPI tiles above the list
- Sidebar filter rails
- Stack of filter dropdowns in the toolbar
- Settings preference toggles on this page

### `/project-new.html` — Form (wizard)

**Must**

- Multi-step create (≥2 steps): e.g. basics → details → review
- Step list + per-step validation; sticky Cancel / Next (or Save on last step)
- Draft persist + Discard (`defaults`)
- Narrow column; labels above fields

**Must not**

- A single modal chain instead of a route
- Disabled primary until “valid” without clickable submit that shows errors

### `/project.html?id=` — Detail

**Must**

- Record name, status + metadata, breadcrumb back to list
- Tabs (e.g. Details | Documents | Activity | Notes); each tab loads on its own
- Edits via slide-over; delete with named confirm
- Activity tab may use Inbox variant B (newest first, Load more)

**Must not**

- One long scrolling dump of every field with no tabs
- Cards wrapping each tab section
- Project configuration fields that belong on Settings

### `/tasks.html` — Board

**Must**

- Stages as columns with live counts; empty columns stay visible with + Add
- Search + Filters; optional List | Board toggle of the **same** task records
- Keyboard path to change stage (⋯ → Move to…). Drag cannot be the only way
- Card click → slide-over or Detail-style preview

**Must not**

- Split tasks across three URLs (`tasks-list` / `tasks-board` / `tasks-calendar`)
- Hide empty stages to “clean up” a filter
- Use a table as the only stage UI when stages are the main job

### `/calendar.html` — Calendar

**Must**

- Month (or week) grid always renders; empty period message **on** the grid
- Today control; empty cell → create with that date filled (slide-over)
- Events are a separate record type from tasks

**Must not**

- Replace the grid with a blank empty-state page
- Reuse task stages as the calendar’s only data

### `/inbox.html` — Inbox (standalone)

**Must**

- Time-ordered queue; unread uses weight **and** a leading accent (not colour alone)
- Rows are not a DataTable (no headers, no sort)
- Actions such as Approve / Decline or Mark all read
- First-use empty: header + value + CTA

**Must not**

- Table headers / column sort on the feed
- Unread indicated by colour only

### `/messages.html` — Split Pane

**Must**

- Left: compact list (avatar/title/meta/time). No table headers or sort
- Right: selected thread detail; selection updates right panel only
- Arrow keys move selection; Enter moves focus right
- First-use empty with CTA

**Must not**

- Navigate away on select
- Put a DataTable in the left pane

### `/reports.html` — Analytics (Analytical)

**Must**

- Date range always visible; filters; KPI strip (max 5); primary + secondary charts; detail table
- One filter change updates every chart
- Charts load with their own skeletons when slow
- **Export** in the header (this pattern only)

**Must not**

- No date range
- Put Export on the List toolbar instead
- Inline-edit numbers on the report
- Use this page as a no-filter overview (that is Dashboard)

### `/settings.html` — Settings

**Must**

- Section nav (sticky) + section heading + controls + Save where grouped fields need it
- Instant switches may save themselves
- Danger zone last, separated, destructive styling (e.g. delete workspace with named confirm)
- Configures the **workspace**, not a project record

**Must not**

- Edit project record fields here
- One card per individual setting
- Mash settings onto Dashboard or List

---

## 7. Overlay and confirm contracts

These exist in **both** finished apps so `surfaces` cannot be `n/a`.

### Inline rename (0 layout shift)

- Where: project name on `/projects.html`
- Display and edit share one reserved box (same width, height, position)
- Enter saves; Escape cancels
- Neighbor row `getBoundingClientRect().top` and `.left` unchanged before vs after entering edit
- **Fail** if taller input, Save/Cancel wrap, drawer, or modal for one field

### Slide-overs (&lt;10s)

| Trigger | Content |
| --- | --- |
| Quick-add project (list header secondary path) | Name + timezone only |
| Quick edit project | Name, timezone, notes |
| Task card open | Title, stage, project link |
| Empty calendar cell | Create event; date prefilled |

Slide-over from trailing edge; focus trap; Esc dismisses; restore focus to trigger. Draft persist on forms (`defaults`).

### Pages (≥10s)

Wizard (`project-new.html`), Settings, and all other full routes above. No stacked modals.

### Delete confirm

- Used for project, task, and event (at least)
- Title names the entity (e.g. `Delete project 'Harbor launch'?`)
- Destructive verb on confirm; Cancel is default focus; Esc dismisses without deleting
- **Fail** on “Are you sure?” / OK

---

## 8. Cross-cutting skill checklist

Every domain skill must be applicable on a full Harbor run.

| Skill | Binary checks on Harbor |
| --- | --- |
| spacing | 4/8pt rhythm; body 65–75ch; icons align to cap-height |
| typography | ≤3 weights, none &gt;600; no text &lt;12px; heading LH 1.1–1.25; body 1.5–1.6 |
| colour-palette | 60-30-10; 1px border before shadow; light shadow alpha &lt;0.08 |
| anti-slop | No rainbow CTA, unbounded glass, cartoon people, decorative input icons, pastel metadata pills |
| viewports | No page overflow at 375 or 1280; chrome collapsed on narrow; hit targets ≥44px (AA); primary actions work without hover |
| page-patterns | Pattern named before each page’s markup (greenfield); all ten anatomies match; no invented eleventh pattern |
| surfaces | Inline / slide-over / route / named delete as in §7 |
| forms | Blur-first; clear on focus/keystroke; submit always clickable; no First+Last split for one name |
| keyboard | Full Tab path; visible focus ring; overlay trap + restore; board stage via menu; split pane arrows + Enter |
| defaults | Timezone inferred; wizard + slide-over drafts persist with Discard; no secrets in storage |
| verbs | Imperative CTAs; no OK / Submit / Proceed; sentence case |
| errors | Blameless; what / why / next in ≤2 sentences; Copy error details; no stack dump |
| labels | Visible bound labels; placeholders are format hints only |
| loaders | Demo controls or query flags: fast (&lt;100ms, no spinner), medium (inline), slow (&gt;1s skeleton on list and report charts). No full-page spinner |
| empty-states | Header + value + CTA on list, inbox, messages; filtered list has Clear all filters; calendar empty on grid; board empty columns stay with + Add |
| motion | Durations ∈ {100,150,200,300}ms; ease-out enter / ease-in exit; transform/opacity only; no bounce/elastic chrome loops |
| transitions | Overlay motion matches surface; Esc during exit; stagger ≤30ms/item &amp; ~200ms total; no layout jump |
| reduced-motion | `prefers-reduced-motion: reduce` → instant or opacity-only; meaning not motion-only |

**Setup / audit:** scored by `TEST-PLAN.md` Phase 2 and Prompt B. Read `.ux-profile.md` before UI work. Run `ux-audit` before done.

---

## 9. Greenfield shell + build prompt

### Shell files (`examples/greenfield/`)

1. `README.md` — how to serve; product UI intentionally empty; run `setup-ui-ux-skills` before building; point humans at `../../tests/WORKSPACE-SPEC.md` and `../../tests/TEST-PLAN.md`
2. `index.html` — minimal shell only:
   - `<title>Harbor workspace (greenfield)</title>`
   - Heading “Harbor”
   - Note: “No UI yet. Run setup-ui-ux-skills, then ask the agent to build the workspace from the Harbor spec.”
3. Optional empty `styles.css` / `app.js` — no product features

**Must not include:** forms, modals, loaders, lists, finished chrome, or styled product UI.

### Prompt A — build (jobs only; do not name skills or patterns)

```text
Build Harbor in this folder (vanilla HTML/CSS/JS is fine). Follow tests/WORKSPACE-SPEC.md.

Pages and jobs (name the right page pattern yourself before each page’s markup — do not invent an eleventh product pattern):

- login.html — sign in (centered card, no app sidebar)
- index.html — glance at workspace status, then leave to a module
- projects.html — scan and manage many projects (empty, populated, filtered-zero)
- project-new.html — multi-step create for a new project
- project.html?id= — inspect one project with sections
- tasks.html — move tasks through stages (todo / doing / done); optional list view of the same tasks
- calendar.html — work by date with events (separate from tasks)
- inbox.html — work a time-ordered notification queue
- messages.html — triage message threads without leaving the page
- reports.html — change date range and filters, read charts, export
- settings.html — configure the workspace (not a project record)

Also include:
- App chrome (sidebar + header) on signed-in pages only
- Inline rename for a project name on the list (same reserved box; next row must not move)
- Slide-overs for quick-add project, quick edit project, task card, and create-event from an empty calendar cell
- Delete with named confirmation (project, task, event)
- Saves that can be fast, slow (>1s with skeletons), or fail with a blameless error + Copy error details
- Full keyboard access through overlays; board stage change without relying on drag alone; messages list arrows + Enter
- Short overlay enter/exit that respects prefers-reduced-motion
- Layouts work at 375px: no page-level horizontal scroll; sidebar becomes a menu; actions work without hover
- localStorage data model from the Harbor spec; start empty so zero-states appear

Use this project’s UI/UX profile and skills. Do not skip setup artifacts if they exist.
```

### Prompt B — audit

```text
Finish the UI. Run `ux-audit`.
```

---

## 10. Brownfield files + defect map

### Files (minimum)

| File | Role |
| --- | --- |
| `README.md` | Serve instructions; warn UI is deliberately broken for eval; link this spec |
| `login.html` … `settings.html` | All eleven routes from §3 |
| `styles.css` | Visual defects |
| `app.js` (and optional modules) | Interaction defects, seed data, loaders |
| Optional shared partials | Chrome duplicated or injected — any approach is fine |

Annotate every planted defect:

```html
<!-- DEFECT: skill-or-pattern — short description -->
```

Same for CSS/JS comments.

### Skill-level plants (must be gone after repair)

| Skill | Planted defect |
| --- | --- |
| spacing | Gaps 13px / 19px / 22px; body ~120ch; icons box-centered |
| typography | Weights 400–800; 11px cells; inverted line-heights (heading 1.6, body 1.3) |
| colour-palette | Saturated canvas; shadow alpha 0.25; rainbow CTA |
| anti-slop | Glass blur; cartoon empty; decorative input icons; pastel pills |
| viewports | Shell or body `width: 1440px`; sidebar always 240px; 24×24 icon buttons; row Delete hover-only |
| surfaces | Stacked modals; “Are you sure?” / OK; rename swaps taller input or Save/Cancel wrap so next row jumps |
| forms | Validate-while-typing; disabled Submit; First+Last for project name; placeholder-as-label |
| keyboard | `outline: none`; no focus trap; no restore |
| defaults | Blank timezone; no draft persist |
| verbs | OK / Submit / Proceed labels |
| errors | “You entered an invalid email”; raw `500 INTERNAL_SERVER_ERROR` |
| labels | Placeholder-as-label (with forms) |
| loaders | Spinner on instant save; full-page spinner on slow list / reports |
| empty-states | “Nothing here” no CTA; filtered empty without Clear all filters |
| motion | Bounce/elastic; animate height; 800ms decorative fade |
| transitions | Overlay open jumps layout; long stagger |
| reduced-motion | Ignore `prefers-reduced-motion`; meaning only via motion |

### Pattern plants (must be gone after repair)

| Pattern | Planted defect |
| --- | --- |
| page-patterns (home mash-up) | `index.html` mixes KPI strip + projects table + preference toggles; no single named pattern |
| Board vs views | Tasks split across `tasks-list.html` / `tasks-board.html` / `tasks-calendar.html` instead of one Board page with List toggle |
| Detail | `project.html` is one long field dump (no tabs) |
| Form (auth) | `login.html` keeps the app sidebar |
| Calendar | Empty state **replaces** the grid |
| Split Pane | Left pane is a DataTable; row click navigates away |
| Analytics | No date range; Export sits on the Projects list toolbar |
| Inbox | Table headers/sort; unread is colour-only |
| Settings | Edits project record fields; one card per control |
| Board | Hides empty stages; drag is the only way to move a card |

### CSS plants (shared)

- Gaps: 13px, 19px, 22px
- Prose max-width ~120ch or none
- Icons vertically centered to box, not cap-height
- Font weights including 700 and 800; meta text 11px
- Heading `line-height: 1.6`, body `line-height: 1.3`
- Saturated blue/purple canvas; `box-shadow: 0 8px 24px rgba(0,0,0,0.25)`
- Rainbow multi-stop gradient on primary CTA
- Glass panel with `backdrop-filter: blur(...)` without strong border
- Pastel pill badges on static metadata
- Decorative emoji/icon inside text inputs
- Bounce/elastic keyframes; `transition: height`; no reduced-motion media query
- `body` or `.shell` `width: 1440px`; sidebar `width: 240px` with no narrow collapse
- Icon buttons 24×24; a row Delete shown only on `:hover` (no `(hover: hover)` gate)

### Repair prompt

```text
Fix this Harbor workspace to match our UI/UX skills and tests/WORKSPACE-SPEC.md. Do not rewrite the product — keep the same features, routes, and flows. Repair layout, type, colour, slop, viewports, page patterns, surfaces, forms, keyboard, defaults, copy, loaders, empty states, and motion.
```

---

## 11. Browser verify script

Start a static server. Exercise as a user. A screenshot alone is **not** verification.

1. **Login** — centered card, no sidebar; blur validation; always-clickable submit
2. **Dashboard** — ≤5 KPIs; links out; no projects table or settings toggles
3. **Projects list** — empty CTA (greenfield) or seed rows (brownfield); filter to zero → Clear all filters
4. **Inline rename** — next row’s `top` matches before and after enter-edit
5. **Slide-over** — quick-add or quick edit; Esc; focus restore; no layout jump
6. **Wizard** — `/project-new.html` multi-step; draft survives refresh; Discard works
7. **Detail** — tabs present; edit via slide-over; not a field dump
8. **Board** — empty columns visible; Move to… via keyboard/menu; optional List toggle stays one URL
9. **Calendar** — grid always visible; empty cell opens create with date filled
10. **Inbox** — unread weight + accent; Approve or Mark all read; not a sorted table
11. **Messages** — arrow select updates right pane; Enter moves focus; no navigate-away on select
12. **Reports** — change date range; charts update; Export in header; slow path uses skeletons
13. **Settings** — workspace prefs only; danger zone named confirm with Cancel focused
14. **Delete** — named entity; Cancel focused; Esc cancels
15. **Loaders** — fast save no flicker; slow list/report skeleton; no full-page spinner
16. **Errors** — failed save blameless + Copy error details
17. **Motion** — overlay open/close; with reduced-motion emulated, no slide/bounce; meaning not motion-only
18. **Viewports** — resize a signed-in page to 375px: no page-level horizontal scroll; sidebar rail gone; menu reaches the same links; a primary action works without hover

---

## 12. Out of scope

- Publishing the catalog
- CI that drives an LLM
- React / Svelte / other framework ports of Harbor
- Marketing route types
- Committing `examples/greenfield/` or `examples/brownfield/`
- Changing domain skill hard rules (this spec only describes how to test them)
- Running the eval until explicitly approved after catalog changes land
