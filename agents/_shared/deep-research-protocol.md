# Deep Research Protocol

A structured methodology for compressing months of market/competitive research into hours. Used by the research-creator agent for any substantial market analysis, competitive landscape, or strategic research.

**When to use:** Market entry analysis, competitive landscapes, company evaluations, industry deep dives, due diligence, GTM strategy research. NOT for quick lookups or simple fact-finding.

## Philosophy

Most AI research fails because the questions are lazy. "Research market X" produces a Wikipedia-grade summary. The quality of output is entirely downstream of the quality of questions.

Two principles:
1. **Input-heavy, not prompt-heavy.** Load real artifacts first — the AI synthesizes, it doesn't search cold.
2. **Questions are a funnel.** Each layer forces deeper reasoning than the last.

---

## Phase 1: Artifact Loading

Before any analysis, collect and load real-world artifacts. The more concrete and specific, the better.

### Artifact Types (aim for 10-20 artifacts minimum)
| Type | Where to Find | What It Reveals |
|------|--------------|-----------------|
| Competitor landing pages | Web scrape top 5-8 players | Positioning, value props, pricing signals |
| Earnings call transcripts | SEC filings, Seeking Alpha | What leadership actually worries about |
| Customer reviews | G2, Capterra, TrustRadius, app stores | Unmet needs, real pain points |
| Complaint threads | Reddit, forums, Twitter/X | What vendors won't acknowledge |
| Job postings | LinkedIn, company careers pages | Where they're investing, org structure |
| Industry analyst reports | Gartner, Forrester, CB Insights | Market sizing, category definitions |
| Founder interviews | Podcasts, YouTube, conference talks | Origin stories, strategic bets |
| Patent filings | Google Patents | Technology direction, defensive moats |
| Pricing pages | Competitor websites | Business model, segmentation |
| Case studies | Vendor sites, press releases | Ideal customer profile, outcomes claimed |

### Loading Rules
- **Real artifacts only.** Don't ask the AI to imagine what a competitor's page says. Fetch it.
- **Use `web_fetch` and `web_search` aggressively.** Scrape landing pages, pull review content, find Reddit threads.
- **Save artifacts.** Store collected materials in a research folder for the project so they can be re-analyzed.
- **Check brain/ first.** Existing knowledge in `data/brain/` may already cover some artifacts (learn-030).
- **Note provenance.** Every artifact gets a source URL and access date.

---

## Phase 2: The Insight Funnel

Three questions, asked in sequence. Each builds on the last. Do NOT skip layers.

### Layer 1: Unspoken Truths
> "Based on these artifacts: what does every successful player in this market understand that their customers never say out loud?"

**What this reveals:** The implicit knowledge that separates winners from losers. The thing that takes founders 2 years of customer calls to figure out. This is the market's "open secret."

**Quality check:** If the answer sounds like it could come from a press release, it's too surface. Push deeper.

### Layer 2: Fragile Assumptions
> "What are the 3 assumptions this entire market is built on, and what would have to be true for each one to be wrong?"

**What this reveals:** The attack surface of the industry. The blind spots. The fragile consensus. The opening nobody is talking about.

**Quality check:** Each assumption should be specific and falsifiable. "Customers want good products" is not an assumption. "Enterprise buyers will pay 3-5x more for on-prem deployment" is.

### Layer 3: Investor Stress Test
> "Write 5 questions a world-class investor would ask to destroy this business idea, then answer each one using only the evidence in these artifacts."

**What this reveals:** Where the real risks are. Forces evidence-based answers, not hand-waving. Simulates the hardest conversation you'll have.

**Quality check:** The questions should make you uncomfortable. If they're softballs, the test failed.

---

## Phase 3: Stress Testing

For every weak answer from the Insight Funnel, apply the Strongest Version Test:

> "What's the strongest version of this argument, and where does it still break?"

### Rules
- **Iterate until convergence.** Keep asking until you can't find a break, or until the break is fundamental and irreducible.
- **No strawmanning.** The strongest version means the actual best case, not a version you set up to knock down.
- **Track the chain.** Each stress test round should reference which Layer 2/3 answer triggered it.
- **Maximum 3 rounds per argument.** If it hasn't converged by round 3, flag it as an unresolved risk.

### Output from Stress Testing
For each tested argument:
- The strongest version of the argument
- Where it still breaks (if it does)
- Confidence level: **solid** (survived 3 rounds), **conditional** (holds under specific assumptions), **fragile** (breaks under realistic conditions)

---

## Phase 4: Synthesis

Produce a strategy-grade artifact, not a summary dump.

### Required Sections
1. **Executive Insight** (3-5 sentences) — The single most important thing someone entering this market needs to know. Not a summary. An insight.
2. **Market's Open Secrets** — From Layer 1. What the winners know.
3. **Attack Surface Map** — From Layer 2. The assumptions, their fragility, and what breaks them.
4. **Risk Matrix** — From Layer 3 + stress testing. Each risk rated solid/conditional/fragile with evidence.
5. **Strategic Openings** — Where the market is vulnerable. What a new entrant (or [Your name]'s engagement) could exploit.
6. **Key Unknowns** — What we still don't know and how to find out.
7. **Artifact Index** — Every source used, with URL and access date.

### Quality Bar
- Every claim traceable to a specific artifact
- Confidence levels on every assertion
- "So what" on every finding — why does this matter for the specific use case?
- Minimum A- from research-critic to ship

---

## Integration with Atom of Thought

This protocol and AoT are complementary:
- **Deep Research Protocol** controls the *questioning strategy* — what to ask and in what sequence
- **Atom of Thought** controls the *reasoning rigor* — how each claim is validated

Use both. The funnel generates insights; AoT validates each one independently.

---

## When [Your agent name] Should Invoke This Protocol

[Your agent name] dispatches research-creator with this protocol when:
- [Your name] asks for market analysis on a new space
- A new engagement needs competitive intelligence ([Client B], [Client D], [Client C], etc.)
- Due diligence on a company or opportunity
- Any research where "just Google it" won't cut it

[Your agent name] should specify in the spawn prompt: "Follow the Deep Research Protocol (`agents/_shared/deep-research-protocol.md`)."
