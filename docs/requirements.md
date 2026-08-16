# Requirements

## Scope

Web-based backgammon app for 2 players, supports standard rules, move validation, dice rolling, win detection.

## 1. Functional Requirements

### 1.1 Rules Engine
- FR-1.1.1: Enforce standard backgammon setup (24-point board, standard starting checker positions for both players).
- FR-1.1.2: Support both players' checkers moving in opposing directions around the board toward their respective home boards.
- FR-1.1.3: Enforce the "hitting" rule: landing on a point with a single opposing checker (blot) sends it to the bar.
- FR-1.1.4: Enforce that a checker on the bar must re-enter before any other move is made by that player.
- FR-1.1.5: Prevent moves onto points occupied by two or more opposing checkers.
- FR-1.1.6: Support standard backgammon variants configuration (optional — e.g., Acey-deucey) if enabled; base rules apply by default.

### 1.2 Turn Management
- FR-1.2.1: Alternate turns between the two players, starting player determined by an opening roll (higher single die wins; re-roll on tie).
- FR-1.2.2: Track and display whose turn it is at all times.
- FR-1.2.3: Require the active player to use all legal dice values if possible; if only a partial number of moves can be played, enforce the maximum legally playable moves.
- FR-1.2.4: Automatically pass the turn when a player has no legal moves available.
- FR-1.2.5: Prevent the non-active player from making moves out of turn.

### 1.3 Dice Rolling
- FR-1.3.1: Provide a randomized, fair two-die roll each turn using a cryptographically sound or well-tested PRNG.
- FR-1.3.2: Support doubles (rolling the same number on both dice), granting four moves of that value instead of two.
- FR-1.3.3: Display dice results clearly to both players.
- FR-1.3.4: Disallow manual dice manipulation by players (no re-rolling except as game rules dictate).

### 1.4 Move Legality / Validation
- FR-1.4.1: Validate every proposed move against current board state, dice values, and turn state before applying it.
- FR-1.4.2: Reject moves that violate blocked-point, bar-reentry, or direction rules.
- FR-1.4.3: Highlight/support legal destination points for a selected checker (UI aid, not required for engine correctness).
- FR-1.4.4: Support undo of an in-progress (not yet confirmed) move within the same turn, prior to turn submission.
- FR-1.4.5: Validate combined moves (using both dice as a single checker's move) where applicable.

### 1.5 Bearing Off
- FR-1.5.1: Allow bearing off only when all of a player's checkers are within their home board.
- FR-1.5.2: Support exact and overage bear-off rules (a checker may bear off with a higher roll than needed if no checkers occupy higher points).
- FR-1.5.3: Return checkers to play (no longer eligible to bear off) if a checker is hit and sent to the bar after bear-off has begun, until it re-enters and returns to the home board.

### 1.6 Doubling Cube (Optional Feature)
- FR-1.6.1: Support an optional doubling cube feature, toggleable per game/session.
- FR-1.6.2: Allow a player, on their turn before rolling, to offer a double; opponent may accept (cube value doubles, opponent gains cube ownership) or decline (offering player wins current stake).
- FR-1.6.3: Track cube value and current owner; only the cube owner may re-offer a double.
- FR-1.6.4: Enforce the doubling cube maximum value per configured game rules (e.g., default cap or unlimited).

### 1.7 Win Detection
- FR-1.7.1: Detect and declare a win when a player bears off all 15 checkers.
- FR-1.7.2: Support standard scoring: single game, gammon (opponent has borne off zero checkers), and backgammon (opponent has a checker in winner's home board or on the bar when the game ends).
- FR-1.7.3: Display final result (winner, win type, and cube value/points if doubling cube is enabled) at game end.
- FR-1.7.4: Prevent further moves once a win condition is met.

### 1.8 Game Session Management
- FR-1.8.1: Support starting a new game/match between two players.
- FR-1.8.2: Support resigning/forfeiting a game.
- FR-1.8.3: Maintain move history for the current game (for display and undo purposes).

## 2. Non-Functional Requirements

### 2.1 Performance
- NFR-2.1.1: Move validation and board state updates must complete within 100ms under normal conditions.
- NFR-2.1.2: Initial page load (time to interactive) should be under 3 seconds on a standard broadband connection.
- NFR-2.1.3: UI animations (dice roll, checker movement) should run at a smooth frame rate (target 60fps) without blocking game logic.

### 2.2 Browser Support
- NFR-2.2.1: Support the latest two major versions of Chrome, Firefox, Safari, and Edge.
- NFR-2.2.2: Responsive layout supporting desktop and tablet viewport sizes (minimum 768px width); mobile phone support is a stretch goal, not required for initial release.
- NFR-2.2.3: No dependency on browser plugins (e.g., Flash); pure HTML/CSS/JS (or equivalent framework) implementation.

### 2.3 Accessibility
- NFR-2.3.1: Meet WCAG 2.1 AA where feasible for a graphically-driven board game (color contrast, focus indicators, text alternatives for icons).
- NFR-2.3.2: Support keyboard navigation for selecting checkers and destination points as an alternative to drag-and-drop/mouse interaction.
- NFR-2.3.3: Provide ARIA labels/live regions announcing dice rolls, turn changes, and game results for screen reader users.
- NFR-2.3.4: Avoid relying on color alone to distinguish player checkers (use shape/pattern/label differentiation as well).

### 2.4 Reliability & Correctness
- NFR-2.4.1: Game state must remain consistent and recoverable from a page refresh during an active game (session persistence).
- NFR-2.4.2: All rule enforcement (move legality, bearing off, win detection) must be handled authoritatively to prevent invalid states, whether validation occurs client-side, server-side, or both.

### 2.5 Security
- NFR-2.5.1: If played over a network (not purely local hot-seat), prevent a player from viewing or manipulating the opponent's dice roll or move choices before they are committed.
- NFR-2.5.2: Sanitize any user-provided input (e.g., player names, chat if present) to prevent XSS.

## 3. Out of Scope

- Multiplayer matchmaking, ranked ladders, or spectator modes.
- AI/computer opponent (single-player vs. bot).
- Real-time chat, voice, or video communication between players.
- Tournament management, brackets, or multi-match scoring beyond a single match.
- Native mobile applications (iOS/Android); this is a web app only.
- Offline/local-only play without any session/state handling (unless explicitly added later).
- Backgammon variant rule sets beyond standard rules (e.g., Nackgammon, Hypergammon) unless separately scoped.
- Persistent user accounts, profiles, statistics tracking, or leaderboards.
- Localization/internationalization (multi-language support) for the initial release.
- Monetization features (ads, in-app purchases, subscriptions).
