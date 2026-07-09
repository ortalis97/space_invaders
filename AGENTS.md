# AGENTS.md

## Project Overview

This repository contains a lightweight, browser-based **Space Invaders** game implemented as a single static HTML file.

- Primary gameplay logic, rendering, and input handling are embedded directly in `index.html`.
- There is no package/dependency manifest, build pipeline, test runner, or CI configuration in the current repository.
- Local serving is supported via `.claude/launch.json` using Python’s built-in HTTP server.

## Repository Structure

Current top-level structure:

```text
space_invaders/
├── .claude/
│   └── launch.json
├── .gitignore
├── AGENTS.md
├── README.md
└── index.html
```

### File Roles

- `README.md` — minimal project title documentation.
- `index.html` — complete game application (HTML, CSS, JavaScript in one file).
- `.gitignore` — ignore rules for generated/local artifacts (`node_modules/`, `dist/`, env files, etc.).
- `.claude/launch.json` — local run configuration (`python3 -m http.server 8123`).

## Development Guidelines

Because this is a flat, static repo, follow simple and predictable editing practices:

1. **Keep runtime requirements minimal**
   - Preserve no-build, no-dependency workflow unless explicitly changing project scope.
2. **Prefer small, focused changes**
   - Separate gameplay changes, UI styling updates, and documentation edits when possible.
3. **Keep controls and gameplay text in sync**
   - If controls change in JS logic, update the on-screen instruction text in `#info`.
4. **Validate in browser after each change**
   - Confirm movement, shooting, collision behavior, score/lives display, and win/lose states.

### Local Run

Use the existing static server pattern from `.claude/launch.json`:

```bash
python3 -m http.server 8123
```

Then open:

```text
http://localhost:8123
```

## Code Patterns

This repository intentionally uses a single-file pattern.

- **Game state**: global variables in script scope (`player`, `invaders`, `enemyBullets`, `score`, `lives`).
- **Main loop**: `loop()` calls `update()` then `draw()` via `requestAnimationFrame`.
- **Input handling**: keyboard state tracked with `keydown`/`keyup` event listeners.
- **Collision logic**: centralized through `rectsOverlap(a, b)`.

There is currently no modular source layout (`src/`, multiple JS modules, or class-based architecture).

## Quality Standards

For any change, ensure:

- **Functional correctness**
  - Player movement remains bounded to canvas.
  - Bullets behave correctly (spawn, travel, cleanup).
  - Invader movement and edge-step behavior remain stable.
  - Game-over and win conditions trigger correctly.
- **Readability**
  - Keep function names descriptive and maintain existing straightforward style.
  - Add concise comments only where logic is non-obvious.
- **UI consistency**
  - Maintain retro visual style unless intentionally redesigning.
  - Ensure canvas dimensions and HUD text remain legible.

## Critical Rules

1. **Do not invent toolchains**
   - Do not add documentation that assumes npm scripts, bundlers, test frameworks, or CI jobs unless they are actually introduced in the repo.
2. **Do not break static execution**
   - `index.html` must continue to run directly in a browser via static hosting.
3. **Keep repository reality reflected in docs**
   - Documentation must match actual files and commands present in the repository.
4. **Avoid unnecessary structural expansion**
   - Do not introduce complex architecture unless the task explicitly requires it.

## Common Tasks

### Update gameplay values

Edit constants/variables in `index.html`, then refresh browser:

- Player tuning: `player.speed`
- Enemy motion: `invSpeed`, `invStepDelay`
- Difficulty/shooting: enemy shooting probability in `update()`

### Adjust visuals

Modify CSS in the `<style>` block inside `index.html`:

- Page/canvas colors
- Border thickness
- HUD text appearance

### Update docs

- Keep `README.md` concise and accurate.
- Update `AGENTS.md` when repository structure or workflow changes.

## Reference Examples

### Existing launch configuration

From `.claude/launch.json`:

```json
{"name":"static-server","runtimeExecutable":"python3","runtimeArgs":["-m","http.server","8123"],"port":8123}
```

### Existing ignore rules

From `.gitignore`:

```gitignore
node_modules/
dist/
.DS_Store
.env
.env.local
```

These entries indicate common local/generated artifacts may appear, even though no Node-based workflow is currently defined in repository files.

## Additional Resources

- Browser APIs used in `index.html`:
  - Canvas 2D API
  - `requestAnimationFrame`
  - Keyboard events (`keydown`, `keyup`)
- For lightweight local hosting, Python stdlib docs for `http.server` are relevant to the current workflow.
