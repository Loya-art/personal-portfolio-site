---
name: personal-portfolio-site
description: "Build a personal one-page portfolio/landing site with progressive info-gathering — especially for Chinese-speaking users who provide info piece by piece."
version: 1.1.0
author: Hermes Agent
license: MIT
platforms: [windows, linux, macos]
metadata:
  hermes:
    tags: [portfolio, landing-page, personal-site, chinese, html-css-js, glassmorphism, scroll-animations]
    related_skills: [claude-design, sketch, image-content-analysis, plan]
---

# Personal Portfolio / Landing Page

Build a personal one-page website when the user provides their self-introduction info progressively. The site is a polished single HTML file with inline CSS/JS — no build step, just open in browser.

## When to Use This

- User says "帮我做个个人网站/主页"
- User shares a profile screenshot and says "帮我做成网站"
- User is Chinese-speaking and gives info one piece at a time
- User wants a personal landing page with bio, skills, and contact info

## Principles

### Don't ask for info already provided
If the user shared a screenshot/profile image, try to extract what you can. Only ask for what's genuinely missing. User frustration signal: "图片里有的内容，你不要问我" means "don't ask about what's already in the image" — acknowledge the limitation, offer a pragmatic alternative.

### Progressive info-gathering
Users give info one piece at a time. Follow this natural order:

1. **Name / Nickname** ← always the first thing they offer
2. **Status / Role** — "准大一", "学生", "设计师", "前端开发"
3. **Interests / Skills** — what they do/study/learn
4. **One-line tagline** — their self-description (e.g. "热爱折腾的创造者")
5. **Style preference** — specific aesthetic (科技感, 简洁, 活力)
6. **Contact details** — one platform at a time

Do NOT ask 5 questions upfront. Build after each piece.

### Build-Incrementally

Each info piece triggers a rebuild:

| Phase | User gives | You build |
|---|---|---|
| 1 | Name + role | Hero section, nav, basic structure |
| 2 | Interests + tagline | About section with cards, skill tags |
| 3 | Style preference | Apply full aesthetic (colors, animations, layout) |
| 4 | Each contact | Add one entry at a time to contact section |

## Tech Stack

- Single `index.html` file
- Inline `<style>` with CSS variables
- Inline `<script>` for animations
- Google Fonts via `<link>` (Inter is safe default)
- No build step, no dependencies

## Tech/Cyber Aesthetic (科技感)

When the user wants "科技感 style":

### CSS Variables

```css
:root {
  --bg: #0a0a0f;
  --surface: #12121a;
  --cyan: #00f0ff;
  --purple: #a855f7;
  --pink: #ec4899;
  --text: #e2e8f0;
  --text-dim: #64748b;
  --border: rgba(0, 240, 255, 0.1);
}
```

### Suggested Animated Elements (Pick What Fits)

1. **Animated grid background** — Canvas with intersecting lines, floating dots at intersections, slowly pulsing opacity:

```js
const spacing = 40;
function drawGrid() {
  // draw vertical/horizontal lines with pulsing opacity
  // draw dots at intersections with sin-based sizing
  requestAnimationFrame(drawGrid);
}
```

2. **Hero name effect** — Two options depending on user preference:

**Option A: Glitch text** (colorful RGB split — ask first, some users dislike this style):
```css
.glitch {
  text-shadow:
    0.05em 0 0 var(--cyan),
    -0.05em -0.025em 0 var(--purple),
    0.025em 0.05em 0 var(--pink);
  animation: glitch-shake 4s infinite;
}
```

**Option B: Monochrome 3D extrusion** (clean, classy — use when user says "单色立体" or rejects colorful glitch):
```css
:root {
  --shadow-3d-1: rgba(0,0,0,0.10);
  --shadow-3d-2: rgba(0,0,0,0.07);
  --shadow-3d-3: rgba(0,0,0,0.05);
  --shadow-3d-4: rgba(0,0,0,0.03);
}
body.dark {
  --shadow-3d-1: rgba(255,255,255,0.08);
  --shadow-3d-2: rgba(255,255,255,0.06);
  --shadow-3d-3: rgba(255,255,255,0.04);
  --shadow-3d-4: rgba(255,255,255,0.02);
}
.glitch {
  font-size: clamp(3.5rem, 9vw, 7.5rem);
  font-weight: 900;
  color: var(--text);
  text-shadow:
    1px 1px 0 var(--shadow-3d-1),
    2px 2px 0 var(--shadow-3d-2),
    3px 3px 0 var(--shadow-3d-3),
    4px 4px 0 var(--shadow-3d-4);
  letter-spacing: -2px;
  line-height: 1;
}
```
No shake animation needed — 4-layer stacked shadow gives a clean 3D extrusion feel that works in both light and dark themes.

3. **Cursor glow** — Fixed radial gradient following mouse:

```html
<div id="cursor-glow"></div>
```

```css
#cursor-glow {
  width: 300px; height: 300px;
  background: radial-gradient(circle, rgba(0,240,255,0.06) 0%, transparent 70%);
  transform: translate(-50%, -50%);
}
```

```js
document.addEventListener('mousemove', (e) => {
  glow.style.left = e.clientX + 'px';
  glow.style.top = e.clientY + 'px';
});
```

4. **Scroll indicator** — bouncing "SCROLL" + animated arrow line at bottom of hero

5. **Card hover effects** — Cards with top accent bar gradient transition, border glow on hover

### Section Layout (Tech/Cyber)

- **Nav**: Fixed top, transparent-to-dark gradient, logo (name in CYAN), links: /about /skills /contact
- **Hero**: Full viewport, hero name (glitch or 3D extrusion), tagline, badge list
- **About**: Two-column grid (text + interest cards 2×2)
- **Skills**: Section with tag list
- **Contact**: Icon + text links with hover glow

## Contact Formatting

Add entries one at a time as user provides them. For mobile-friendliness, use click-to-copy instead of plain links:

```html
<a href="javascript:void(0)" onclick="copyText('ZZX274155583')" class="copy-link">
  <span class="copy-icon">📋</span> 💬 微信: ZZX274155583
</a>
```

See the full copy function + toast CSS in `portfolio-website` skill's `references/click-to-copy.md`.

For unprovided platforms, show muted placeholders:
```html
<a href="#" style="opacity:0.5; pointer-events:none;">🐙 GitHub (待添加)</a>
```

Update the section description dynamically: "微信/QQ 已就位，其他平台陆续添加中……"

## Minimal/Clean Aesthetic (简洁)

Alternative to tech/cyber. Use:
- White (#fafafa) or slate (#f8fafc) background
- Dark gray text (#1a1a1a)
- One accent color (blue #3b82f6 or indigo #6366f1)
- Ample whitespace, no animations
- Clean card borders with subtle shadows
- Centered layout, serif or system font

## Glassmorphism + Background Image Aesthetic (通透毛玻璃)

When the user wants to see a background image (clouds, landscape, abstract) clearly with a bright, airy feel. This is the "反科技感暗色" option — light background, dark text, glass cards.

### CSS Variables

```css
:root {
  --cyan: #00c8ff;
  --purple: #a855f7;
  --pink: #ec4899;
  --text: #0f172a;          /* dark navy for readability on bright bg */
  --text-dim: #334155;
  --surface: rgba(255,255,255,0.78);
  --surface-hover: rgba(255,255,255,0.92);
  --border: rgba(0,200,255,0.15);
  --glow: rgba(0,200,255,0.2);
}
```

### Layer Stack

Use THREE background layers, not one:

```
z-index: -2   → .bg-layer      (the image, with will-change:transform for parallax)
z-index: -1   → .bg-overlay    (very subtle gradient + optional backdrop-filter:blur(1px))
z-index:  0   → #particles-canvas (floating particle network)
z-index:  1   → sections (content)
```

### Background Image with Subtle Overlay

⚠️ **Avoid translateY parallax on the background image** — pushing the bg down on scroll causes blank space at the bottom of long pages. Use a simple fixed background instead.

```css
.bg-layer {
  position: fixed; inset: 0; z-index: -2;
  background: url('path/to/image.jpg') center / cover no-repeat;
}
.bg-overlay {
  position: fixed; inset: 0; z-index: -1;
  background: linear-gradient(180deg,
    rgba(255,255,255,0.15) 0%,
    rgba(200,220,240,0.08) 50%,
    rgba(180,200,220,0.12) 100%);
  backdrop-filter: blur(1px);
}
```

No JS needed. `background-size: cover` + `position: fixed` ensures the background always fills the viewport at any scroll position. If you must have parallax, see the `portfolio-website` skill's `references/effects-snippets.md` for the safe approach.
```

### Floating Particle Network

Canvas animation with dots connected by lines when close:

```js
const particles = [];
for (let i = 0; i < 60; i++) {
  particles.push({
    x: Math.random() * canvas.width, y: Math.random() * canvas.height,
    vx: (Math.random() - 0.5) * 0.3, vy: (Math.random() - 0.5) * 0.3 - 0.1,
    r: Math.random() * 2.5 + 1, alpha: Math.random() * 0.4 + 0.1
  });
}
// Each frame: move particles, draw circles, draw connection lines
// when dist < 120px with opacity proportional to closeness
```

### Scroll Reveal Animations

IntersectionObserver-based fade-in + slide-up with staggered delays:

```css
.reveal { opacity: 0; transform: translateY(40px); transition: opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1), transform 0.8s cubic-bezier(0.16, 1, 0.3, 1); }
.reveal.visible { opacity: 1; transform: translateY(0); }
.reveal-delay-1 { transition-delay: 0.1s; }
.reveal-delay-2 { transition-delay: 0.2s; }
```

```js
const observer = new IntersectionObserver((entries) => {
  entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
}, { threshold: 0.15, rootMargin: '0px 0px -50px 0px' });
document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
```

Apply to HTML elements:
```html
<div class="reveal">content</div>
<div class="reveal reveal-delay-1">delayed content</div>
```

### Glassmorphism Cards

Cards have `backdrop-filter: blur()` on semi-transparent backgrounds:

```css
.card {
  background: var(--surface);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: 1px solid rgba(255,255,255,0.5);
  border-radius: 16px;
  transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
}
.card:hover {
  background: var(--surface-hover);
  transform: translateY(-4px);
  box-shadow: 0 20px 60px rgba(0,0,0,0.08);
}
```

Apply same pattern to nav, contact buttons, skill tags.

### Auto-Hide Navbar

Hide navbar on scroll down, show on scroll up:

```js
let lastScroll = 0;
window.addEventListener('scroll', () => {
  const current = window.pageYOffset;
  if (current > lastScroll && current > 100) navbar.style.transform = 'translateY(-100%)';
  else navbar.style.transform = 'translateY(0)';
  lastScroll = current;
});
```

### Key Differences from Dark Tech/Cyber

| Aspect | Dark Tech/Cyber | Glassmorphism + Background Image |
|---|---|---|
| Background | Black (#0a0a0f) + grid | User's image + very light overlay |
| Text | Light (#e2e8f0) | Dark (#0f172a) |
| Cards | Dark solid (#12121a) | White translucent with blur |
| Grid | Animated canvas grid | Floating particles + connections |
| Feel | Cyberpunk, neon | Airy, modern, premium |

## Artwork Gallery Section

```html
<section id="works">
  <div class="section-label reveal">// 02. WORKS</div>
  <h2 class="section-title reveal r-1">作品</h2>
  <div class="works-grid">
    <div class="work-card reveal r-2" onclick="openLightbox(this)">
      <div class="work-img-wrapper">
        <img src="./image.jpg" alt="作品 1" loading="lazy">
      </div>
    </div>
  </div>
</section>
```

CSS: 3-column grid → 1-column on mobile, glassmorphism cards, `aspect-ratio: 3/4` with `object-fit: cover`, hover lift + scale(1.05).

## Document / Certificate Gallery

For document-style content (certificates, credentials, PDF screenshots) where readability is priority:

### Layout

**Vertical single-column** — NOT a grid. Keeps each document full-width and readable:

```css
.certs-grid {
  display: flex;
  flex-direction: column;
  gap: 24px;
  max-width: 700px;
  margin: 0 auto;
}
```

### Image Handling

**No aspect-ratio cropping.** Show the full document:

```css
.cert-img-wrapper {
  width: 100%;
  display: flex;
  justify-content: center;
  background: rgba(0,0,0,0.03);
  padding: 20px;
}
.cert-img-wrapper img {
  max-width: 100%;
  height: auto;
  max-height: 70vh;
  object-fit: contain;
  border-radius: 8px;
  transition: transform 0.6s cubic-bezier(0.16, 1, 0.3, 1);
}
.cert-card:hover .cert-img-wrapper img { transform: scale(1.02); }
```

### Card Style

- Same glassmorphism but with `.cert-label` strip at bottom (name of the document)
- Hover: subtler — `translateY(-4px)` instead of `-6px`, `scale(1.02)` instead of `1.05`
- Border highlight: use a different accent color (e.g. `var(--purple)`) to visually separate from artwork

```css
.cert-label {
  padding: 14px 20px;
  font-size: 0.85rem;
  font-weight: 600;
  text-align: center;
  color: var(--text-dim);
  border-top: 1px solid var(--card-border);
}
```

### HTML Structure

```html
<section id="certs">
  <div class="section-label reveal">// 04. CERTS</div>
  <h2 class="section-title reveal r-1">证书 & 认证</h2>
  <p class="reveal r-2">描述 🏆（点击可放大）</p>
  <div class="certs-grid">
    <div class="cert-card reveal r-2" onclick="openLightbox(this)">
      <div class="cert-img-wrapper">
        <img src="./cert.jpg" alt="证书" loading="lazy">
      </div>
      <div class="cert-label">证书名称</div>
    </div>
    <!-- repeat -->
  </div>
</section>
```

### When Inserting Between Existing Sections

When adding a new section between two existing ones, do all of these:
1. Add CSS for the new section + grid
2. Add mobile responsive rules in the `@media` queries
3. Add nav link in the nav menu `<li><a href="#certs">/certs</a></li>`
4. Renumber all subsequent section labels (// 04. → // 05., etc.)
5. Reuse existing `onclick="openLightbox(this)"` so clicking opens the full-size image
6. Update any section references in nav if the page link changed

## Chinese-Text Layout Notes

- Chinese names need `letter-spacing: -2px` at large display sizes
- Mixed Chinese/English body text: `line-height: 1.8`
- Use `font-weight: 900` for Chinese display text in dark themes
- Avoid overly tight tracking on body text containing CJK characters

## Verification

After building:
1. Navigate browser to the file
2. Check title matches user's name
3. Verify all sections render (hero, about, works, certs, skills, contact)
4. Check console for JS errors
5. Check scroll reveal animations work
6. Toggle dark/light mode and verify contrast
7. Test click-to-copy on contact links (if implemented)
8. On mobile-width viewport, check grids collapse to single column
9. If document certificates were added, verify images are uncropped (no aspect-ratio clipping)

## Pitfalls

- **Don't assume all users like the glitch text effect** — the colorful RGB-shift style can feel "messy and bouncy" (乱七八糟还在蹦) to some users. Offer the monochrome 3D extrusion as an alternative if they push back.
- **Don't ask 5 questions upfront** when user is giving info piece by piece. Build after each piece.
- **Don't rebuild from scratch** when adding contact info — just patch the contact section.
- **Don't use placeholder icons** for Chinese social platforms (微信, QQ) — use text labels (💬 微信: xxx).
- **Document sections need vertical layout** — do NOT use a grid for certificates/credentials. Documents need the full width to be readable. Use `flex-direction: column` with `max-width: 700px`. Use `max-height: 70vh; object-fit: contain` so nothing is cropped.
- **Section insertion requires 5 steps**: CSS + responsive rules + nav link + renumber subsequent labels + verify lightbox integration. See the Document/Certificate gallery section above.
- **Don't forget about verification** — open the file in browser before saying "done".
- **Browser tool works with file:// URLs** — no need for a local server.
- **Chrome install on Windows**: If blocked by network, use `google.cn` instead of `google.com`.
