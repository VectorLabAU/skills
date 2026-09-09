---
name: surface-routing-and-dialogs
description: Chooses slide-over, page, or inline edit by task duration; mandates destructive confirmation. Use when adding modals, drawers, dialogs, routes, or destructive actions.
title: Surface Routing and Dialogs
category: interaction-friction
severity: hard-rule
references:
  - reference/destructive-actions.md
---

If `.ux-profile.md` exists at the project root, read it before changing surfaces, forms, or focus behavior.

### Intent

Users lose context when the wrong surface type interrupts their flow. Quick edits stay in place; longer work gets a dedicated route; destructive actions never fire without explicit, named confirmation. This skill routes tasks to the lightest surface that still supports the work.

### Hard Rules (Non-Negotiable)

- **Task <10s: slide-over, drawer, or non-modal popover.** Do not navigate away from the current page or replace the main view. The user must retain spatial context of where they started.
- **Task ≥10s or multi-step: dedicated sub-page with its own URL route.** Stacking modals is prohibited. A second modal on top of an open modal is a hard failure — promote to a route or collapse into one sequential flow on a page.
- **Single field edits: in-place inline expansion with 0 layout shift.** Reserve height/width or use absolute overlay positioning so surrounding content does not jump when edit mode opens.
- **All destructive operations: dedicated confirmation dialog** that (a) names the exact entity, e.g. "Delete workspace 'Analytics'?" — never "Are you sure?"; (b) uses a destructive verb on the confirm button in destructive color; (c) sets Cancel as default keyboard focus; Escape dismisses without executing.

See [reference/destructive-actions.md](reference/destructive-actions.md) for confirmation layout, focus trapping, and copy templates.

### Design Heuristics & Taste Principles

- Estimate task duration from field count and decision points: one field + one action ≈ slide-over; three+ fields or branching steps ≈ page.
- Slide-overs enter from the trailing edge (right in LTR); width 400–480px for forms, full-height on mobile.
- Inline edit: show pencil affordance on hover/focus; swap label for input in the same box; Save/Cancel as text buttons inline, not a modal.
- Prefer URL-updatable state for ≥10s tasks so refresh and share links preserve progress.
- Non-destructive dismiss (Escape, backdrop click on non-modal popover) must not lose unsaved work — persist draft per `smart-defaults-and-inference`.

### Concrete Scenarios (Before vs. After)

#### ❌ Anti-Pattern

Editing a project name opens a centered modal on a modal (stacked). Deleting a folder shows "Are you sure?" with OK/Cancel. Changing one tag navigates to `/settings/tags/edit/123`. The inline rename shifts the table row height by 40px.

#### ✅ Best Practice

Rename opens inline: label becomes input in-place, row height unchanged, Enter saves, Escape cancels. Delete folder opens a confirmation dialog: title "Delete folder 'Q4 Reports'?", body lists item count impact, red "Delete folder" button, Cancel focused by default. A 5-step onboarding wizard lives at `/onboarding/step-2` with browser back support — no modal chain.

### Framework-Agnostic Implementation Blueprint

```
function chooseSurface(estimatedSeconds, fieldCount, isMultiStep):
  if fieldCount == 1 and estimatedSeconds < 10 and not isMultiStep:
    return "inline-edit"
  if estimatedSeconds < 10 and not isMultiStep:
    return "slide-over"
  return "route"   // never "stacked-modal"

function confirmDestructive(action, entityLabel):
  open dialog with title = action + " " + entityLabel + "?"
  focus trap inside dialog
  focus Cancel button on open
  on Escape or Cancel: close, restore focus to trigger
  on Confirm: execute action, then close and announce result
```

```html
<!-- Inline edit: reserve space -->
<div class="cell-edit" style="min-height: 2.5rem;">
  <span class="cell-display" hidden>...</span>
  <input class="cell-input" />
</div>
```

Route-based flows update `history.pushState` or framework router; slide-overs use `role="dialog"` with `aria-modal="true"` only when modal; popovers use `role="dialog"` without trapping page scroll.

### Agent Checklist

- [ ] Read `.ux-profile.md` if present.
- [ ] Classify task duration and step count; pick inline, slide-over, or route — never stacked modals.
- [ ] Verify single-field edits cause zero layout shift.
- [ ] Confirm all destructive actions use named-entity confirmation per reference spec.
- [ ] Set Cancel as default focus; Escape dismisses without side effects.
- [ ] Restore focus to trigger element when any overlay closes.
