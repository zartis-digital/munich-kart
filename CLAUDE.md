# Munich Kart — live demo project (Anthropic Lab, Munich, 16 Sep 2026)

## What this is
A single-file browser kart racer used in a live 20-minute showcase in front of ~40 people. Every change happens on stage. Speed and reliability beat elegance.

## How to work in this session
- Do not ask clarifying questions. Pick the sensible default, state it in one line, proceed.
- Keep replies to five lines or fewer. No explanations of the code, no recap of what you changed beyond one line.
- Make small, targeted edits. Never restructure or rewrite index.html wholesale.
- After any visual change: make sure the server is running, take a Playwright screenshot into shots/, look at it, fix what is off, then report.
- Bump the build stamp (the <title> and the HUD corner label, "build N") on every change to index.html.
- Never add dependencies, package.json, bundlers or frameworks. No audio files: Web Audio synthesis only.
- Do not touch .claude/, qr.html or shots/ unless asked.
- If a change breaks the game, run `git checkout -- index.html` to restore the last good build, say so in one line, and continue.
- Never delete directories. To clean screenshots, overwrite files; do not remove shots/.

## Product & tech constraints
- One self-contained index.html: vanilla JS + Canvas 2D. Must work in current Chrome and Safari, on desktop and on phones.
- Keyboard: arrows drive, Shift drifts, M mutes, Enter starts. Touch devices: on-screen Left / Right / Boost buttons, auto-accelerate.
- 60 fps target; keep per-frame work light. HUD text large enough for a projector.

## Art direction
- Flat, colourful vector look. Palette: Bavarian blue #0066B3, white #FFFFFF, asphalt #3A3F47, grass #6BBF59, accent #F4B400 for pickups.
- Checkered finish line. Munich landmark silhouettes around the track. No copyrighted characters or logos of any kind.

## Run & verify (this machine is Windows)
- Use `python`, never `python3` (it does not exist here). Paths may be written with forward slashes.
- Serve: a static server is already running on http://localhost:8000 during the demo. Check with `Invoke-WebRequest -Method Head http://localhost:8000` (PowerShell) or `curl -sI http://localhost:8000` (Bash). Only if it is down: `python -m http.server 8000` as a background job.
- Screenshot: `npx playwright screenshot --viewport-size=1280,720 http://localhost:8000 shots/<name>.png` (Chromium is installed).
- Open in the browser: `Start-Process http://localhost:8000` (PowerShell) or `start http://localhost:8000` (Bash). Open a file the same way with its path.

## Deploy
- Repo: zartis-digital/munich-kart on GitHub, branch main. GitHub Pages serves / from main.
- Live URL: https://zartis-digital.github.io/munich-kart/ (qr.html in this folder already points here).
- Commit only index.html, README.md, launch/ and analysis/. Never force-push. Never change Pages settings.

## Files
- index.html — the game
- README.md — controls and how to run
- launch/ — marketing and executive artefacts (created live)
- analysis/ — balance results from the dry run
- shots/ — screenshots (gitignored)
- qr.html — QR page for the projector (do not edit)
