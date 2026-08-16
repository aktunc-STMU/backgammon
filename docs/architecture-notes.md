# Architecture Notes — Open Questions

Carried over from design review (Claude Code's review of `design/components/board.html`,
see PR history / design phase). These are decisions the architecture phase needs to
resolve before implementation starts — not yet answered, not yet designed.

Status: **Open — to be resolved during architecture phase.**

---

## 1. Checker anchor coordinate system

The board design is layout-and-color only — no coordinate system exists yet for
where checkers stack on a point.

Needs:
- A defined base-center point per point index (x, y)
- Stacking direction and spacing (checkers stack toward the center of the board)
- Overflow handling once a stack exceeds visible space (common approaches:
  show a count badge after N checkers, shrink checker size, or start a second
  row/column)

**Decision needed**: pick one overflow strategy and the max checkers before it
kicks in (5 is typical in physical sets).

---

## 2. Point index → anchor data contract

`buildPoints()` currently computes polygon geometry and the point number together,
internally, with no reusable lookup exposed.

Needs:
- A `pointAnchors[1..24]` (or equivalent) export: point index → `{ x, y, orientation }`
- This becomes the contract between the board/design layer and the game engine —
  whatever renders checkers should query this rather than recomputing geometry

**Decision needed**: where this lookup lives (design component export vs.
recomputed in the app layer from board dimensions) and its exact shape.

---

## 3. Bear-off tray geometry when hidden

When `showBearOffTray` is false, the tray/divider/edge elements don't render, but
the base frame rect and 1100×700 viewBox stay fixed — leaving the ~158px tray
column as dead frame-colored space rather than the board recentering/expanding.

**Decision needed**: recompute board geometry (resize/recenter) when the tray is
off, or accept the asymmetry as a known visual trade-off. Relevant only if the
app actually needs the tray to be toggleable at runtime — confirm this is in
scope before investing in a fix.

---

## 4. Numbering convention as an explicit API

The numbering scheme is correct and consistent but was only discoverable by
reading the component's source, not stated as an intentional contract:

- Bottom-right: 1–6 (edge → bar)
- Bottom-left: 7–12 (bar → edge)
- Top-left: 13–18 (edge → bar)
- Top-right: 19–24 (bar → edge)

This is now documented in `docs/design.md` §1.2. Whatever consumes this later
(game engine / state management) must agree on this exact scheme — flag as a
constraint when defining the rules engine's board representation.

---

## 5. Minor / cleanup

- An unused `@font-face` for `'system-fallback'` is declared in the component's
  `<helmet>` but never referenced (SVG text uses `'Helvetica Neue', Arial, sans-serif`
  directly). Likely leftover scaffolding — remove during implementation, not
  meaningful enough to block on.

---

## Next step

These should be resolved (or explicitly deferred with reasoning) as part of
`docs/architecture.md`, before checker/dice components are designed or the
rules engine's board representation is implemented.
