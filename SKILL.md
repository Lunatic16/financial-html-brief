---
name: financial-html-brief
description: >
  Converts financial research, market data, or investment analysis (in any format — markdown, uploaded docs, raw notes, CSV data) into a polished, interactive HTML presentation ready for VP or senior stakeholder review. Use this skill whenever the user wants to: turn a market report into a presentation, create an investor brief or one-pager, make research "presentable" for a meeting, output an interactive HTML from financial data or analysis, or produce a Bloomberg-terminal-style dashboard from notes or documents. Trigger even when the user says things like "make this presentable", "clean this up for my VP", "create a brief from this", "turn this into a deck" or "generate an HTML from this research". Always use this skill for finance-related HTML output.
---

# Financial HTML Brief

Converts financial research or market analysis into a polished, interactive HTML presentation for senior stakeholder review.

## Core Design System

Always use the dark financial terminal aesthetic defined in `references/design-system.md`. Read it before writing any code.

## Workflow

### Step 1 — Parse the Input

Identify from the user's content:
- **Asset / subject**: What is being analyzed (equity, commodity, macro theme, fund, etc.)
- **Key price data**: Current price, % changes, ranges, benchmarks
- **Sections present**: Forecasts, scenarios, risks, catalysts, technicals, geopolitical actors, verdict
- **Time sensitivity**: Any live/breaking developments that should be flagged

If the input is a file, read it fully before proceeding.

### Step 2 — Map Content to Sections

Use the section map below. Include only sections for which content exists. Never leave a section empty or with placeholder text.

| Content Type | HTML Section |
|---|---|
| Price / headline metrics | Hero with live stats row |
| Breaking news / recent events | Developments Feed |
| Bank / analyst forecasts | Forecast Grid |
| Upside / base / downside | Scenario Boxes |
| Risk factors with probability | Risk Table (tabbed by bull/bear/geo) |
| Technical levels / support / resistance | Technical Levels with bar chart |
| Catalysts / watch items | Numbered Catalyst List |
| Summary / recommendation | Verdict with metadata scorecard |

### Step 3 — Build the HTML

Read `references/design-system.md` for the full CSS variable set, component patterns, and layout rules, then produce a **single self-contained HTML file** that:

1. Embeds all CSS and JS inline (no external files except Google Fonts)
2. Uses the IBM Plex Mono + Playfair Display font pairing
3. Includes a scrolling ticker tape with key price data
4. Includes sticky navigation with section anchors
5. Uses scroll-reveal animations on each section
6. Is fully responsive down to 768px width
7. Passes the **VP-readiness checklist** (see below)

### Step 4 — VP-Readiness Checklist

Before outputting, verify:
- [ ] No placeholder text ("Lorem ipsum", "TBD", "N/A" without reason)
- [ ] All prices and percentages are formatted consistently (e.g., `$103.73`, `+46.1%`)
- [ ] Color coding is consistent: red = bullish pressure / upside risk, green = bearish / resolution, gold = neutral/current, blue = informational
- [ ] Risk table has probability badges on every row
- [ ] Verdict section has a populated metadata scorecard
- [ ] Disclaimer present in footer
- [ ] Date and data source attribution present

## Section Components

Detailed HTML patterns for each component are in `references/components.md`. Read it when building a section you haven't built yet in this session.

## Ticker Tape Content

Extract 6–8 key data points for the ticker. Ideal items:
- Asset name + current price + % change
- Session high / low
- YTD or YoY performance
- A relevant benchmark (gold, USD index, spread, etc.)
- Status of a key macro factor (e.g., "HORMUZ STATUS: ~10% CAPACITY")

Duplicate the content once so the tape loops seamlessly.

## Naming Conventions

- File: `[asset-slug]-[context]-brief.html` (e.g., `brent-crude-vp-brief.html`)
- Section IDs: `overview`, `developments`, `forecasts`, `scenarios`, `risks`, `technicals`, `catalysts`, `verdict`
- Tab IDs for risk section: `bull-risks`, `bear-risks`, `geo-matrix`

## Output

Save to `/mnt/user-data/outputs/` and present with `present_files`. Confirm the file is self-contained and opens correctly in a browser without any external dependencies beyond Google Fonts.
