# Competitor X-Ray — Full Guide

How the skill works under the hood, and how to squeeze the most value out of it.

---

## Part 1 — What it actually does

You hand it a list of competitors. It returns, for **each one**, a sourced read on three things:

- **ICP** — who they really sell to (and how that differs from who *follows* them)
- **Funnel** — the path a stranger takes to become a paying customer
- **Monetization** — every revenue stream, with real price points

Then it zooms out into a **cross-competitor synthesis**: shared patterns, where they diverge, and a **threat ranking** ordered by how built-out their money machine is *and* how fast they're growing.

It's not a chatbot guessing. It runs disciplined research, tags every claim by how trustworthy it is, and tells you what it *couldn't* verify instead of making something up.

---

## Part 2 — How it works, step by step

When you trigger it, here's the pipeline that runs:

**1. Normalize the targets.**
You can paste a messy mix — `@handle`, `instagram.com/...`, "Notion", `acme.com`. It sorts each into a social handle, a company name, or a website, and infers which is which. It even catches mistyped handles and chases the corrected spelling instead of giving up.

**2. Ask your output format + anchor.**
It asks two quick questions (as clickable options): which **format** you want (designed PDF / chat / spreadsheet / Word), and optionally **whose business to read the findings against** — so it can add a "what this means for you" angle.

**3. Fan out — one research agent per competitor, in parallel.**
This is the core trick. Each competitor gets its own dedicated research agent, all running at once. Each agent follows the same strict brief: search widely, pull from real sources, separate audience from buyer, map the funnel in stages, list every revenue stream with prices.

**4. Pull the quantitative layer.**
Qualitative reads ("they sell courses to founders") are only half the story. Each agent also gathers **2–3 real numbers** that show how big, how fast-growing, and how strong the competitor is:
- *Creators:* follower counts per platform (via Social Blade), engagement rate (HypeAuditor), posting cadence, newsletter subs.
- *Companies / SaaS:* funding (Crunchbase), headcount + open roles (LinkedIn), G2/Capterra review counts, self-reported ARR, traffic range.

Every number gets a **source and a date** — because a 2022 follower count is worthless.

**5. Tag every claim by evidence tier.**
This is what makes it trustworthy:
| Tier | Means | Example |
|---|---|---|
| 🟢 **CONFIRMED** | Seen on an owned/authoritative page | "Their pricing page says $97/mo" |
| 🟠 **REPORTED** | Stated but self-reported or third-party estimate, unaudited | "They *claim* $759K in 6 months" |
| ⚪ **INFERRED** | A reasoned guess | "They probably upsell a service" |

Self-reported revenue **never** gets passed off as fact.

**6. Synthesize.**
Once every brief is in, it writes the comparison: where everyone converges, where they split, the **threat ranking** (maturity × momentum, using the numbers — not vibes), and the single sharpest takeaway.

**7. Render in your chosen format.**
The flagship is the **designed PDF** — a branded intelligence brief with a cover, a visual threat-ranking with bars, one card per competitor (stat callouts colored by evidence tier), and a synthesis page. It renders the file and *looks at the pages* before handing it over.

---

## Part 3 — How gated profiles are handled

Instagram, TikTok, and LinkedIn block direct reading (login walls). The skill does **not** guess to fill the gap. Most real intel lives *outside* the social platform, so it works a fallback chain:

1. The target's **own website** (pricing, about, sales pages — least gated, highest value)
2. **Link-in-bio hubs** (Linktree, Stan, Beacons) — the fastest map of their whole funnel
3. **Community pages** (Skool, Whop, Circle) — public price + member count + ICP in their own words
4. **Newsletter/Substack** about pages — often expose subscriber counts
5. **Podcast appearances** — where people are most candid about real numbers
6. **Third-party analytics** (Social Blade, HypeAuditor, Similarweb-style search)
7. **Cached snippets** — Google's preview of the gated page itself

Only if a specific important fact still can't be found will it offer to open the profile in a logged-in browser (if you enable computer use). It never invents the missing fact.

---

## Part 4 — How to get the most out of it

### Phrase the request well
You don't need to name the skill. Just paste targets and say what you want. The more you specify, the better:

```
research @sabrina_ramonov @thedankoe gregisenberg — I want ICP, funnel, and
how each makes money, with the numbers. I run an AI automation agency, so tell
me what it means for me.
```

That single prompt gives it: the targets, the three pillars, the quant layer, **and** an anchor (your business) so the synthesis is actionable for *you*.

### Give it an anchor
When it asks "whose business should I read this against?" — **answer it.** A list of competitor facts is interesting; a list of facts plus "here's the gap between you and them" is a strategy. This is the difference between a report and a weapon.

### Pick the right output format
- **Designed PDF** → you're presenting, sharing, or pitching. This is the lead-magnet format. Use it when it needs to look like real intelligence.
- **Spreadsheet** → you have many competitors (5+) and want to scan them side by side. One row each, columns for ICP/funnel/offer/pricing/size.
- **Chat** → quick, you just want the read and the ranking now.
- **Word doc** → you'll edit it and hand it to a team or client.

### Right number of competitors
**3–6 is the sweet spot** — enough for real patterns in the synthesis, few enough that each gets deep research. One competitor is fine (it skips the comparison and just delivers a deep brief). 10+ is doable but lean toward the spreadsheet format.

### Read the evidence tiers, not just the numbers
A competitor "doing $2M/yr" tagged 🟠 REPORTED is a self-reported claim — treat it as order-of-magnitude. The same number 🟢 CONFIRMED off a filing is a fact. **The tier is half the information.** Don't make decisions off REPORTED numbers as if they were audited.

### Act on the threat ranking
The ranking blends *how built-out* their monetization is with *how fast* they're growing. A small but fast-growing competitor can outrank a bigger stagnant one — that's the one to watch. Use it to decide where to focus, not just to feel informed.

### Mine the Links directory
Every brief includes a **Links directory** — the competitor's own site, socials, podcast, community, store. This is the map of their funnel. Click straight into their lead magnet, their Skool page, their pricing — go see the machine yourself.

### Follow-up prompts that pay off
After the first run, push deeper:
- *"Go deeper on [competitor]'s funnel — what's their exact lead magnet → email → offer sequence?"*
- *"Compare just their pricing side by side."*
- *"What's the one move I could copy from the strongest one this week?"*
- *"Re-run [competitor] with computer use — I want the real follower count."*

### Enable computer use for gated numbers
If you need exact follower/engagement numbers for a private profile, turn on computer use (Settings → Desktop app → Computer use) and ask it to pull the profile live. Otherwise those numbers come back tagged REPORTED (estimated).

---

## Part 5 — What it will and won't promise

- It tells you **"not found"** instead of inventing a number. Absence of evidence is labeled as such.
- Exact website traffic is usually an order-of-magnitude **range** unless you have a paid SEO source — it won't fake precision.
- Gated follower counts without a logged-in browser are **estimates** (REPORTED).

That honesty *is* the product. A competitor read that confidently states fabricated pricing is worse than useless — this one holds the line so you can actually trust it.

---

*Built by [Mahan AI](https://instagram.com/mahanaicoach). Follow for more AI builds.*
