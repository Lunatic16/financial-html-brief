# Design System Reference

## CSS Variables

```css
:root {
  --black: #0a0a0a;
  --off-black: #111111;
  --dark: #161616;
  --card: #1c1c1c;
  --border: #2a2a2a;
  --border-light: #333;
  --gold: #c8a84b;
  --gold-bright: #e8c870;
  --gold-dim: #7a6530;
  --red: #e05252;
  --green: #4caf7d;
  --blue: #6ab0e8;
  --text: #e8e2d6;
  --text-muted: #8a8070;
  --text-dim: #555045;
}
```

## Typography

| Role | Font | Weight | Size |
|---|---|---|---|
| Display headings (h1, h2) | Playfair Display, serif | 700–900 | 32px–96px |
| Monospace labels, prices, data | IBM Plex Mono, monospace | 400, 600 | 9px–56px |
| Body copy, descriptions | IBM Plex Sans, sans-serif | 300, 400, 500 | 12px–15px |

Google Fonts import:
```html
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700;900&family=IBM+Plex+Mono:wght@400;600&family=IBM+Plex+Sans:wght@300;400;500&display=swap" rel="stylesheet">
```

**Never use**: Inter, Roboto, Arial, system-ui, or any other generic sans-serif.

## Color Semantics

| Color | Variable | When to Use |
|---|---|---|
| Gold | `--gold`, `--gold-bright` | Current price, neutral/baseline, section numbers, nav brand |
| Red | `--red` | Bullish oil pressure, upside risk, escalation, "Very Bullish" tags |
| Green | `--green` | Bearish oil signals, resolution/downside, "Bearish" tags |
| Blue | `--blue` | Informational/neutral, range forecasts, session stats |
| Muted text | `--text-muted`, `--text-dim` | Labels, subtitles, secondary content |

## Page Structure

```
[ Ticker Tape — fixed, 32px, gold bg ]
[ Navigation — fixed, 52px, dark bg + blur ]
[ Main content — padding-top: 84px ]
  [ Hero section ]
  [ Section 01 — Developments ]
  [ Section 02 — Forecasts ]
  [ Section 03 — Scenarios ]
  [ Section 04 — Risks ]
  [ Section 05 — Technicals ]
  [ Section 06 — Catalysts ]
  [ Section 07 — Verdict ]
[ Footer ]
```

Alternate section backgrounds: odd sections use `var(--black)`, even sections use `var(--off-black)`. Max content width: 1280px, centered.

## Standard Section Header

Every section opens with this pattern:
```html
<div class="section-header">
  <span class="section-num">01</span>
  <h2 class="section-title">Section Name</h2>
</div>
```

```css
.section-header {
  display: flex;
  align-items: baseline;
  gap: 20px;
  margin-bottom: 40px;
  padding-bottom: 20px;
  border-bottom: 1px solid var(--border);
}
.section-num {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 11px;
  color: var(--gold-dim);
  letter-spacing: 0.1em;
}
.section-title {
  font-family: 'Playfair Display', serif;
  font-size: 32px;
  font-weight: 700;
  color: var(--text);
}
```

## Scroll Reveal Animation

Add `class="reveal"` to any container. Include this CSS and JS:

```css
.reveal {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}
.reveal.visible { opacity: 1; transform: translateY(0); }
```

```js
const observer = new IntersectionObserver(
  entries => entries.forEach(el => { if (el.isIntersecting) el.target.classList.add('visible'); }),
  { threshold: 0.1 }
);
document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
```

## Hero Entry Animation

Use staggered `animation-delay` for hero elements:

```css
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}
/* Apply with: animation: fadeUp 0.7s 0.3s forwards; */
/* Start with: opacity: 0; */
```

Typical stagger: label 0.2s → h1 0.3s → subtitle 0.4s → price row 0.55s → risk badge 0.7s.

## Ticker Tape

Fixed at top, 32px, gold background, black text. Use IBM Plex Mono 11px, uppercase.

```css
.ticker-wrap { position:fixed; top:0; left:0; right:0; z-index:100; background:var(--gold); height:32px; overflow:hidden; }
.ticker-content { display:flex; align-items:center; height:100%; white-space:nowrap; animation: ticker 28s linear infinite; }
.ticker-item { font-family:'IBM Plex Mono',monospace; font-size:11px; font-weight:600; color:var(--black); padding:0 32px; letter-spacing:0.05em; }
.ticker-item span { opacity:0.6; margin-right:8px; }
@keyframes ticker { 0%{transform:translateX(0)} 100%{transform:translateX(-50%)} }
```

Duplicate all items so the loop is seamless.

## Navigation

Fixed below ticker (top: 32px), 52px height, dark background with `backdrop-filter: blur(12px)`.

Include:
- Left: brand name in IBM Plex Mono gold
- Center: anchor links in IBM Plex Mono 10px uppercase
- Right: pulsing "LIVE" badge in red if content is time-sensitive; otherwise date badge in gold

```css
@keyframes pulse { 0%,100%{opacity:1} 50%{opacity:0.6} }
.nav-badge { font-family:'IBM Plex Mono',monospace; font-size:10px; background:var(--red); color:#fff; padding:3px 10px; letter-spacing:0.1em; animation:pulse 2s infinite; }
```

## Grid Patterns

**1px-gap grids** (used for forecast cards, scenario boxes, geo matrix):
```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(N, 1fr);
  gap: 1px;
  background: var(--border); /* gap becomes visible border */
}
.grid-item { background: var(--card); } /* items cover the gap color */
```

## Impact / Probability Badges

```css
/* Impact tags on developments feed */
.impact-bullish { color:var(--red);   border:1px solid rgba(224,82,82,0.3);   background:rgba(224,82,82,0.06); }
.impact-bearish { color:var(--green); border:1px solid rgba(76,175,125,0.3);  background:rgba(76,175,125,0.06); }
.impact-neutral { color:var(--blue);  border:1px solid rgba(106,176,232,0.3); background:rgba(106,176,232,0.06); }

/* Probability badges on risk table */
.prob-high { color:var(--red);          border:1px solid rgba(224,82,82,0.35); }
.prob-med  { color:var(--gold);         border:1px solid rgba(200,168,75,0.35); }
.prob-low  { color:var(--green);        border:1px solid rgba(76,175,125,0.35); }
/* All use: font-family:'IBM Plex Mono'; font-size:10px; padding:3px 10px; letter-spacing:0.06em; */
```

## Tab Component

```html
<div class="tabs">
  <button class="tab-btn active" onclick="switchTab(event,'tab-id-1')">Label 1</button>
  <button class="tab-btn" onclick="switchTab(event,'tab-id-2')">Label 2</button>
</div>
<div id="tab-id-1" class="tab-panel active">...</div>
<div id="tab-id-2" class="tab-panel">...</div>
```

```js
function switchTab(e, id) {
  document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
  document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
  e.target.classList.add('active');
  document.getElementById(id).classList.add('active');
}
```

## Background Radial Accent (Hero)

Add atmospheric depth to the hero with:
```css
.hero::before {
  content: '';
  position: absolute;
  top: -200px; right: -200px;
  width: 700px; height: 700px;
  background: radial-gradient(circle, rgba(200,168,75,0.07) 0%, transparent 70%);
  pointer-events: none;
}
```
