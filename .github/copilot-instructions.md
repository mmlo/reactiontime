# Copilot / AI Agent Instructions — reactiontime

These notes are tailored for an AI coding agent working on this small, single-page reaction-time demo.

**Repository Big Picture**
- Single-file static web app: the entire app lives in `index.html` (HTML, CSS, JS inline). No build system or server-side components.
- Purpose: measure user visual reaction time across `totalTrials` trials, present session summary and comparison tables derived from `MU`/`SIGMA` parameters.

**Key Files / Places to Edit (explicit examples)**
- `index.html` — the only app source. Script contains the core state and functions (e.g., `startSession()`, `startGame()`, `handleClick()`, `renderComparisonTables()`).
  - To change the default trials, edit `const totalTrials = 3;` in the script.
  - To adjust the reference distribution, edit `const MU = 273; const SIGMA = 60;`.
- `README.md` — authoritative usage notes and quick run commands. Keep it updated when adding new workflows.

**Developer Workflows / Commands**
- No build step. Run locally with a static server when previewing in-browser to avoid CORS/resource quirks:

```bash
# from the project root
authoritative: python3 -m http.server 8000
# then open http://localhost:8000
```
- Alternatively use the editor's Live Server extension or open `index.html` directly (double-click) for simple edits.

**Project-specific Patterns & Conventions**
- All behavior is inline in `index.html`. When adding features prefer keeping tightly coupled UI + logic in the same file unless the feature grows in complexity.
- Local state persists via `localStorage` using the key `bestReactionTime` (value stored in milliseconds). When changing storage schema, migrate carefully and update `README.md`.
- Accessibility is considered: `#prompt` has `role="button"` and `aria-label`, keyboard support via `Space`, and touch optimization (`touch-action: manipulation`). Follow these patterns when adding interactive elements.
- Timing relies on `performance.now()` for high-resolution measurements — do not replace with `Date.now()` unless precision is unnecessary.

**Testing / Validation Notes (discoverable)**
- No automated tests present. Manual checks to run after changes:
  - Load page and run full session (default `totalTrials`) on desktop and mobile emulation.
  - Validate `localStorage` updated: `localStorage.getItem('bestReactionTime')` returns numeric ms.
  - Confirm percentiles and z-scores update in the comparison tables (`renderComparisonTables`).

**Integration points & external deps**
- External font: Google Fonts (`Inter`) is loaded via `<link>`. If working offline, either vendor-lock the font or remove the dependency.
- No backend or third-party analytics integrated — adding them requires introducing a new config area and updating `README.md`.

**Suggested agent behaviors / priorities**
- Small, focused PRs only: modify a handful of lines or add one small file. Keep `index.html` changes easy to review.
- When introducing new files (JS/CSS/asset), update `README.md` with run instructions and mention any new local dev steps.
- Preserve inline accessibility features and use `role`/`aria` attributes when adding interactive controls.
- Prefer non-breaking defaults: changing `totalTrials`, `MU`, `SIGMA` should not invalidate existing `localStorage` values without an explicit migration.

**Examples the agent may use directly**
- Change default trials to 5:
```js
// in index.html script
const totalTrials = 5;
```
- Read best saved time (dev console):
```js
localStorage.getItem('bestReactionTime');
```
- Serve locally:
```bash
python3 -m http.server 8000
```

**Merging guidance (if `.github/copilot-instructions.md` already existed)**
- Preserve any project-specific rules in the old file, but prefer the concrete code references here (constants and function names in `index.html`).
- Keep high-level policies but remove generic, non-actionable advice. Add concrete examples above.

If anything here is unclear or you'd like extra items (e.g., a suggested test harness, or moving JS into a separate file), tell me which area to expand and I will iterate.