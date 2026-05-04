# Ygramul + Codex Architecture Reference (v2 — 11-Lever)

**Audience:** Internal — handoff document for future Claude chats picking up Ygramul work.
**Purpose:** Skip ~30 minutes of context rebuild. Capture the framework, the Codex, the RAG architecture, the agent layer, and the open questions in one place.
**Source of truth for the methodology:** [github.com/IvanNon/ygramul-methodology](https://github.com/IvanNon/ygramul-methodology) (`README.md` + `LEVERS.md`).
**Last updated:** May 4, 2026 — rebuilt from scratch to align with the 11-lever model. Replaces the v1 doc that referenced 7 Levers.

---

## How to use this doc

This is a reference, not a runbook. Future Claude chats should read it once, internalize the structure, and then move to whatever workstream Ivan is asking for. If a downstream doc (Doc 2 lever framework deep, Path B handoff, Path C-Narrow manual, Path A architecture spec) contradicts this one, **this doc wins** unless Ivan or the GitHub repo says otherwise.

If `LEVERS.md` in the GitHub repo has been updated since this doc was last touched, **`LEVERS.md` wins**. This doc is downstream of the public methodology repo, not the other way around.

---

## Part 1 — What Ygramul is

Ygramul is Rush Media Agency's proprietary methodology and product for enterprise technical SEO and GEO (Generative Engine Optimization). It is structured around eleven levers, grounded in a primary-source Codex, and designed to learn from each engagement so the rules sharpen with use rather than going stale.

The name comes from the spider in Michael Ende's *The Neverending Story* — a nod to the fact that search crawlers are, themselves, spiders. The methodology mirrors how those crawlers work: many simultaneous angles, no single source of truth, judgment emerging from the pattern across signals rather than any one of them.

The framing that distinguishes Ygramul from a checklist audit:

- **Findings are tied to hypotheses.** Each recommendation predicts what should move, by how much, on what timescale.
- **Hypotheses are designed to be tested.** Outcomes are measured at consistent cadences (typically 30/60/90 days post-implementation).
- **Outcomes update the rules.** Patterns that consistently predict outcomes get reinforced. Patterns that consistently fail get demoted. The version of Ygramul applied to a new engagement is more accurate over time.

This is what the README means by *AI-native rather than AI-assisted*. Without AI, the loop is theoretical. With AI, it becomes operationally realistic.

The target buyer is a Director, VP, or Head of SEO at a $5M–$500M ARR company with a complex technical stack — headless CMS, multilingual rollouts, programmatic content surfaces, active GEO exposure. Ygramul is calibrated for sites in the 100,000+ URL range. Smaller or simpler sites can run a subset of the levers; the framework is granular by intent and not the right tool for every site.

---

## Part 2 — The eleven levers

The full chapter-by-chapter detail lives in `LEVERS.md`. This section is the compressed reference.

### Three groupings

**Engagement levers (1–9)** — sequenced work done during a client engagement. Run in dependency order. Each unblocks the next.

**Long-arc lever (10)** — Brand & Search Demand Generation. Operates on multi-year timescales and runs in parallel to engagement work, not sequenced after it.

**Cross-engagement lever (11)** — Auto-Research & Outcome Measurement. Operates across the full client base and feeds back to update the rules used in Levers 1–10.

### The compressed table

| # | Lever | Group | Senior-practitioner bucket |
|---|---|---|---|
| 1 | Crawl Architecture | Engagement | Find and index |
| 2 | Canonical Architecture | Engagement | Find and index |
| 3 | Page Technical Signals | Engagement | Find and index |
| 4 | Keyword Strategy & Opportunity Modeling | Engagement | Rank |
| 5 | Content Production & Optimization | Engagement | Rank |
| 6 | Programmatic SEO | Engagement | Rank |
| 7 | Internal Link Architecture | Engagement | Rank |
| 8 | Authority, Trust & GEO Visibility | Engagement | Rank |
| 9 | Local SEO & Google Business Profile | Engagement | Rank |
| 10 | Brand & Search Demand Generation | Long-arc (parallel) | Measure and learn |
| 11 | Auto-Research & Outcome Measurement | Cross-engagement (loop) | Measure and learn |

### Why the order matters

Optimizing for AI citation before fixing crawl waste is wasted effort — the citation signals can't reach pages the crawler isn't indexing reliably. Running programmatic SEO before fixing canonical architecture multiplies the problem rather than solving it. The order is not arbitrary.

The most common cross-lever finding is a Lever 1 + Lever 2 issue: phantom URLs (Lever 1 crawl waste) compounded by canonical bugs (Lever 2). Standard sequencing: fix canonicals first, validate crawl recovery, then move to Lever 3.

### Two structural notes worth carrying forward

**Findings cross levers.** A canonical loop on a programmatic page is both a Lever 2 and Lever 6 issue. A schema gap on author pages is both a Lever 3 and Lever 8 issue. When a finding crosses levers, name both, then sequence the fix by dependency order. *"Issue at Lever X compounds with issue at Lever Y. Fix Y first, then validate X recovery."*

**Lever 11 is recursive, not sequential.** It observes everything Levers 1–10 produce, scores outcomes, and updates the rules used by Levers 1–10 in subsequent engagements. This is the differentiator. A checklist runs the same way regardless of outcome history. Ygramul updates its own priors as evidence accumulates.

### What Ygramul deliberately does not cover

Naming what's out of scope is more honest than implying everything is in scope. Ygramul does not cover ICP development, conversion rate optimization beyond surfacing friction, public relations and demand-generation execution, multi-location franchise SEO at enterprise scale, paid search, or lifecycle marketing. The exclusions are deliberate.

---

## Part 3 — The Codex

Underneath the levers sits the Codex — a curated library of primary sources that grounds the recommendations Ygramul produces.

### What it is

132 primary sources across 15 categories. Examples: the May 2024 Google Search API leak (Rand Fishkin / SparkToro, with Mike King / iPullRank's technical companion), DOJ antitrust testimony synthesis, Google patents, Search Central documentation, foundational ML/IR papers, peer-reviewed GEO and AI-search research.

### Why it exists

Most SEO advice circulates as inherited wisdom. *"Google likes X"* gets repeated for years without anyone being able to point at why. The Codex is the discipline of insisting that recommendations have citations — a leaked document, a patent, a peer-reviewed paper, a piece of antitrust testimony, a Search Central page. When a finding says *"missing dateModified weakens freshness signals,"* the Codex tells you which source supports that claim and how strong the evidence is.

### Citation convention

- First mention per section: **"Ygramul Codex"** in full
- Subsequent mentions in the same section: **"the Codex"**
- Citations: **`Codex #[number]`** (hash format, not section symbol — chosen for developer-audience compatibility)

### V1 deferral

For V1 deliverables (and the in-flight Ygramul Doc Set), citation numbers are deferred. Use source names instead — *"the March 2024 Google API leak,"* *"the DOJ antitrust testimony,"* *"the Karpathy auto-research framework."* Switch to `Codex #[number]` once RAG is wired and citation lookup is automatic. This is a locked decision in the handoff.

### Architectural status

The Codex is implemented as a vector database used as a RAG layer for audits, briefs, and recommendations. The architecture is published. The source list is not.

---

## Part 4 — The RAG and agent architecture

### Tech stack (locked)

- **LLM:** Anthropic Claude API direct. No LangChain. Claude Opus 4.6 / 4.7 for complex agents (Technical SEO triage, Auto-Research). Claude Sonnet 4.6 for high-volume tasks (content briefs, optimization). Claude Haiku 4.5 for routing and simple classification.
- **Vector DB:** Supabase (PostgreSQL + pgvector). Free tier viable for V1 / small client base. Supabase Pro at scale.
- **Embeddings:** Voyage or OpenAI text-embedding-3-small (decision deferred to build sprint).
- **Frontend:** Next.js 14 App Router + TypeScript + Tailwind on Vercel.
- **Auth:** Clerk with `growth_lead` and `client` roles.
- **Secrets:** Supabase Vault.
- **Backend host:** Railway (recommended, TBD at build time).
- **Prompt caching:** Day 1.
- **Model routing:** Week 2 (Haiku → Sonnet → Opus by complexity).
- **Batch API:** Month 2 (for auto-research loops).

### Why RAG over fine-tuning

The Codex is a knowledge library with citation requirements. That's a textbook RAG use case, not fine-tuning.

- Citations work natively — retrieval returns `Codex #47` with the relevant chunk
- Updating the Codex = re-embedding one document, not retraining anything
- Costs ~$0.10 to embed the whole corpus once, then pennies per query
- Fine-tuning teaches *style and behavior*, not *facts*. Models hallucinate fine-tuned facts.

The hybrid pattern — RAG for factual retrieval + light fine-tuning (or strong system prompt) for output format and Ygramul voice — is the long-term plan, but V1 is RAG-only.

### Agent inventory

The published Claude Skills are the open-source surface:

| Skill | Lever addressed | Status | Repo |
|---|---|---|---|
| Schema Detector | 3 (Page Technical Signals) | Public | `IvanNon/schema-detector-skill` |
| Ygramul AIO Cascade | 5 (Content Production & Optimization) | Public | `IvanNon/ygramul-aio-cascade` |

The proprietary surface — used in active engagements but not published:

| Agent | Primary lever(s) | Risk routing | Notes |
|---|---|---|---|
| Technical SEO Triage Agent | 1, 2, 3 | LOW/HIGH classifier | v3 system prompt locked. Outputs Execution Routing OR High-Risk Proposal |
| Execution Agent | 1, 2, 3 | LOW-RISK only | Writes meta titles, descriptions, alt text, schema, internal links direct to staging via CMS API |
| High-Risk Proposal Agent | 2, 3 | HIGH-RISK only | Outputs BEFORE/AFTER diffs for Growth Lead manual implementation. Canonicals, robots.txt, redirects, hreflang, sitemaps, any change affecting 50+ pages |
| Keyword Research Agent | 4 | n/a | Clusters by intent + commercial value, scores by traffic potential × difficulty |
| Content Brief Agent | 5 | n/a | Generates briefs against Lever 4 roadmap |
| Content Optimization Agent | 5 | LOW-RISK | Surfaces decay, generates AIO opener blocks (delegates to AIO Cascade skill) |
| Programmatic SEO Agent | 6 | HIGH-RISK | Template design and small-batch validation. Bulk deployment requires Growth Lead approval |
| Internal Link Agent | 7 | LOW-RISK | Anchor text optimization, orphan page resolution |
| GEO Visibility Agent | 8 | n/a | Tracks LLM citations across ChatGPT, Perplexity, Gemini, AI Overviews on a 3-day cadence |
| Local SEO Agent | 9 | n/a | GBP monitoring, citation consistency, review cadence |
| Measurement Agent | 11 | n/a | GSC monitoring at Day 7/30/90 post-implementation |
| Auto-Research Agent | 11 | n/a | Karpathy loop. Updates agent prompts monthly from outcome scores |

### The execution loop

The architectural diagram, in words:

```
DETECT (Triage Agent)
    ↓
CLASSIFY (LOW-RISK or HIGH-RISK)
    ↓                              ↓
EXECUTE on staging           PROPOSE to Growth Lead
(Execution Agent + CMS API)  (BEFORE/AFTER diff)
    ↓                              ↓
Growth Lead approves         Growth Lead implements
    ↓                              ↓
DEPLOY to production         DEPLOY to production
    ↓                              ↓
MEASURE (Measurement Agent at Day 7/30/90 via GSC)
    ↓
RELEARN (Auto-Research Agent monthly Karpathy loop)
    ↓
UPDATE agent prompts → next engagement runs on updated rules
```

This is the loop the README is gesturing at when it says *"designed to learn from each engagement so the rules sharpen with use rather than going stale."*

### Hybrid risk classification (locked)

- **LOW-RISK** (Execution Agent → staging direct): meta titles, meta descriptions, alt text, schema markup, H1 changes, internal link additions
- **HIGH-RISK** (Proposal → Growth Lead manual): canonicals, robots.txt, redirects, hreflang, sitemaps, any change affecting 50+ pages, any structural change
- **Confidence threshold:** Findings below 60% confidence are not routed. They surface in the Triage Agent's session summary as "needs human review."

---

## Part 5 — The auto-research loop

This is Lever 11 in operation. It is the framework's primary differentiator and the reason "methodology" rather than "checklist" is the right framing.

### How the loop runs

1. **Baseline.** Every recommendation produced by Levers 1–10 is tied to a measurable hypothesis. The hypothesis names the metric, the predicted direction, the predicted magnitude, and the timescale.
2. **Implementation.** Either via Execution Agent (LOW-RISK) or Growth Lead (HIGH-RISK). Implementation is logged with timestamp.
3. **Evaluation.** The Measurement Agent pulls GSC data at Day 7, 30, and 90 post-implementation. Outcomes are scored: Win, Neutral, Regression.
4. **Update.** The Auto-Research Agent runs monthly across all engagements. It looks for patterns: which finding categories predict outcomes most reliably? Which fail? It produces prompt updates for the agents that generated the findings.

### Status calibration (per `LEVERS.md`)

The auto-research loop is **designed and partially operational**. Outcome measurement on individual findings happens today across active engagements. The cross-engagement pattern recognition layer — where findings from one engagement inform recommendations on another — is being instrumented, not yet running at full scale.

Ygramul is honest about this in the public methodology. It is a working framework that is *designed to learn*. It is not yet a system that has learned across hundreds of engagements. That is the goal, not the current reality.

### The pattern the loop is designed to produce

A recommendation category — for example, "add Person schema for content authors" — generates findings across multiple engagements. Outcomes get measured 30/60/90 days after implementation. After enough measured outcomes, a pattern emerges: the recommendation produces strong AI-search citation lift on engagements where the author has existing external authority signals (verified LinkedIn, external publications, professional associations) and minimal lift on engagements where the author is anonymous. The methodology updates: Person schema additions get flagged as high-confidence when external authority signals are present, low-confidence when they aren't. The next engagement runs on the updated rule.

This is what conditional rules look like. They are the output of cumulative measurement, not the output of consensus opinion.

### Why the loop fails when it fails

- **Recommendations shipped without measurable hypotheses.** No hypothesis = no scoring = no learning.
- **Outcome measurement on too short a horizon.** A 7-day check on a fix that compounds over 90 days underrates slow-acting work.
- **Pattern recognition overfit to recency.** Latest 10 outcomes weighted more than the prior 100. A bad month in algorithm noise discards rules that were working.
- **Auto-research treated as a backend process invisible to engagements.** The framework updates rules, but updates don't surface back to active audit work. Learning is generated and lost.

---

## Part 6 — Build phases

This is the build path Ygramul is on, by phase.

### Phase 1 — V1 / Foundation tier (CURRENT)

Service tier: $10K/month. Target: 2–3 pilot clients in active onboarding through Q3 2026. Dina Osman is Product Owner.

**What's operational:**
- Two public Claude Skills (Schema Detector, AIO Cascade) — open-source surface
- Manual audit delivery using the Ygramul methodology, supported by Claude in chat
- Codex available as RAG-ready content (132 sources distilled)
- Technical SEO Triage Agent v3 prompt locked
- Execution Agent, Measurement Agent prompts locked
- Karpathy auto-research loop conceptually defined; manual runs in flight

**What's not yet operational:**
- Cross-engagement pattern recognition layer
- Production CMS API integrations (Webflow targeted first, then WordPress + RankMath, Contentful, Sanity, Shopify)
- Multi-client orchestration (single agent pool vs. per-client agents — open question)
- Codex publication (50 entries first vs. wait for full 132 — open question)

### Phase 2 — Growth tier ($15K/month)

- Add programmatic SEO production
- Add GEO Visibility tracking at production scale
- Auto-research loop running across the client base
- Multi-client orchestration architecture decided and shipped

### Phase 3 — Enterprise (custom)

- Full agent ensemble running per-client
- Custom CMS integrations
- Per-client auto-research loops feeding back into client-specific rule updates as well as cross-client framework updates

### Phase 4 — Self-serve SaaS

- Per-domain or per-finding pricing
- Public Codex with `Codex #[number]` citation lookup
- Schema Detector and AIO Cascade as productized tools on the Rush Media website
- Open question: per-domain, per-finding, or flat retainer for SaaS tier

---

## Part 7 — Open questions

Not yet decided. These compound across downstream docs and should be flagged whenever they touch a workstream.

1. **Production CMS API integrations.** Which platforms first? Webflow is the leading candidate (Rush Media's own stack). WordPress + Yoast/RankMath is the largest install base. Contentful and Sanity are the headless market. Shopify is e-commerce. The order depends on which client comes first.

2. **Multi-client orchestration.** Single agent pool that any client engagement can draw from, or per-client agents that maintain client-specific context across sessions? The single-pool approach is cheaper and simpler. The per-client approach maintains continuity better. Decision deferred until 2nd or 3rd client is in active engagement.

3. **Codex publication strategy.** Ship 50 entries publicly first to seed authority and SEO traffic to `rushmediaagency.com/codex`, or wait for the full 132? The 50-first approach gets the marketing flywheel running sooner. The 132-first approach avoids a half-finished public artifact. Leaning toward 50-first based on marketing velocity priorities.

4. **SaaS tier pricing model (Phase 4).** Per-domain, per-finding, or flat retainer? Per-finding aligns price with value delivered but is hard to explain and hard to predict revenue against. Per-domain is predictable but penalizes large-site customers. Flat retainer is simplest. Decision deferred until the build is closer to Phase 4.

5. **Embedding model.** Voyage or OpenAI text-embedding-3-small? Voyage scored higher on retrieval benchmarks in 2025 evaluations. OpenAI is cheaper and more battle-tested. Decision deferred to build sprint — both are viable.

---

## Part 8 — What this doc is not

To prevent scope drift in future chats:

- **Not** the operating manual for running an audit. That's Path C-Narrow (`ygramul-path-c-narrow-operating-manual.md`).
- **Not** the agentic platform planning context for fundraise. That's Path B (`ygramul-path-b-handoff.md`).
- **Not** the lever framework deep-dive for audit execution. That's Doc 2 of the Ygramul Doc Set.
- **Not** the data input spec for audit deliverables. That's Doc 3.
- **Not** the API-first MVP architecture spec. That's Path A (pending).
- **Not** the n8n wrapper architecture. That's Path C-Broad (pending).

This doc is the **system reference** that all of the above inherit from. If a downstream doc contradicts this one, this one wins (unless `LEVERS.md` says otherwise).

---

## Downstream docs that inherit from this one

The handoff cascade flagged in `session-handoff-2026-04-27.md`:

1. **This doc** (`ygramul-codex-architecture.md`) — system reference. ✅ Updated to 11 levers.
2. **Doc 2** (`ygramul-doc-2-7-lever-framework-deep.md`) — needs full rewrite. Rename to `ygramul-doc-2-11-lever-framework-deep.md`.
3. **Doc 1** (`ygramul-doc-1-master-prompt.md`) — patch workflow Step 4 to "Apply 11 Levers." Add Levers 10/11 handling.
4. **Path B handoff** (`ygramul-path-b-handoff.md`) — patch lever count, agent inventory, dependency-order roadmap.
5. **Path C-Narrow** (`ygramul-path-c-narrow-operating-manual.md`) — patch Section 3.2 execution sequence, Section 4 QA references.

After the cascade, the four downstream docs all inherit cleanly from the 11-lever model. New docs (Doc 3 data spec, Doc 4 voice, Doc 5 runbook, Doc 6 codex catalog, Path A architecture, Path C-Broad n8n) should reference this doc as the system source.

---

## Quick reference for next-Claude

**If asked to run an audit:** Use `tech-seo-audit` skill + Path C-Narrow manual + this doc for system context.

**If asked to write a Jira ticket:** Use the P0/P1/P2/P3 framework. Format is documented in Doc 1 master prompt + Path C-Narrow.

**If asked about the agent architecture:** Reference Part 4 of this doc. Don't invent agent names — use the inventory above.

**If asked about the auto-research loop:** Reference Part 5 of this doc + Lever 11 in `LEVERS.md`.

**If a downstream doc contradicts this one:** This doc wins (unless `LEVERS.md` says otherwise).

**If `LEVERS.md` has updated since this doc was last touched:** `LEVERS.md` wins. Update this doc to match before doing anything else with it.

---

**End of architecture reference.**

Hand to: any new Claude chat doing Ygramul / Codex / RAG / agent architecture work. Skips ~30 minutes of context rebuild.
