# design/components/

Design-time artifacts exported from Claude Design. These are reference
components used to define visual/layout decisions — they are **not** part
of the application and are not imported into app source.

## Files

- **`board.html`** — the approved board layout component (24 points, bar,
  optional bear-off tray). Colors are defined as CSS custom properties;
  see `docs/design.md` for the finalized token values and layout decisions.
- **`support.js`** — Claude Design's generic preview/templating runtime
  (handles `sc-if`/`sc-for`/`{{ }}` interpolation, prop schemas, React-based
  rendering for the `.dc.html` preview format). It is **not backgammon-specific**
  and contains no app logic. Required only so `board.html` renders standalone
  when opened directly; do not reuse it in the actual application.

## How this fits into the project

These files are the durable record of what was designed and approved, kept
in version control for traceability alongside `docs/requirements.md` and
`docs/design.md`. They are a snapshot at the point design work concluded —
claude.ai/design remains the working/iteration environment for producing
new or updated components, but once a component is finalized it should be
exported and committed here the same way this one was.

## What NOT to do with these files

- Do not import `board.html` or `support.js` directly into the app's
  `src/` — extract the SVG geometry and CSS variable values as the source
  of truth, then rebuild as a real component in the app's actual stack.
- Do not treat `support.js` as reusable application code.

## Known open items

See `docs/architecture-notes.md` for unresolved questions this design
raises (checker anchor coordinates, point-index data contract, bear-off
tray geometry when hidden) that the architecture phase needs to answer.
