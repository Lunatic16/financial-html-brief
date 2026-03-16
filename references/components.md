# Component Patterns

Reference HTML/CSS patterns for each section type. Copy and adapt — don't invent new patterns unless the content genuinely requires it. Consistency across briefs is a feature, not a limitation.

---

## Hero Section

The hero fills (approximately) 100vh and establishes the asset, current price, and key stats.

**Required elements:**
1. Label (asset class / report type / date)
2. H1 with asset name — use `<em>` for italic accent word in gold
3. Subtitle sentence
4. Price row: main price + 4–6 supporting stats
5. Risk classification badge (bottom-right)

**Price row stat types:** current price (large, gold), YoY %, YTD %, session high, 52-wk high, 52-wk low, spread, benchmark price.

```html
<div class="hero-price-row">
  <div class="hero-price-main">
    <div class="label">Asset Name (Context)</div>
    <div class="price">$103.73<span class="unit">/bbl</span></div>
  </div>
  <div class="hero-stat">
    <div class="label">YoY Return</div>
    <div class="val up">+46.1%</div>
  </div>
  <!-- repeat hero-stat for each metric -->
</div>
```

```css
.val.up { color: var(--green); }
.val.down { color: var(--red); }
.val.neutral { color: var(--blue); }
.hero-price-main .price { font-family:'IBM Plex Mono',monospace; font-size:56px; font-weight:600; color:var(--gold-bright); line-height:1; }
```

**Optionally** include an inline SVG analyst-price-target distribution chart below the price row. Map institutions to horizontal bars scaled to a min/max price axis. Include a vertical dashed line for the current price.

---

## Developments Feed

Ordered list of recent news items, most recent first. Each item has timestamp, headline, and impact tag.

```html
<div class="feed-item">
  <div class="feed-time">8 min ago</div>
  <div class="feed-headline"><strong>Event Title</strong> — Supporting context.</div>
  <div class="feed-impact impact-bullish">Very Bullish</div>
</div>
```

```css
.feed-item {
  display: grid;
  grid-template-columns: 120px 1fr auto;
  gap: 24px;
  align-items: start;
  padding: 24px 0;
  border-bottom: 1px solid var(--border);
  transition: background 0.2s;
}
.feed-item:hover { background: rgba(200,168,75,0.03); }
.feed-time { font-family:'IBM Plex Mono',monospace; font-size:11px; color:var(--text-dim); letter-spacing:0.05em; }
```

Impact tag options: `impact-bullish` (red) / `impact-bearish` (green) / `impact-neutral` (blue).

---

## Forecast Grid

3-column grid of bank/analyst price targets.

```html
<div class="forecast-grid"> <!-- 3-col 1px-gap grid -->
  <div class="forecast-card [highlight]">
    <div class="forecast-inst">Goldman Sachs</div>
    <div class="forecast-price">$71 avg / $100+</div>
    <div class="forecast-note">Explanatory note about the forecast and conditions.</div>
    <div class="forecast-bar" style="width:80%;"></div>
  </div>
</div>
```

The `.forecast-bar` is a 2px absolute line at the bottom of each card. Its width (as % of card) should be proportional to the forecast price relative to the range across all forecasts. Animate it from `width:0` to the target width on load.

Add `class="highlight"` to the highest-conviction or most-cited forecast cards.

```css
.forecast-card { background:var(--card); padding:28px; position:relative; overflow:hidden; }
.forecast-card.highlight { background:#1e1a12; }
.forecast-inst { font-family:'IBM Plex Mono',monospace; font-size:11px; color:var(--text-dim); letter-spacing:0.1em; text-transform:uppercase; margin-bottom:12px; }
.forecast-price { font-family:'IBM Plex Mono',monospace; font-size:36px; font-weight:600; color:var(--gold); line-height:1; margin-bottom:10px; }
.forecast-note { font-size:12px; color:var(--text-muted); line-height:1.5; }
.forecast-bar { position:absolute; bottom:0; left:0; height:2px; background:var(--gold); transition:width 1s ease; }
```

Override `.forecast-price` color for outliers: bearish targets → `var(--green)`, high-end targets → `var(--red)`.

---

## Scenario Boxes

3 side-by-side scenario panels: bear (resolution/downside), base (current), bull (escalation/upside).

```html
<div class="scenarios-row"> <!-- 3-col 1px-gap grid, background:var(--border) -->
  <div class="scenario-box bear">
    <div class="scenario-label">Bear / Resolution</div>
    <div class="scenario-range">$70–80</div>
    <div class="scenario-desc">Trigger condition and price rationale.</div>
    <div class="scenario-prob">TRIGGER: Specific catalyst</div>
  </div>
  <div class="scenario-box base">...</div>
  <div class="scenario-box bull">...</div>
</div>
```

```css
.scenario-box.bear  { background:#111a14; }
.scenario-box.base  { background:#1a1710; }
.scenario-box.bull  { background:#1a1111; }
.scenario-label { font-family:'IBM Plex Mono',monospace; font-size:10px; letter-spacing:0.2em; text-transform:uppercase; margin-bottom:16px; }
.bear .scenario-label  { color:var(--green); }
.base .scenario-label  { color:var(--gold); }
.bull .scenario-label  { color:var(--red); }
.scenario-range { font-family:'Playfair Display',serif; font-size:42px; font-weight:900; line-height:1; margin-bottom:16px; }
.scenario-prob { margin-top:20px; font-family:'IBM Plex Mono',monospace; font-size:10px; color:var(--text-dim); letter-spacing:0.1em; }
```

---

## Risk Tables

Use tabs to separate bull risks, bear risks, and geopolitical matrix. See design-system.md for tab component.

**Risk table structure:**

```html
<table class="risk-table">
  <thead>
    <tr>
      <th>Risk Factor</th><th>Impact</th><th>Probability</th><th>Assessment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Factor Name</strong></td>
      <td>Specific impact</td>
      <td><span class="prob-badge prob-high">Med-High</span></td>
      <td>Assessment sentence.</td>
    </tr>
  </tbody>
</table>
```

```css
.risk-table { width:100%; border-collapse:collapse; }
.risk-table th { font-family:'IBM Plex Mono',monospace; font-size:10px; color:var(--text-dim); letter-spacing:0.1em; text-transform:uppercase; padding:12px 16px; text-align:left; font-weight:400; }
.risk-table td { font-size:13px; padding:18px 16px; border-bottom:1px solid var(--border); vertical-align:top; line-height:1.5; }
.risk-table tr:hover td { background:rgba(255,255,255,0.02); }
```

**Geopolitical matrix** — use a 2-column grid instead of a table:

```html
<div class="geo-grid"> <!-- 2-col 1px-gap grid -->
  <div class="geo-item">
    <div class="geo-actor">Actor Name</div>
    <div class="geo-pos">Position / role description.</div>
    <div class="geo-impact geo-vbull">Very Bullish</div>
  </div>
</div>
```

Geo impact classes: `geo-vbull` (red) / `geo-bull` (orange) / `geo-bear` (green) / `geo-neut` (blue) / `geo-unc` (muted).

---

## Technical Levels

Two-column layout: left = visual level bars, right = pattern analysis + target bands grid.

```html
<div class="level-row">
  <div class="level-label">Resistance</div>
  <div class="level-bar-wrap">
    <div class="level-bar-fill" style="width:100%; background:var(--red);"></div>
  </div>
  <div class="level-val" style="color:var(--red);">$119.50</div>
</div>
```

```css
.level-row { display:flex; align-items:center; gap:16px; padding:14px 0; border-bottom:1px solid var(--border); }
.level-label { font-family:'IBM Plex Mono',monospace; font-size:10px; color:var(--text-dim); letter-spacing:0.08em; text-transform:uppercase; width:110px; flex-shrink:0; }
.level-bar-wrap { flex:1; height:2px; background:var(--border); position:relative; }
.level-bar-fill { height:100%; background:var(--gold); transition:width 1.2s ease; }
.level-val { font-family:'IBM Plex Mono',monospace; font-size:13px; font-weight:600; color:var(--text); min-width:80px; text-align:right; }
```

Bar widths are relative: map prices to a 0–100% scale between the overall low and high. Current price gets `var(--gold-bright)`. Resistance gets `var(--red)`. 52-wk low gets `var(--green)`.

**Target bands grid** — 2×2 inline grid of scenario targets:
```html
<div style="display:grid; grid-template-columns:1fr 1fr; gap:1px; background:var(--border);">
  <div style="background:var(--card); padding:20px;">
    <div style="font-family:'IBM Plex Mono',monospace; font-size:9px; color:var(--text-dim); margin-bottom:8px; letter-spacing:0.1em; text-transform:uppercase;">Scenario Name</div>
    <div style="font-family:'IBM Plex Mono',monospace; font-size:24px; font-weight:600; color:var(--gold);">$100–110</div>
  </div>
</div>
```

---

## Catalyst List

Numbered list with hover animation.

```html
<div class="catalyst-item">
  <div class="catalyst-num">01</div>
  <div class="catalyst-content">
    <strong>Catalyst Title</strong>
    <p>One or two sentences on why this matters and what to watch for.</p>
  </div>
</div>
```

```css
.catalyst-item { display:flex; align-items:flex-start; gap:20px; padding:22px 0; border-bottom:1px solid var(--border); transition:padding-left 0.25s; cursor:pointer; }
.catalyst-item:hover { padding-left:12px; }
.catalyst-num { font-family:'IBM Plex Mono',monospace; font-size:13px; color:var(--gold-dim); width:28px; flex-shrink:0; padding-top:2px; }
.catalyst-content strong { display:block; font-size:14px; font-weight:500; color:var(--text); margin-bottom:4px; }
.catalyst-content p { font-size:12px; color:var(--text-muted); line-height:1.6; }
```

---

## Verdict Section

Two-column layout: prose analysis (left) + metadata scorecard (right).

```html
<div class="verdict-body">
  <div class="verdict-text">
    <p>Paragraph 1 — main conclusion.</p>
    <p>Paragraph 2 — key variable / inflection point.</p>
    <p>Paragraph 3 — forward-looking statement / timeline.</p>
    <p style="color:var(--text-dim); font-size:12px; margin-top:24px;">Sources: ...</p>
  </div>
  <div class="verdict-meta"> <!-- 1px border box -->
    <div style="/* header row */"> SUMMARY METRICS </div>
    <div class="verdict-meta-row">
      <span class="meta-k">Confidence</span>
      <span class="meta-v gold">High</span>
    </div>
    <!-- repeat rows -->
  </div>
</div>
```

```css
.verdict-body { display:grid; grid-template-columns:1.2fr 0.8fr; gap:64px; align-items:start; }
.verdict-text p { font-size:15px; color:var(--text-muted); line-height:1.85; margin-bottom:16px; font-weight:300; }
.verdict-text strong { color:var(--text); font-weight:500; }
.verdict-meta { border:1px solid var(--border); padding:28px; }
.verdict-meta-row { display:flex; justify-content:space-between; align-items:center; padding:12px 0; border-bottom:1px solid var(--border); }
.verdict-meta-row:last-child { border-bottom:none; }
.meta-k { font-family:'IBM Plex Mono',monospace; font-size:10px; color:var(--text-dim); letter-spacing:0.1em; text-transform:uppercase; }
.meta-v { font-family:'IBM Plex Mono',monospace; font-size:12px; font-weight:600; }
.meta-v.gold { color:var(--gold); }
.meta-v.red  { color:var(--red); }
.meta-v.green { color:var(--green); }
```

Scorecard rows to include (where data available):
Confidence · Risk Level · Current Price · Fair Value Range · Bull Target · Bear Target · Key Timeline · [Asset-specific status] · Updated

---

## Footer

```html
<footer>
  <div class="footer-note">
    This report is for informational purposes only and does not constitute investment advice...
  </div>
  <div class="footer-brand">
    [Asset] Strategic Brief<br>
    [Date]<br>
    Prepared for [Audience]
  </div>
</footer>
```

```css
footer { padding:40px 48px; border-top:1px solid var(--border); max-width:1280px; margin:0 auto; display:flex; justify-content:space-between; align-items:center; }
.footer-note { font-size:11px; color:var(--text-dim); line-height:1.6; max-width:500px; }
.footer-brand { font-family:'IBM Plex Mono',monospace; font-size:10px; color:var(--text-dim); letter-spacing:0.1em; text-align:right; }
```
