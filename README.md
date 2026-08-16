# Backgammon App

A web-based backgammon app for 2 players, built as a teaching example of the full
software development lifecycle using Claude Code and Claude Design — from
requirements through UX design, architecture, implementation, testing, and
deployment.

## Project goals

This repo is used in a software engineering class to demonstrate:

- Generating initial requirements from a project scope
- Defining UX design from those requirements
- Designing software architecture
- Implementing the app with test coverage
- Deploying the finished app

Each phase is tracked as its own PR, so the git history itself shows the
progression from idea to shipped app.

## Repo structure

```
docs/
  requirements.md        Functional & non-functional requirements
  design.md               UX/design decisions, palette, layout, traceability
  architecture-notes.md   Open questions carried from design into architecture
  architecture.md         (added during architecture phase)
design/
  components/             Design-time artifacts exported from Claude Design
    board.html             Approved board layout component (reference only)
    support.js              Claude Design's preview runtime (not app code)
    README.md                Explains what these files are and aren't
src/                      (added during implementation phase)
tests/                    (added during implementation phase)
```

## Status

| Phase | Status |
|---|---|
| Project scope & requirements | Done |
| UX design | Done (board layout) |
| Software architecture | Not started |
| Implementation | Not started |
| Testing | Not started |
| Deployment | Not started |

## Tooling

- **Claude Code** — implementation, tests, git/PR workflow
- **Claude Design** — UX component design (board, checkers, dice, panels)
- **GitHub** — version control; PRs reviewed and merged manually per phase

## Getting started

Setup instructions will be added once implementation begins.
