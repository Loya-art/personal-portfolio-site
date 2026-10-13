# Glassmorphism + Background Image Portfolio

Complete working template reference. Combine with SKILL.md instructions.

## Structure

```
HTML
├── .bg-layer          (z:-2, background image + will-change for parallax)
├── .bg-overlay        (z:-1, very light gradient + backdrop-filter blur)
├── #particles-canvas  (z:0, floating dots with connection lines)
├── nav                (fixed, glassmorphism background)
├── #hero              (name + glitch, subtitle, tagline, badges)
├── #about             (2-column: text + 2x2 glass cards)
├── #skills            (tag list)
├── #contact           (glass buttons)
└── footer
```

## Key CSS Variables (Bright Theme)

```css
--cyan: #00c8ff; --purple: #a855f7; --pink: #ec4899;
--text: #0f172a; --text-dim: #334155;
--surface: rgba(255,255,255,0.78);
--surface-hover: rgba(255,255,255,0.92);
```

## Background — Safe Fixed (No Parallax)

⚠️ **Avoid translateY parallax** — pushing the bg down on scroll causes blank space at the bottom of long pages.

✅ **Safe approach:**
```css
.bg-layer {
  position: fixed; inset: 0; z-index: -2;
  background: url('path/to/image.jpg') center / cover no-repeat;
}
```
No JS needed. `background-size: cover` fills the viewport at any scroll position.

If you must use parallax (not recommended for content-heavy pages), use a much taller container: `height: 300%; top: -100%` and warn the user about potential bottom bleed.

## Particle Network (60 dots, connection dist < 120px)

```js
const COUNT = 60;
// Each particle: { x, y, vx, vy, r, alpha }
// Each frame: move, wrap around edges, draw circle, draw lines to nearby particles
```

## Scroll Reveal (IntersectionObserver)

threshold: 0.15, rootMargin: '0px 0px -50px 0px'
Staggered delays: .reveal-delay-1 = 0.1s, .reveal-delay-2 = 0.2s, etc.
Transition: 0.8s cubic-bezier(0.16, 1, 0.3, 1)

## Auto-Hide Navbar

Hide on scroll down (past 100px), show on scroll up.

## Glassmorphism Card Pattern

```css
background: var(--surface);
backdrop-filter: blur(12px);
-webkit-backdrop-filter: blur(12px);
border: 1px solid rgba(255,255,255,0.5);
border-radius: 16px;
transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
```

Hover: `background: var(--surface-hover); transform: translateY(-4px); box-shadow: 0 20px 60px rgba(0,0,0,0.08);`

## Chinese Name Display

- Glitch effect uses text-shadow with cyan/purple/pink offsets
- letter-spacing: -2px for large display
- font-weight: 900 for Chinese display text
