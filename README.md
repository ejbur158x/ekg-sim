# Telemetry EKG Simulator

Single-file vanilla JS + Canvas app. No build step, no dependencies.

## Deploy to GitHub Pages (same flow as pxpgrcn / perigon / flagrush)

```bash
git init
git add index.html manifest.json sw.js
git commit -m "EKG sim v1"
git branch -M main
git remote add origin https://github.com/ejbur158x/ekg-sim.git
git push -u origin main
```

Then in repo Settings → Pages → Deploy from branch → `main` / `root`.
It'll be live at `https://ejbur158x.github.io/ekg-sim/` and installable
as a PWA (Add to Home Screen) since it ships a manifest + service worker.

## Notes

- `icon-192.png` / `icon-512.png` referenced in `manifest.json` aren't
  included — drop your own app icons in the repo root or the manifest
  will just fall back to no custom icon (app still installs fine).
- Rhythm engine lives entirely in `index.html` under `scheduleNext()`.
  Each rhythm case controls: R-R interval logic, whether a P wave is
  present, PR interval, QRS width/amplitude ("wide" flag = bizarre/
  ventricular morphology), and T wave shape.
- `sampleAt(tSec)` is the single function that turns "what beats are
  scheduled" into "what's the trace value right now" — that's the one
  to touch if you want to tune morphology further.
- Measured HR readout is calculated from actual R-R spacing of
  captured beats (not just echoing the slider) — so during AV blocks/
  afib you'll see it diverge from your target rate, which is the point.

## Educational tool only — not for clinical use.
