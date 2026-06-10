# Architecture Sonifier

3D spectrogram visualization of architecture converted to sound.

**Live demo:** [Deploy to Vercel]

## What it does

Converts the geometry of the Taj Mahal (11,846 vertices from a 3D model) into an 8-second piece of music using additive synthesis. The result is visualized as an interactive 3D spectrogram — height = frequency, color = amplitude, X axis = time.

## How it works

1. Parse 3D model vertices (GLB/SketchUp format)
2. Map geometry to audio: height → frequency, horizontal position → time offset, depth → amplitude
3. Compute STFT spectrogram of the synthesized audio
4. Render as 3D mesh with Three.js
5. Synthesize audio in-browser via Web Audio API (additive synthesis from spectrogram bins)

## Self-contained

No backend, no file uploads. The 40×100 spectrogram matrix is embedded as ~21KB of base64 data. Audio is synthesized in the browser on first load (~3 seconds).

## Run locally

```bash
# Just open index.html in a browser
open index.html

# Or with a local server (Chrome requires it for some audio features)
python3 -m http.server 8080
```

## Deploy to Vercel

```bash
npm i -g vercel
vercel --prod
```

Or connect the GitHub repo in the Vercel dashboard — zero config required, auto-detects as static site.

## Controls

- **Drag** — rotate view
- **Scroll** — zoom
- **Play button** — play synthesized audio with animated playhead
- **Wireframe toggle** — show mesh structure
- **Rotation toggle** — auto-rotate

## Tech

- [Three.js r128](https://threejs.org) — 3D rendering
- Web Audio API — in-browser audio synthesis
- Python (offline) — GLB parsing, STFT, data embedding
- No build step, no dependencies to install
