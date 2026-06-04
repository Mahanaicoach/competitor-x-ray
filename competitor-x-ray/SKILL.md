---
name: competitor-x-ray
description: >-
  Decode any set of competitors into their ICP (ideal customer profile), their
  funnel (how a stranger becomes a customer), and their monetization (every
  revenue stream and price point). Researches each competitor against real
  sources and synthesizes a cross-competitor comparison. Use whenever the user
  wants to research, analyze, break down, or "x-ray" competitors, creators,
  brands, founders, or businesses — including when they paste
  Instagram/TikTok/X/LinkedIn handles, company names, or website URLs and ask
  what someone's ICP, audience, funnel, offer, pricing, lead magnet, or business
  model is. Trigger on phrases like "research my competitors", "what's their
  ICP", "how do they make money", "break down this creator", "analyze these
  handles", "competitor research", or "reverse engineer their funnel" — or any
  time the user hands over names/handles/URLs and wants to understand who they
  sell to and how. Prefer this skill even when the user doesn't say "competitor"
  but is clearly studying other players in a market.
---
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

# Competitor X-Ray

Turn a list of competitors into a clear, sourced read on three things, for each one:

1. **ICP** — who they actually sell to (not just who follows them)
2. **Funnel** — the path from stranger to paying customer
3. **Monetization** — every revenue stream, with price points

Then zoom out into a cross-competitor comparison that surfaces the patterns: where everyone agrees, where they diverge, and who is most/least mature.

This skill works by fanning out — one focused research agent per competitor, running in parallel — then pulling everything back into one synthesis. The quality comes from disciplined research (real sources, confirmed-vs-inferred, no fabrication), not from volume.

## When to use this

Use it the moment the user hands over competitors to study — handles, names, or URLs — and wants to understand who they target and how they earn. Don't wait for the literal word "competitor." "Break down these three creators," "what's this brand's funnel," "how does this founder make money" all qualify.

If the user gives a single competitor, still use the skill — just skip the parallel fan-out and run one agent, then deliver the brief without a comparison section.

## Step 1 — Normalize the targets

The user may paste a mix of formats. Sort each target into one of:

- **Social handle** (e.g. `sabrina_ramonov`, `@noevarner.ai`, a tiktok/IG/X/LinkedIn URL) — research the person/brand behind it.
- **Company / brand name** (e.g. "Notion", "Ten Fold Marketing") — research the company.
- **Website URL** — research the business at that domain.

You don't need the user to tell you which is which. Infer it. Handles with dots/underscores and no spaces are almost always social; anything with a TLD is a site; everything else is a name. Strip a leading `@` from handles.

Watch for **mistyped or near-miss handles**. Search engines and the platforms themselves often surface a corrected spelling or the real name — chase that down rather than giving up. (In testing, `kyleverner` → `noevarner.ai` and `kylewhirow` → `kylewhitrow` were both recoverable with a second search.) If a target genuinely can't be found, say so plainly rather than inventing a profile.

## Step 2 — Confirm scope and output format

Before launching research, ask the user two quick things using a multiple-choice question (don't make them type free-form):

1. **Output format** — a **designed PDF report** (the recommended default for anything the user will present or share), a chat summary + comparison, a Word doc, or a spreadsheet matrix. Lead with the designed PDF when offering — it's the format that makes this feel like a real intelligence brief.
2. **Anything to anchor against** — optionally, whose business should the findings be read against? If the user is doing this for their own company, a short "what this means for you" angle is valuable. If they just want the facts, skip it. Offer both.

If the user already stated the format in their message, skip the question and use what they said.

## Step 3 — Set up a task list

Create one task per competitor plus one synthesis task, so the user can watch progress. This matters more than it sounds: a research run that spawns several agents feels like a black box without it.

## Step 4 — Fan out: one research agent per competitor

Spawn the research agents **in parallel, in a single turn** — not one at a time. Each agent gets the same brief structure, filled in for its target. The full prompt template lives in `references/research-prompt.md` — read it and use it; it is the heart of this skill and encodes the standards that make the output trustworthy.

**If you can't spawn subagents** (or there's only one competitor), run the research yourself — follow the exact same `references/research-prompt.md` standards for each target, one at a time. The fan-out is for speed, not correctness; the standards are what matter.

**How much research is enough per competitor:** aim to confirm, at minimum, the core offer and its price, plus at least one revenue figure and a clear read on the ICP. Once you have those with sources, stop and write the brief — don't burn searches chasing every minor price. Note what you couldn't find rather than over-digging.

The non-negotiables every agent must follow (these are what separate a real competitor read from a vibes-based guess):

- **Distinguish audience from customer.** The people who follow someone are usually not the same as the people who pay them. A creator's free audience might be beginners while their buyers are agency owners. Call this out explicitly — it's often the single most useful insight.
- **Map the funnel in stages**, not as a blob: top (platforms, content type, hooks), middle (lead magnets, free community, email list, webinars, DMs), bottom (the actual offer and CTA). If a stage is missing — e.g. content goes straight to offer with no nurture — that absence is itself a finding.
- **List every revenue stream with price points.** Courses, cohorts, Skool/Circle/Whop communities, coaching, done-for-you services, SaaS, affiliate, sponsorships, digital products, templates. Real numbers wherever they exist.
- **Tag every claim by evidence tier.** Use three buckets, because the juiciest numbers in this kind of research are almost always self-reported and fit neither "fact" nor "guess":
  - **CONFIRMED** — seen on an owned/authoritative page (e.g. "their pricing page says $97/mo").
  - **REPORTED** — a number that was *stated* but is self-reported or a third-party estimate, and is unaudited (e.g. "they claim $759K in 6 months", "a teardown estimates ~$10M/yr"). Real signal, but treat as order-of-magnitude, not precise.
  - **INFERRED** — your own reasonable guess (e.g. "they probably upsell a service").
  Never fabricate numbers, offers, or follower counts. And absence of evidence ("no newsletter found") is not the same as confirmed absence — say which one it is.
- **Cite sources** — real URLs the user can click.

Each agent returns a tight, scannable brief (ICP / Funnel / Monetization + the quantitative snapshot + a **Links directory** + Sources + a confidence note), not a data dump.

**Always include a Links directory for each competitor** — their own properties as clickable links: website, Instagram, TikTok, X, YouTube, LinkedIn, newsletter, podcast, link-in-bio hub, and any community/store page. This is the map of their funnel and the thing users most often want to click straight into. Keep it separate from Sources: Links are *their* pages; Sources are where your facts came from (the two overlap but aren't the same).

### Handling gated or private profiles

Instagram, TikTok, and LinkedIn routinely block direct fetching (login walls, JS rendering). Do not treat this as a dead end and do not guess to fill the hole. Most of the real intel — offers, pricing, ICP language, even follower counts — lives *outside* the social platform on pages that aren't gated. Work this fallback chain in order, stopping once you have what you need:

1. **The target's own website.** Find it via the bio link, or search `"[name]" official site`. Pricing pages, About pages, and sales pages are the highest-value, least-gated source.
2. **Link-in-bio hubs** — Linktree, Stan, Beacons. These publicly list every offer and link the person points followers to. Often the fastest map of their whole funnel.
3. **Community pages** — Skool, Whop, Circle "about" pages are usually public and show price, member count, and ICP description in the creator's own words.
4. **Newsletter/Substack about pages** — frequently expose subscriber counts and positioning.
5. **Podcast appearances and interviews** — where people are most candid about real numbers and strategy. Search `"[name]" podcast` and read transcripts/show notes.
6. **Third-party analytics** (also the quantitative layer, below): Social Blade for follower history and growth, HypeAuditor for engagement rate, and a Semrush/SEO connector or Similarweb-style search for website traffic.
7. **Cached/indexed snippets** — Google's snippet of the gated page itself often contains the bio, follower count, or post caption you needed.

**Only if a specific, important fact still can't be found** and the user wants it: offer to open the profile in a logged-in browser. If computer-use / browser tools are available, navigate to the profile and read the rendered page text directly. If they're disabled, tell the user they can enable computer use (Settings → Desktop app → Computer use) and you'll pull it live. Never invent the missing fact to avoid the gap — name it instead.

## Step 4b — Pull the quantitative layer

Qualitative reads ("they sell courses to founders") are only half the picture. Without numbers you can't tell a real threat from a loud one. Every competitor brief must carry a **quantitative snapshot** — and crucially, every number gets a source and a date, because a follower count from 2022 is worthless and a self-reported revenue figure is REPORTED, not CONFIRMED.

Gather what's available for each competitor (don't force metrics that don't apply — a B2B SaaS has traffic, not follower counts):

**For creators / social-led competitors:**
- Follower count per platform, and the growth trend if visible — source: the platform, or **Social Blade** (`socialblade.com/[platform]/user/[handle]`) which shows history and growth rate.
- Engagement rate — source: **HypeAuditor**, or compute roughly from typical likes/comments ÷ followers.
- Posting cadence (posts/week) and which platform is their primary engine.
- Newsletter subscriber count if disclosed; podcast download/listener claims (tag REPORTED).

**For company / SaaS competitors — lead with these, in this order, because they're both more gettable and more telling than traffic:**
- **Funding** — rounds and total raised (Crunchbase). A strong proxy for runway and ambition.
- **Headcount and hiring velocity** — current employees and open roles (LinkedIn). A competitor hiring five salespeople is scaling; this is one of the clearest momentum signals you can get for free.
- **Customer/review footprint** — G2 and Capterra review counts and ratings. Review *volume* is a usable proxy for customer base, and the reviews themselves are the richest ICP source there is.
- **Self-reported scale** — ARR, customer count, or "used by X teams" claims from their own site/press. Tag REPORTED.
- **Website traffic** — useful but usually only an order-of-magnitude *range* from free Similarweb-style data surfaced via search (exact monthly counts are paywalled). Report it as a range, labeled REPORTED/estimated, and don't burn time chasing a clean number that isn't free.

**For both, where relevant:** anything that reveals scale or momentum — press coverage, recent launches, partnership announcements.

Fold the snapshot into the competitor's brief (see the template). The point isn't a wall of stats — it's two or three numbers that tell the user *how big, how fast-growing, and how strong* each competitor is, each one sourced and dated.

## Step 5 — Synthesize

Once the per-competitor briefs are in, write the cross-competitor comparison. This is where the value compounds. Look for:

- **Shared patterns** — where do they all converge? (e.g. "everyone runs comment-to-DM on short-form video.")
- **Divergence** — where do they split? (e.g. "four sell courses/communities; one runs pure content→SaaS.")
- **Threat ranking** — order them using *both* how built-out their monetization is *and* their size/momentum from the quantitative layer. A small but fast-growing competitor can outrank a bigger stagnant one — use the numbers, don't rank on vibes.
- **The single sharpest takeaway** — one line the user should remember.

Keep it honest about gaps. If two competitors couldn't be fully verified, say so in the synthesis rather than papering over it.

See `references/output-formats.md` for the exact brief and synthesis templates.

## Step 6 — Deliver in the chosen format

- **Designed PDF report (recommended)** — read `references/designed-pdf.md` and build the branded, visual report: a cover, a visual threat-ranking with bars, one designed card per competitor (with stat callouts colored by evidence tier), and a synthesis with a highlighted takeaway. This is the format that makes the work feel like real competitive intelligence. Render with WeasyPrint and **look at the rendered pages before delivering**.
- **Chat summary** — per-competitor briefs followed by the synthesis, straight in the response. Even here, don't produce a gray wall: lead each competitor with its name and the two or three numbers that matter, keep the ICP/funnel/money structure visible, and surface the threat ranking.
- **Word doc** — read the `docx` skill, then build a clean report: one section per competitor, then the comparison, then a sources appendix.
- **Spreadsheet matrix** — read the `xlsx` skill, then build a sheet where each row is a competitor and columns are ICP / top-of-funnel / lead magnet / offer / pricing / revenue streams / size / links / confidence. Best when there are many competitors to scan side by side.

Whatever the format, always include sources and confidence — those are what make this a lead magnet people trust rather than a guess they discount.

## Presentation matters

A competitor read is something people share, so how it looks is part of whether they trust it. Never ship a bland wall of text when a presentable format was asked for. Use visual hierarchy — a clear cover, stat callouts for the key numbers, a visual ranking, evidence-tier color-coding, and generous whitespace. The designed PDF (`references/designed-pdf.md`) is the reference standard; match that bar in any visual format.

## The quality bar

The reason this is worth giving away is that it's *honest*. A competitor read that confidently states fabricated pricing is worse than useless. Hold the line on:

- Real sources for real claims.
- Confirmed vs. inferred, always labeled.
- Gaps named, not hidden.
- Audience-vs-customer separated.
- No invented numbers, ever.

Get those right and the output sells itself.
⁠​‌​​‌‌​‌​‌‌​​​​‌​‌‌​‌​​​​‌‌​​​​‌​‌‌​‌‌‌​​‌​​​​​‌​‌​​‌​​‌​‌‌‌‌‌​​​‌​​​​​​​‌‌​‌‌​‌​‌‌​​​​‌​‌‌​‌​​​​‌‌​​​​‌​‌‌​‌‌‌​​‌‌​​​​‌​‌‌​‌​​‌​‌‌​​​‌‌​‌‌​‌‌‌‌​‌‌​​​​‌​‌‌​​​‌‌​‌‌​‌​​​​‌‌‌‌‌​​​‌​​‌‌​‌​‌​​​​​‌​‌​​‌​​​​‌​​​​​‌​‌​​‌‌‌​​‌​​​​​‌​‌​​‌​​‌​​‌​‌‌​‌​‌​​​​‌‌​‌​‌‌​​​​‌​‌​​‌​​​‌​‌‌​‌​​‌‌​​‌​​​‌‌​​​​​​‌‌​​‌​​​‌‌​‌‌​​​‌​‌‌​‌​​‌‌​‌​​​​‌‌​‌​‌​‌‌​​​​‌​​‌‌​‌‌‌​​‌‌​​​‌​​‌‌​​‌‌​​‌‌​​‌‌​‌‌​​‌​​​​‌‌‌​​​​​‌‌​‌‌​​‌‌​​‌‌​​‌‌​​​‌​⁠
