# AI Posture & Focus Monitor

Real-time posture detection that runs entirely in your browser using on-device AI. No servers, no data leaves your machine.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![TensorFlow.js](https://img.shields.io/badge/TensorFlow.js-4.22-orange.svg)
![MoveNet](https://img.shields.io/badge/model-MoveNet_Lightning-green.svg)

---

## What It Does

Uses your webcam and **TensorFlow.js MoveNet** pose estimation to track your upper-body posture in real time. When it detects sustained bad posture, it triggers an audible alarm until you correct yourself.

**Detects three types of bad posture:**

| Type | What It Means |
|---|---|
| **Hunching Forward** | Head dropped too close to shoulders |
| **Leaning Back** | Shoulders moved away from camera (shrinking) |
| **Slumping in Chair** | Head dropped significantly down the frame |

## Features

- **100% Private** — All AI inference runs locally via WebGL. Zero network requests for pose data.
- **Instant Calibration** — One click saves your ideal posture baseline.
- **Configurable Alarm Delay** — Set how long bad posture is tolerated (1–10 seconds).
- **Sensitivity Presets** — Low / Medium / High to match your comfort level.
- **Volume Control** — Adjustable alarm volume.
- **Session Statistics** — Tracks session duration and good-posture percentage.
- **Page Visibility Handling** — Pauses detection when the tab is hidden to save resources.
- **Keyboard Shortcuts** — Press `S` to start, `C` to calibrate.
- **Accessible** — ARIA labels, focus rings, and screen-reader-friendly status updates.

## Quick Start

1. **Open `main.html`** in any modern browser (Chrome, Edge, Firefox, Safari).
2. Click **Start Camera** and grant camera permission.
3. Sit in your ideal posture, looking at the screen.
4. Click **Calibrate Posture**.
5. Work normally — the monitor runs in the background.

> No build step, no install, no dependencies to manage. Just open the file.

## Requirements

| Requirement | Details |
|---|---|
| **Browser** | Chrome 80+, Edge 80+, Firefox 78+, Safari 14+ |
| **Hardware** | Webcam, WebGL-capable GPU (most modern devices) |
| **Network** | Required only on first load (to fetch TensorFlow.js + model from CDN) |

## How It Works

```
Webcam → TensorFlow.js MoveNet (pose estimation) → Keypoint Analysis → Posture Classification → Alert System
```

1. **MoveNet Lightning** detects 17 body keypoints from the video feed at ~30 FPS.
2. On calibration, the app records baseline metrics: eye-to-shoulder distance, eye Y-position, and shoulder width.
3. Each frame compares current metrics against the baseline using configurable sensitivity thresholds.
4. If bad posture persists beyond the alarm delay, a two-tone siren plays via the Web Audio API.
5. The skeleton overlay provides real-time visual feedback of detected keypoints.

## Project Structure

```
AI-Posture-Focus-Monitor/
├── main.html      # Complete application (HTML + CSS + JS in one file)
├── README.md      # This file
└── LICENSE         # MIT License
```

## Configuration

Open the **Settings** panel in the app to adjust:

| Setting | Default | Range |
|---|---|---|
| Alarm Delay | 2.0s | 1.0 – 10.0s |
| Sensitivity | Medium | Low / Medium / High |
| Alarm Volume | 80% | 10% – 100% |

### Sensitivity Thresholds

| Preset | Hunched Ratio | Lean-Back Ratio | Slump Drop |
|---|---|---|---|
| Low | < 0.65 | < 0.70 | > 16% |
| Medium | < 0.75 | < 0.80 | > 12% |
| High | < 0.82 | < 0.87 | > 8% |

## Privacy

- **No telemetry.** No analytics, no tracking pixels, no external API calls.
- **No video storage.** Frames are processed in-memory and immediately discarded.
- **No server.** The entire app is a single static HTML file.
- CDN scripts (TensorFlow.js, Tailwind CSS) are fetched once and cached by the browser.

## Browser Compatibility Notes

- **Camera permissions**: HTTPS or `localhost` is required for `getUserMedia` in most browsers.
- **WebGL backend**: Required for TensorFlow.js GPU acceleration. Falls back to CPU if unavailable (slower).
- **Web Audio API**: Used for the alarm. Requires a user interaction (button click) before audio can play.

## License

[MIT](LICENSE) © 2026 AdinAbdullahSaleem
