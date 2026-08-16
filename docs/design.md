# Design Documentation

Traces UX/design decisions back to `docs/requirements.md`. Updated as design work
progresses through each component (board, checkers, dice, panels, etc.).

## Status

| Component | Status | Notes |
|---|---|---|
| Board layout | Done | `design/components/board.html` (Claude Design) |
| Checkers | Not started | Depends on anchor coordinate system — see `architecture-notes.md` |
| Dice | Not started | |
| Turn / score panel | Not started | |

---

## 1. Board Layout

### 1.1 Overview

Standard backgammon board: 24 triangular points arranged in 4 quadrants of 6,
split by a central bar (60px), with an optional bear-off tray on the right.

Reference component: `design/components/board.html`, built in Claude Design.
Runtime dependency (`support.js`) is a generic Claude Design preview templating
runtime — not backgammon-specific, not part of the app itself.

### 1.2 Decisions

- **Orientation / perspective**: Fixed single-screen layout. The `perspective`
  prop relabels point numbers only (`25 - baseNumber`); it does **not** rotate
  or reposition the triangles. Confirmed sufficient for this project's scope
  (no physical 180° board rotation for the other player's view).
- **Point numbering convention**: Standard convention, encoded in geometry
  but not previously written down as a contract. Now explicit:
  - Bottom-right quadrant: points 1–6 (edge → bar)
  - Bottom-left quadrant: points 7–12 (bar → edge)
  - Top-left quadrant: points 13–18 (edge → bar)
  - Top-right quadrant: points 19–24 (bar → edge)
- **Bear-off tray**: Toggleable via `showBearOffTray` prop. Currently, hiding
  the tray leaves the ~158px tray column as dead frame-colored space rather
  than recomputing board geometry. **Open — see architecture-notes.md.**
- **Point numbers**: shown directly on the board (not purely in the data model),
  with text color chosen per-point for contrast against that point's fill.

### 1.3 Color tokens (finalized)

| Token | Value | Role |
|---|---|---|
| `--frame` | #5C3A21 | Outer board frame |
| `--frame-edge` | _(see component)_ | Frame border detail |
| `--point-a` | #E9D8B4 | Point color, light |
| `--point-b` | #8B3A2A | Point color, dark |
| `--bar` | #2A1810 | Central bar |
| `--tray-bg` | _(see component)_ | Bear-off tray background |
| `--number-light` | _(see component)_ | Point number text on dark points |
| `--number-dark` | _(see component)_ | Point number text on light points |

These are the canonical design tokens going forward — reused as-is for
checkers, dice, and panel components rather than redefined per-component.

### 1.4 Geometry (as built)

- Board split into left/right halves, 429px each, meeting a 60px central bar
  exactly (no gap/overlap).
- Color alternates `i % 2` both across the bar and column-wise between top/bottom
  quadrants.
- ViewBox: 1100×700 (fixed regardless of tray visibility — see open question above).

### 1.5 Known gaps (not part of this component, tracked in architecture-notes.md)

- No checker anchor coordinate system defined yet
- No exposed `pointAnchors[1..24]` data contract
- Bear-off tray hidden state leaves unresolved dead space

---

## 2. Traceability

| Design decision | Related requirement |
|---|---|
| 24-point board, standard layout | Functional: "supports standard rules" |
| Fixed orientation, numbering relabel only | Functional: 2-player, single shared screen |

---

## 3. Change Log

| Date | Change |
|---|---|
| _(earlier)_ | Initial skeleton created; board layout section drafted |
| _(today)_ | Board layout finalized in Claude Design; palette, numbering, and orientation decisions recorded; open items moved to `architecture-notes.md` |
