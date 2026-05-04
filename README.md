# 🎈 Little Girl & Red Balloon

A scroll-driven 2D interactive animation — inspired by Banksy's iconic street art *Girl with Balloon*, built without libraries using HTML Canvas.
<img width="572" height="326" alt="Screenshot 2026-05-02 at 9 21 45 PM" src="https://github.com/user-attachments/assets/ca98880b-e0c9-4089-9d3f-53adcbd4b926" />

[**View the live demo**](https://vivian-chi.github.io/2D-Interactive-Illustration/)

---

## Inspiration

The interaction concept is inspired by **Banksy's *Girl with Balloon*** (2002). The visual idea of a girl and a balloon was the starting point.

The 8 animation frames were **generated with GPT Image 2** and exported as SVGs. They were then mapped to scroll positions and wired into a custom animation engine built with HTML Canvas.

---

## The Story

A little girl stands quietly, holding a red balloon. As you scroll, she reaches for it, breaks into a run, leaps — and then floats away into the sky, carried off by the balloon entirely.

The whole experience unfolds in a single scroll gesture. It's designed to feel alive, not mechanical: her run cycle responds to scroll speed, she pauses for a breath-holding moment just before the grab, and her exit is a smooth float into open space.

---

## How It Works

The animation is driven entirely by **scroll percentage (0–100%)**. A set of keyframes maps each scroll position to a character pose, horizontal position, and vertical height. Between keyframes, values are interpolated and smoothed with a simple lerp so nothing ever snaps.

```
0%   → Holding the balloon, standing still
10%  → Reaching out, curious
15%  → Starting to chase
20%  → Running (G4/G5 alternate based on scroll velocity)
65%  → Almost there — leaping upward
70%  → Grabbing moment — brief pause locks scroll here
73%  → Flying, lifted off the ground
100% → Gone — floated off the top-right corner
```

Touch and mouse wheel are both supported, with `preventDefault()` so the browser never interferes.

---

## Project Structure

```
little-girl/
├── index.html          # Entry point — structure only
├── css/
│   └── style.css       # Layout and scroll indicator styles
├── js/
│   └── script.js       # All animation logic
└── frames/
    ├── 1-holding.svg
    ├── 2-reaching.svg
    ├── 3-start-chasing.svg
    ├── 4-running.svg
    ├── 5-running-harder.svg
    ├── 6-almost-there.svg
    ├── 7-grabbing-moment-new.svg
    └── 8-flying-away-update.svg
```

---

## Running Locally

No build step needed. Just open `index.html` in a browser — or serve it locally to avoid any SVG cross-origin quirks:

```bash
npx serve .
```

---

## Design Notes

- **SVG frames** are pre-illustrated in a consistent coordinate space. The engine scales them to always fill half the viewport height, regardless of screen size.
- **HiDPI / Retina** displays are handled by reading `devicePixelRatio` and scaling the canvas physical size accordingly.
- **The grab pause** at 70% is intentional — a 200ms lock that makes the balloon-catch feel earned, not accidental.
- **The SCROLL indicator** fades in only at the very start and very end, then disappears to keep the frame clean.

---

## Credits

- **Concept inspiration** — Banksy, *Girl with Balloon* (2002)
- **Illustration prompt** — [Aleena Amir](https://x.com/aleenaamiir/status/2049400614195794230) (@aleenaamiir)
- **Frame generation** — GPT Image 2 (OpenAI)
- **Animation & code** — built with HTML Canvas and vanilla JS, developed with AI coding assistance (Antigravity)
