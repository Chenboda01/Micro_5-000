# AGENTS.md — Micro 5,000

## Repo overview

Single-file HTML space shooter game. GitHub: `Chenboda01/Micro_5-000` on `main`.

The actual git workspace root is this directory (`Micro_5-000/`), **not** the parent
`Micro_5,000/`. The parent README.md at `../README.md` contains the game source code
embedded inside it — it is **not** a real README and is not tracked by git.

## File conventions

- The game is a single static HTML file. The author refers to it as **`Space.html`**.
- Currently the game source lives embedded inside the parent `README.md`. If you
  extract it, put it in this directory as `Space.html`.
- No build system, no package manager, no linter, no test framework.
- Open `Space.html` directly in a browser to run. No dev server needed.

## Tech stack

- Vanilla HTML + CSS + JavaScript. No frameworks, no TypeScript, no dependencies.
- Canvas-based rendering (`<canvas id="gameCanvas">`, 800×600).
- Mobile-friendly: touch controls via `touchmove`, `user-scalable=no` in meta viewport.

## Game architecture

Single global object `S` holds all state. No modules, no classes — everything is
global functions and the `S` object. Key state fields:

| Field | Purpose |
|---|---|
| `S.gameMode` | `'basic'` or `'full'` |
| `S.difficulty` | `'easy'`, `'mid'`, or `'hard'` |
| `S.wave` | Current wave (1–100) |
| `S.paused` | Global pause flag — most functions gate on this |
| `S.upgrading` | True during the "upgrade to full" loading screen |
| `S.betweenWaves` | True during inter-wave break timer |

The game loop is a single `requestAnimationFrame` chain (`loop()` calls `update()` then `draw()`).

### Game modes

- **Basic mode**: No enemy shooting, no autopilot/pause/restart buttons. Every 5 waves
  in basic mode, the "Upgrade to Full Game" prompt appears.
- **Full mode**: All features enabled (enemy bullets, shop, autopilot, pause, restart).

### Weapons

Indexed array in `S.weapons[]`. Weapon 0 (Laser/Laser Cannon) is always owned.
Weapons are purchased in the shop overlay. Weapon stats differ between basic and
full mode (full mode weapons are rebalanced with higher costs).

## Versioning note

The README states this is version 1. A version 2 is mentioned with a planned
release in "2 years and 2 weeks". Treat the current codebase as v1.
