# financial-html-brief

A Claude/Gemini/Qwen skill that converts financial research, market data, and investment analysis into polished, interactive HTML presentations — ready for VP or senior stakeholder review.

This skill is meant to be used in tandem with the [Deep Financial Reasearch Skill](https://github.com/Lunatic16/deep-financial-research).

---

## What it does

Drop in a markdown report, uploaded document, CSV data, or raw notes. The skill produces a single self-contained HTML file with:

- **Scrolling ticker tape** populated with key price data
- **Sticky navigation** with anchor links to each section
- **Hero section** with large price display and supporting stat row
- **Developments feed** — live events ordered by recency, each tagged with directional impact
- **Analyst forecast grid** — bank price targets with animated proportion bars
- **Scenario boxes** — Bear / Base / Bull with price targets and trigger conditions
- **Tabbed risk tables** — Bull risks, Bear risks, and a Geopolitical Matrix
- **Technical levels** — visual bar chart of support/resistance levels
- **Catalyst watchlist** — numbered, hover-animated list
- **Verdict** — prose analysis with a metadata scorecard sidebar
- **Scroll-reveal animations** throughout

Everything is inline — no build step, no dependencies beyond Google Fonts. Open the file in any browser.

---

## Example output

The `example/` folder contains a full Brent Crude Oil brief generated from a markdown research document:

👉 **[View live example](example/brent-crude-oil-vp-presentation.html)**

![Brief preview showing dark terminal aesthetic with gold ticker tape, price hero, and developments feed](example/preview-description.md)

The example was generated from [`example/brent-crude-oil-analysis-march-2026.md`](example/brent-crude-oil-analysis-march-2026.md) with a single prompt:

> *"Make this markdown into an interactive HTML for presentation to my VP at an investment bank"*

---

## Design system

The brief uses a consistent dark financial terminal aesthetic:

| Token | Value | Usage |
|---|---|---|
| `--gold` / `--gold-bright` | `#c8a84b` / `#e8c870` | Current price, neutral/baseline, section numbers |
| `--red` | `#e05252` | Bullish pressure, upside risk, escalation |
| `--green` | `#4caf7d` | Bearish signal, resolution, downside |
| `--blue` | `#6ab0e8` | Informational, range forecasts |
| `--card` | `#1c1c1c` | Card backgrounds |
| `--border` | `#2a2a2a` | Dividers, grid gaps |

**Fonts:** [Playfair Display](https://fonts.google.com/specimen/Playfair+Display) (headings) + [IBM Plex Mono](https://fonts.google.com/specimen/IBM+Plex+Mono) (prices, labels, data) + [IBM Plex Sans](https://fonts.google.com/specimen/IBM+Plex+Sans) (body copy).

---

## Skill structure

```
financial-html-brief/
├── SKILL.md                      # Main skill instructions + workflow
└── references/
    ├── design-system.md          # CSS variables, typography, animation patterns
    └── components.md             # HTML/CSS patterns for every section type
```

The skill uses progressive loading — Claude reads `design-system.md` before writing any code, and consults `components.md` for each section to maintain visual consistency across briefs.

---

## Trigger phrases

The skill activates on prompts like:

- *"Make this presentable for my VP"*
- *"Turn this research into a brief"*
- *"Create an investor one-pager from this"*
- *"Generate an HTML from this analysis"*
- *"Clean this up for the meeting"*
- *"Build a Bloomberg-style dashboard from these notes"*

---

## Installing the skill

1. Download [`financial-html-brief.skill`](financial-html-brief.skill)
2. In Claude, open **Settings → Skills**
3. Click **Install skill** and select the `.skill` file
4. The skill is now available in any conversation

---

## What to feed it

The skill handles any of these input formats:

| Input | Works? |
|---|---|
| Markdown research document | ✅ |
| Uploaded PDF or Word doc | ✅ |
| Raw notes / bullet points | ✅ |
| CSV with price/forecast data | ✅ |
| Pasted text from a terminal or Bloomberg | ✅ |
| Already-structured HTML | ✅ (reformats to this design system) |

The skill maps whatever sections exist in your content to the appropriate HTML components. If your input has no technical levels, that section is omitted — no empty placeholders.

---

## VP-readiness checklist

Before outputting, the skill verifies:

- No placeholder text anywhere in the document
- Prices and percentages formatted consistently (`$103.73`, `+46.1%`)
- Color coding applied correctly throughout
- Probability badges on every risk table row
- Verdict scorecard fully populated
- Disclaimer and data source attribution in the footer

---

## Adapts to asset class

While the example is a commodity brief, the skill works across asset classes. The section set adapts to whatever data is present:

- **Equities** — EPS forecasts, P/E comps, earnings catalysts
- **Fixed income** — yield curves, spread analysis, central bank catalysts
- **Macro / FX** — rate differentials, positioning data, policy risks
- **Private markets** — deal comps, IRR scenarios, GP/LP dynamics
- **Crypto** — on-chain metrics, exchange flow data, regulatory risks

---

## Files

| File | Description |
|---|---|
| `financial-html-brief.skill` | Installable skill package |
| `SKILL.md` | Main skill source |
| `references/design-system.md` | Full CSS design system reference |
| `references/components.md` | HTML/CSS component library |
| `example/brent-crude-oil-vp-presentation.html` | Full example output |
| `example/brent-crude-oil-analysis-march-2026.md` | Source document used for example |

---

## License

MIT — use freely, adapt for your own asset classes or house style.
