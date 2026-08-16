# Design Documentation
Traces UX/design decisions back to `docs/requirements.md`. This document is updated
as design work progresses through each component (board, checkers, dice, panels, etc.).

## Status

| Component | Status | Notes |
|---|---|---|
| Board layout | In progress | This document |
| Checkers | Not started | |
| Dice | Not started | |
| Turn / score panel | Not started | |

---

## 1. Board Layout

### 1.1 Overview

Standard backgammon board: 24 triangular points arranged in 4 quadrants of 6,
split by a central bar, with bear-off/home areas on the right side.

```
 13 14 15 16 17 18 |BAR| 19 20 21 22 23 24
+-------------------+   +-------------------+  |
|  ↓  ↓  ↓  ↓  ↓  ↓ |   |  ↓  ↓  ↓  ↓  ↓  ↓ |  |  <- Home
|                   |   |                   |  |     (Player 2 bears off here,
|                   |   |                   |  |      or Player 1, depending on
|  ↑  ↑  ↑  ↑  ↑  ↑ |   |  ↑  ↑  ↑  ↑  ↑  ↑ |  |      orientation below)
+-------------------+   +-------------------+  |
 12 11 10  9  8  7  |BAR|  6  5  4  3  2  1
```

### 1.2 Open questions / decisions to finalize

- [ ] **Orientation**: Which player's home board is on the right vs left? Does
      orientation flip depending on which player is viewing (if two-device/remote
      play is ever in scope), or is it fixed for a single shared-screen game?
- [ ] **Point numbering**: Show point numbers (1–24) on the board at all, or keep
      them purely internal to the data model? If shown, where (above/below each
      triangle)?
- [ ] **Point direction**: Top row of points points downward, bottom row points
      upward — confirm this is the convention we're using.
- [ ] **Bear-off tray**: Separate visual area outside the 24 points, or implied
      by the edge of the board?

### 1.3 Structure

- **24 points**: alternating two colors (e.g., light/dark or two accent colors),
  drawn as triangles.
- **4 quadrants** of 6 points each, split into two halves (left/right of the bar).
- **Bar**: central vertical strip, holds checkers that have been hit.
- **Frame/border**: outer edge of the board, distinct from the point colors.

### 1.4 Visual approach

- Build as a single self-contained HTML file with inline SVG for the points
  (triangles are easiest to draw precisely in SVG vs. CSS clip-paths).
- No interactivity or checkers in this first pass — layout and color only.
- Use CSS variables for colors/spacing so the board can restyle consistently
  once synced into the claude.ai/design component library via DesignSync.

### 1.5 Color palette

_TBD — fill in once first visual draft is reviewed._

| Element | Color | Notes |
|---|---|---|
| Point (light) | | |
| Point (dark) | | |
| Board frame | | |
| Bar | | |
| Background | | |

---

## 2. Traceability

| Design decision | Related requirement |
|---|---|
| 24-point board, standard layout | Functional: "supports standard rules" |
| _(add as decisions are made)_ | |

---

## 3. Change Log

| Date | Change |
|---|---|
| 2026-08-16 | Initial skeleton created; board layout section drafted |
