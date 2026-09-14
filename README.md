# Munich Kart

A top-down arcade kart racer in one self-contained `index.html`. Vanilla JS + Canvas 2D,
no dependencies, no build step. Three laps around a Bavarian circuit against three AI karts.

Play it live: https://zartis-digital.github.io/munich-kart/

## Controls

**Keyboard**

| Key | Action |
| --- | --- |
| ↑ | Accelerate |
| ↓ | Brake / reverse |
| ← → | Steer |
| Shift | Drift |
| Space | Drop a slick (3 per race) |
| M | Mute |
| Enter | Start / race again |

**Touch** — auto-accelerate, with large on-screen buttons: `◀` `▶` to steer, `DRIFT` to slide,
`SLICK` to drop a patch. Works in portrait and landscape.

## Racing

- 3 laps, 4 karts, live position and lap timer in the HUD, minimap top right.
- Gold chevrons on the asphalt are boost pads.
- Grass slows you down badly — stay on the black stuff.
- A dropped slick makes any kart that hits it, including the AI, lose grip for about a second.
- Podium and a **Race again** button at the finish.

## Run it

Any static server from this folder:

```
python -m http.server 8000
```

Then open http://localhost:8000.

## Screenshot check

```
npx playwright screenshot --viewport-size=1280,720 http://localhost:8000 shots/start.png
```

## Notes

- Sound is Web Audio synthesis only (engine hum that tracks speed, pickup blips) — no audio files.
- The `<title>` and the HUD corner label carry the build number; bump both on every change.
