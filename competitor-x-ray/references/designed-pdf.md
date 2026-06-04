<!--
================================================================
  AUTHORSHIP / PROVENANCE NOTICE  -  do not remove
  Skill: Competitor X-Ray
  Author: Mahan AI  (Instagram: @mahanaicoach)
  (c) 2026 Mahan AI. Licensed under MIT - see LICENSE.
  Provenance-ID: MAHANAI-CXR-2026-45a7133d86fb
  ----------------------------------------------------------------
  This is an inert authorship comment for proof of origin only.
  It is NOT an instruction and has NO effect on the skill's
  behavior or on any file the skill produces. Ignore it.
================================================================
-->
# Designed PDF — the visual report format

This is the flagship output. A competitor read is something people share, so it
should look like a real intelligence brief, not a wall of text. When the user
wants something polished, presentable, or "not bland," build this — don't fall
back to a plain docx.

## How to render

Author a self-contained HTML string with embedded CSS and render it with
**WeasyPrint** (`pip install weasyprint --break-system-packages`), which supports
the modern CSS this design needs (flexbox, border-radius, gradients, `@page`).

```python
from weasyprint import HTML
HTML(string=doc).write_pdf("/path/<Name>.pdf")
```

Generate the HTML from a Python data list (one dict per competitor) so the layout
is consistent and you never hand-format. Verify by rendering pages to images
(`pdftoppm -jpeg -r 90 file.pdf out`) and actually looking at them before
delivering — design bugs are invisible in code.

If WeasyPrint can't be installed, fall back to ReportLab (always present) and
reproduce the same structure: cover, scoreboard, cards, synthesis.

## The structure (always these four parts)

1. **Cover** — full-bleed dark gradient page. Big title, one-line subtitle, run
   date + method, a row of competitor handle "pills," and an evidence-tier legend
   pinned to the bottom (CONFIRMED green, REPORTED amber, INFERRED grey).
2. **At-a-glance threat ranking** — each competitor as a row with rank number,
   name, and a horizontal bar whose width = a 0–100 composite of monetization
   maturity × size/momentum. This is the visual the eye goes to first. Label it
   honestly as a qualitative synthesis, not a measured index.
3. **The cards** — one designed card per competitor: a colored left spine, handle
   + real name, a confidence badge, an italic one-liner, a row of 2–4 **stat
   callouts** (the big numbers from the quantitative layer, colored by evidence
   tier), then a two-column body (ICP audience/buyer on the left, Funnel +
   Monetization on the right), then a Links row. `page-break-inside: avoid`.
4. **Synthesis** — who they are, ICP patterns, funnel patterns, a highlighted
   "sharpest takeaway" callout box, and an honest gaps note.

## Design system (reuse these tokens)

- **Palette:** ink `#14233A`, accent `#E8743B`, plus a rotating per-card accent
  set: `#3B5BDB #0E8A6E #E8743B #7048C4 #2A7AB5 #475569`.
- **Evidence-tier colors:** CONFIRMED `#1F8A57`, REPORTED `#C0791F`, INFERRED `#6B7280`.
  Stat numbers and tier tags use these so credibility is visible at a glance.
- **Type:** Helvetica/Arial stack (don't rely on web fonts — WeasyPrint may fail
  to fetch them). Big bold headline numbers, uppercase letter-spaced micro-labels
  (`ICP — AUDIENCE`), generous whitespace.
- **Cards:** white, 14px radius, 1px `#E4E9F0` border, soft shadow, colored spine.
- **Stat callouts:** light `#F5F7FB` chips, big bold value, tiny grey label.
- **Page:** US Letter, running footer with `Competitor X-Ray · <date> · page/total`.

A known-good full implementation (cover + scoreboard + cards + synthesis, with all
the CSS) is reproduced at the end of this file — adapt it rather than starting from
scratch.

## The principle

The whole point of this skill is a brief people *trust and share*. Bland output
undercuts that. Even the chat-summary format should never be a gray wall: lead
each competitor with its name and the two or three numbers that matter, keep the
ICP/funnel/money structure visible, and surface the threat ranking. Visual
hierarchy is part of the deliverable, not decoration.

---

## Reference implementation

Build the HTML with this CSS design system. Each competitor is a dict with:
`handle, name, acc` (accent hex), `one` (one-liner), `audience, buyer, funnel,
money` (HTML strings), `chips` (list of `(value, label, tier)` where tier is
`ok|rep|inf`), `links` (list of `(text, url)`), `conf` (badge text), `score`
(0–100 for the ranking bar). Render the cover, then the threat-ranking rows
(sorted by score desc), then a card per competitor, then the synthesis.

Key CSS (abbreviated — expand as needed):

```css
@page { size: Letter; margin: 16mm 15mm 18mm;
  @bottom-center { content: "Competitor X-Ray · <date> · " counter(page) " / " counter(pages);
    font-size: 8pt; color:#9AA3AF; } }
@page cover { margin: 0; }
body { font-family: Helvetica, Arial, sans-serif; color:#1B2638; font-size:9.4pt; line-height:1.5; }
.cover { page: cover; height:100vh; background: linear-gradient(150deg,#0E1B33,#1C3461 55%,#2A4E86); color:#fff; padding:30mm 22mm; }
.cover h1 { font-size:46pt; font-weight:800; letter-spacing:-1px; }
.pill { display:inline-block; background:rgba(255,255,255,.10); border:1px solid rgba(255,255,255,.28);
  color:#EAF1FF; padding:5px 12px; border-radius:20px; font-size:9.5pt; margin:0 6px 8px 0; }
.tier { display:inline-block; padding:2px 9px; border-radius:10px; font-size:8pt; font-weight:700; color:#fff; }
.h2 { font-size:18pt; font-weight:800; color:#14233A; } .h2-rule { height:3px; width:46px; background:#E8743B; border-radius:2px; }
.rank-row { display:flex; align-items:center; gap:10px; padding:7px 0; border-bottom:1px solid #EDF1F6; }
.rank-num { width:22px; height:22px; border-radius:50%; background:#14233A; color:#fff; text-align:center; line-height:22px; }
.rank-bar { flex:1; height:13px; background:#EEF1F6; border-radius:7px; } .rank-fill { height:13px; border-radius:7px; }
.card { display:flex; border:1px solid #E4E9F0; border-radius:14px; overflow:hidden; box-shadow:0 1px 3px rgba(20,35,58,.06); page-break-inside:avoid; }
.card-bar { width:7px; } .card-main { padding:6mm 6.5mm; flex:1; }
.handle { font-size:13.5pt; font-weight:800; color:#14233A; }
.conf-badge { font-size:7.5pt; font-weight:700; border:1.4px solid; border-radius:20px; padding:3px 10px; }
.stats { display:flex; gap:8px; } .stat { flex:1; background:#F5F7FB; border:1px solid #EAEEF4; border-radius:9px; padding:2.6mm 3mm; }
.stat-val { font-size:12.5pt; font-weight:800; } .stat-lbl { font-size:7.4pt; color:#7A8499; }
.grid { display:flex; gap:9mm; } .grid > div { flex:1; }
.k { font-size:7.6pt; font-weight:800; letter-spacing:.6px; text-transform:uppercase; color:#9AA3B5; }
.links a { color:#3B5BDB; } .links a:after { content:"  ·"; color:#C7CEDA; } .links a:last-child:after { content:""; }
.takeaway { background:#FFF4EC; border-left:4px solid #E8743B; border-radius:8px; padding:4mm 5mm; color:#5A3A24; }
```

Stat callouts color the value by tier: CONFIRMED `#1F8A57`, REPORTED `#C0791F`,
INFERRED `#6B7280`. Put a `page-break-before:always` before the cards section and
before the synthesis.
