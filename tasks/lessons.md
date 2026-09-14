# Lessons

## viewports: cap the page, not the app (2026-09-14)

`--vp-wide` (1280px) is a **content** cap. Putting `max-width` on `html`, `body`, `.app`, or `.shell` shrinks the sidebar and header into a centered column. Chrome stays full viewport width. Only `main` / `.page` gets `max-width: var(--vp-wide)`.
