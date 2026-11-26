# Crossy Bots

A Crossy Road-style game in a single self-contained HTML file, with a human mode and four bots that evolve from naive to advanced. The UI is in French.

**Play it online: https://crossy-bots.vercel.app**

Or open `crossy-bots.html` in a modern browser. No build step and no dependencies.

## Modes

| Mode | Controller |
|---|---|
| Joueur | Keyboard: arrow keys or ZQSD, Space to wait, Enter to replay, P to pause, V to switch view |
| Bot v1 | Forward or Wait, one tick of lookahead |
| Bot v2 | All 5 actions, one tick of lookahead, fixed priority |
| Bot v3 | Exhaustive depth-5 search (3125 sequences) |
| Bot v4 | Depth-15 breadth-first search with (x, y, t) state deduplication |

## Views

- **Vision du Jeu**: voxel-style pseudo-3D game view.
- **Vision Superposée**: game view with deadly cells and the live search tree on top.
- **Vision du Robot**: flat debug view with the logical grid, exact hitboxes and the live search tree.

The search runs incrementally: the cyan tree grows level by level, the magenta best path updates as better candidates appear, and an arrow on the player shows the move currently favoured. Pause and Pas-à-pas freeze or advance the search one step at a time.

## Determinism and testing

The world is generated from `(seed, rowIndex)` with a seeded PRNG, so the same seed always gives the same world, and every bot predicts exactly what happens next. Debug assertions check each prediction against the real outcome.

The side panel has a benchmark that plays N seeded games per bot. From the browser console:

```js
crossyBots.runBenchmarkSync(10, 800);
```
