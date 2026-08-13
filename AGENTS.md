# AGENTS.md

Single-page HTML5 Canvas asteroids clone. No build, bundler, tests, lint, or deps — verification is manual: open `index.html` directly or run `npx serve .` then visit `http://localhost:3000`.

## Constraints

- `game.js` is loaded as a classic `<script src="game.js"></script>` in `index.html`. Do NOT introduce ES modules / `import` / `export`, or the game breaks.
- Canvas is fixed at 800x600. Keep `W`/`H` constants in `game.js` in sync with the `width`/`height` attributes on the `<canvas>` in `index.html`.
- UI strings (HUD, overlays) and the README are in Spanish (`NIVEL`, `PUNTAJE`, `GAME OVER`). Match that; keep `SCORE` as-is.

## Game code conventions

- Entities follow a `dead` flag + `filter(p => !p.dead)` cleanup pattern each frame; new entities (power-ups, etc.) should do the same.
- Two input mechanisms: `keys[...]` = held state (used for rotation/thrust in `Ship.update`); `pressed(code)` = edge-triggered, consumed on read (used for shooting/restart). Don't mix them up.
- Position wraps toroidally via `wrap(v, max)` for ship, bullets, asteroids.
- State machine in `update(dt)`: `'playing' | 'dead' | 'gameover'`; new states must be handled in `update`, `draw`, and `drawGameOver`.
- `dt` in `loop(ts)` is clamped to `0.05s`. Use `dt` everywhere for physics.
- Skins: the `SKINS` array defines ship appearances (`name`, `color`, `hull` points, nose at +x). `Ship.draw`, `drawLifeIcon` and the game-over selector all render the active skin via `traceHull(skin.hull)`; selection lives in `skinIndex` (persisted to `localStorage`), changed with `KeyC` in-game or arrow keys in game-over via `cycleSkin(dir)`.