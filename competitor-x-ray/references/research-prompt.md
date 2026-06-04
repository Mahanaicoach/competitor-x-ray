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
# Research-agent prompt template

Use this as the prompt for each per-competitor research subagent. Fill in the
bracketed fields. Launch all agents in parallel in a single turn.

The wording here is deliberate — it pushes the agent to verify against real
sources, separate audience from customer, and refuse to fabricate. Keep those
intact when you adapt it.

---

```
Research the [competitor type: Instagram creator / brand / business] "[TARGET]"
([known URL if any]). [One line of any context you already have — likely real
name, niche, where they operate.] This is a competitor being studied.

Use web search heavily. Look across the target's own website, Instagram,
TikTok, YouTube, X/Twitter, LinkedIn, Linktree/Stan store, newsletter, and any
course / cohort / community (Skool, Circle, Whop) pages, plus podcast
appearances and interviews. Try the handle, the likely real name, and terms
like "course", "community", "agency", "skool", "newsletter", "pricing".

If the handle looks mistyped or returns nothing, search for the corrected
spelling or the real name before giving up. If the target genuinely can't be
found, say so plainly — do not invent a profile.

I need three things, each with concrete evidence and source URLs:

1. ICP (Ideal Customer Profile): Who is their audience/customer? Be specific —
   role, business stage, niche, pain points, demographics. Critically,
   distinguish their AUDIENCE (followers/viewers) from their PAYING CUSTOMERS if
   the two differ — they usually do.

2. FUNNEL: How do they take a stranger to a customer? Map the stages — top of
   funnel (platforms, content type, hooks), middle (lead magnets, free
   community, email list, webinars, DMs), bottom (the actual offer and CTA). If
   a stage is missing, note its absence.

3. MONETIZATION: Every revenue stream you can find — courses, cohorts,
   communities (Skool/Circle/Whop), coaching, agency/done-for-you services,
   SaaS, affiliate, sponsorships, digital products, templates. Include price
   points and tiers wherever they exist.

4. QUANTITATIVE SNAPSHOT: two or three real numbers that show how big, how
   fast-growing, and how strong this competitor is — each with a source and a
   date. For a creator: follower count per platform + growth trend (open the
   Social Blade page directly — socialblade.com/[platform]/user/[handle] — for a
   CONFIRMED count and history rather than relying on a search snippet),
   engagement rate (HypeAuditor), posting cadence, newsletter subs if disclosed.
   For a company/SaaS, lead with the gettable, telling metrics: funding
   (Crunchbase), headcount + open roles (LinkedIn), G2/Capterra review counts
   and rating, and any self-reported ARR/customer count (tag REPORTED). Website
   traffic is usually only a free order-of-magnitude range from Similarweb-style
   search data — report it as a range, labeled REPORTED, and don't chase an exact
   number that's paywalled. Don't force metrics that don't apply; a SaaS has
   funding and headcount, not follower counts.

Rules:
- Tag each claim by evidence tier:
  - CONFIRMED — seen on an owned/authoritative page (e.g. their pricing page).
  - REPORTED — a number that was stated but is self-reported or a third-party
    estimate, unaudited (e.g. "they claim $759K in 6 months"). Real signal, but
    order-of-magnitude, not precise.
  - INFERRED — your own reasonable guess.
- Never fabricate numbers, prices, offers, or follower counts.
- "Not found" is not the same as "confirmed absent" — say which it is.
- If social profiles are gated/login-walled, pull the same facts from owned
  pages (website, store, Skool, podcasts) and third-party analytics instead.

5. LINKS / WHERE TO FIND THEM: a directory of the competitor's own properties,
   with clickable URLs — website, every active social profile (Instagram,
   TikTok, X, YouTube, LinkedIn, Facebook), newsletter/Substack, podcast,
   link-in-bio hub (Linktree/Stan/Beacons), and any community (Skool/Whop/Circle)
   or store/checkout page. This is the map of their funnel touchpoints, so the
   user can go look themselves. List only links you actually found; don't pad
   with guessed URLs.

Return a tight, scannable brief — ICP / Funnel / Monetization / Quantitative
snapshot / Links — each a few sentences or short bullets — plus a "Sources" list
of the URLs you cited and a one-line confidence note. Keep the LINKS directory
(their own properties) separate from SOURCES (where your facts came from); they
overlap but serve different purposes. Do not dump raw search results.
```

---

## Notes for the orchestrator

- One agent per competitor. With many competitors, launching all at once is fine;
  if you hit timeouts, run them in two waves rather than serially.
- Pass along any context you already have (real name, niche) so the agent doesn't
  waste a search rediscovering it.
- When an agent reports a corrected handle or a disambiguation (two people share a
  name), carry that correction into the final synthesis so the user sees it.
