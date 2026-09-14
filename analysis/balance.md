# Munich Kart — AI balance dry run

Headless simulation mode added to `index.html`: open `?sim=N` and the page runs N complete
AI-only races with no rendering, no audio and no rAF, on a fixed 1/60 s step, then puts the
results in `window.SIM_RESULTS`. Each race is seeded (mulberry32, seed = `1013904223 + race*7919`),
so a run is reproducible and two runs are directly comparable.

All four karts run the AI controller and the player top-speed bonus is switched off, so this
measures the AI and the grid, not the human.

- Races per run: **30** (3 laps each)
- Runtime: ~0.7 s per run of 30 races
- Grid: slot 0 = YOU, 1 = BLITZ, 2 = ISAR, 3 = ALPEN (slots 0/1 front row, 2/3 back row)

## Run 1 — before tuning

| Kart | Wins | Win % | Avg place | Avg lap (s) | Best lap (s) | Avg race (s) | DNF |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| YOU | 14 | **46.7** | 2.07 | 16.68 | 14.28 | 51.45 | 0 |
| BLITZ | 10 | 33.3 | 2.33 | 17.50 | 14.28 | 53.79 | 0 |
| ISAR | 4 | 13.3 | 2.50 | 16.52 | 14.02 | 51.15 | 0 |
| ALPEN | 2 | 6.7 | 3.10 | 19.58 | 14.48 | 60.24 | 0 |

**Verdict: fail.** The pole slot took 46.7 % of wins, over the 40 % threshold. The karts are
identical apart from their random draws, so the skew is positional: the front row starts 62 px
up the road, and the back row loses more time in first-corner traffic — ALPEN's average lap was
3 s slower than the leaders' while its best lap was within 0.5 s of theirs, which is traffic,
not pace.

## Tuning applied

Two changes, both aimed at the grid rather than at any one kart's personality:

1. `aiSkill` gains a grid-slot compensation — `0.9 + rnd()*0.14 + gridIdx*0.025`. Skill sets the
   corner-entry speed at which the AI lifts, so karts starting further back now carry slightly
   more speed and can recover.
2. Grid stagger reduced from 62 px to 50 px per row, tightening the field at the start.

## Run 2 — after tuning

| Kart | Wins | Win % | Avg place | Avg lap (s) | Best lap (s) | Avg race (s) | DNF |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| ISAR | 9 | 30.0 | 2.30 | 16.58 | 13.70 | 51.28 | 0 |
| YOU | 9 | 30.0 | 2.53 | 17.81 | 13.98 | 54.85 | 0 |
| BLITZ | 6 | 20.0 | 2.50 | 16.74 | 14.15 | 51.51 | 0 |
| ALPEN | 6 | 20.0 | 2.67 | 18.08 | 14.02 | 55.66 | 0 |

**Verdict: pass.** Top win share is 30 %, under the 40 % threshold. Average place has collapsed
into a 2.30–2.67 band (was 2.07–3.10) and the back-row penalty is down from 3.1 s to 1.5 s of
average lap time. No kart failed to finish in either run.

## Notes for the demo

- A race lasts roughly 50–55 s of AI driving; the human is a little quicker, since the player
  kart keeps a 5 % top-speed edge over the AI.
- Best lap sits around 13.7–14.3 s, average lap 16.6–18.1 s — the gap is traffic and grass
  excursions, so slicks and boost pads have room to matter.
- Reproduce with: `http://localhost:8000/?sim=30`, then read `window.SIM_RESULTS` in the console.
