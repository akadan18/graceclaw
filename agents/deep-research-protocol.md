# Deep Research Protocol

Compress months of market/competitive research into hours.
Use for: market analysis, competitive landscapes, company evaluations, due diligence, GTM research.
NOT for: quick lookups or simple fact-finding.

## Philosophy

Most AI research fails because the questions are lazy. "Research market X" produces a Wikipedia-grade summary. Quality of output is entirely downstream of quality of questions.

Two principles:
1. **Input-heavy, not prompt-heavy.** Load real artifacts first — the AI synthesizes, it doesn't search cold.
2. **Questions are a funnel.** Each layer forces deeper reasoning than the last.

---

## Phase 1: Artifact Loading

Collect 10–20 real-world artifacts before any analysis.

| Type | Where to Find | What It Reveals |
|------|--------------|-----------------|
| Competitor landing pages | Scrape top 5-8 players | Positioning, value props, pricing signals |
| Earnings call transcripts | SEC filings, Seeking Alpha | What leadership actually worries about |
| Customer reviews | G2, Capterra, TrustRadius, app stores | Unmet needs, real pain points |
| Complaint threads | Reddit, forums, X/Twitter | What vendors won't acknowledge |
| Job postings | LinkedIn, company careers pages | Where they're investing, org structure |
| Analyst reports | Gartner, Forrester, CB Insights | Market sizing, category definitions |
| Founder interviews | Podcasts, YouTube, conference talks | Origin stories, strategic bets |
| Pricing pages | Competitor websites | Business model, segmentation |
| Case studies | Vendor sites, press releases | Ideal customer profile, claimed outcomes |

**Rules:**
- Real artifacts only — don't ask the AI to imagine what a competitor's page says
- Use `web_fetch` and `web_search` aggressively
- Save collected materials in a research folder (they can be re-analyzed)
- Check `data/brain/` first — existing knowledge may already cover some artifacts
- Note provenance: every artifact gets a source URL and access date

---

## Phase 2: The Insight Funnel (3 layers — do NOT skip)

### Layer 1: Unspoken Truths
> "Based on these artifacts: what does every successful player in this market understand that their customers never say out loud?"

**What this reveals:** The implicit knowledge that separates winners from losers. The thing that takes founders 2 years of customer calls to figure out.

**Quality check:** If it sounds like it could come from a press release, push deeper.

### Layer 2: Fragile Assumptions
> "What are the 3 assumptions this entire market is built on, and what would have to be true for each one to be wrong?"

**What this reveals:** The attack surface of the industry. Blind spots. Fragile consensus. The opening nobody is talking about.

**Quality check:** Each assumption must be specific and falsifiable. "Customers want good products" is not an assumption. "Enterprise buyers will pay 3-5x more for on-prem deployment" is.

### Layer 3: Investor Stress Test
> "Write 5 questions a world-class investor would ask to destroy this business idea, then answer each one using only the evidence in these artifacts."

**What this reveals:** Where the real risks are. Forces evidence-based answers, not hand-waving.

**Quality check:** The questions should make you uncomfortable. Softballs mean the test failed.

---

## Phase 3: Stress Testing

For every weak answer from the Insight Funnel, apply:

> "What's the strongest version of this argument, and where does it still break?"

**Rules:**
- Maximum 3 rounds per argument
- No strawmanning — the strongest version means the actual best case
- Track the chain: each round references which Layer 2/3 answer triggered it
- After 3 rounds: flag as **solid** (survived), **conditional** (holds under assumptions), or **fragile** (breaks under realistic conditions)

---

## Phase 4: Synthesis Output

Strategy-grade artifact, not a summary dump.

**Required sections:**
1. **Executive Insight** (3-5 sentences) — The single most important thing someone entering this market needs to know. An insight, not a summary.
2. **Market's Open Secrets** — From Layer 1
3. **Attack Surface Map** — From Layer 2: each assumption, its fragility, what breaks it
4. **Risk Matrix** — From stress testing: rated solid/conditional/fragile with evidence
5. **Strategic Openings** — Where the market is vulnerable
6. **Key Unknowns** — What we don't know and how to find out
7. **Artifact Index** — Every source, URL, and access date

**Quality bar:**
- Every claim traceable to a specific artifact
- Confidence levels on every assertion
- "So what" on every finding — why does this matter for the specific decision?
- Minimum A- from the relevant critic before shipping
