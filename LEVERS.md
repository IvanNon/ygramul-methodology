# The Ten Levers

The full Ygramul framework, lever by lever.

---

## How to read this document

This is the working reference for the ten levers Ygramul organizes its work around. Each lever covers a category of work that contributes to organic visibility on classical search and on AI-search surfaces. Each one has its own diagnostic signals and failure modes.

If you've read the [methodology overview](./README.md), the framing here will be familiar. This document goes one level deeper. It describes what each lever covers, why it sits where it sits, and what goes wrong when it's misapplied or skipped.

### How senior practitioners think about this

Senior technical SEOs don't usually carry ten levers in their head. They think in roughly four buckets: *can the bot find it, can the bot index it, will it rank, did it work?*

The ten levers are a more granular version of that same intuition:

- **Find and index** — Levers 1, 2, 3 (Crawl Architecture, Canonical Architecture, Page Technical Signals)
- **Rank** — Levers 4, 5, 6, 7, 8 (Keyword Strategy, Content, Programmatic, Internal Linking, Authority/Trust/GEO)
- **Measure and learn** — Levers 9 and 10 (Brand Demand, Auto-Research)

The granularity is the point. Senior practitioners can compress these ten back to four when they want to think fast. The ten exist so that audit findings have a clean home and so the work scales beyond what one person can hold in their head.

### Three lever groupings

Not all ten levers run on the same timescale or in the same way:

- **Engagement levers (1–8)** — sequenced work done during a client engagement. Run in order. Each unblocks the next.
- **Long-arc lever (9)** — brand and search demand work, which operates on multi-year timescales and runs in parallel to engagement work, not sequenced after it.
- **Cross-engagement lever (10)** — auto-research and outcome measurement. Operates across the full client base and feeds back to update the rules used in Levers 1–9.

The diagram is closer to a loop than a line. Engagement levers run sequenced through the work, brand demand runs in parallel on a longer clock, and auto-research observes everything and updates the framework's rules over time.

### Who this framework is for

Ygramul is calibrated for sites in the 100,000+ URL range with complex technical stacks — headless CMS, multilingual rollouts, programmatic content, active GEO and AI-search exposure. The typical buyer is a Director, VP, or Head of SEO at a $5M–$500M ARR company.

Smaller or simpler sites can run a subset of these levers without loss. A 500-page direct-to-consumer Shopify site does not need the same canonical architecture rigor as a 200,000-URL multilingual SaaS platform with locale prefix bugs and parameter pollution. The framework is granular by intent. It is not the right tool for every site.

### What Ygramul doesn't cover

Naming what's out of scope is more honest than implying everything is in scope. Ygramul does not cover:

- **ICP development and customer research.** Knowing who the buyer is and what they care about is a prerequisite to keyword strategy (Lever 4). Where ICP clarity doesn't exist, surfacing that gap is the first finding — but the work to develop it is brand strategy, not technical SEO.
- **Conversion rate optimization beyond surfacing friction.** Ygramul flags message-match issues and conversion path friction during content audits (Lever 5). It does not redesign funnels, run A/B tests on CTAs, or own conversion optimization as an ongoing workstream.
- **Public relations and demand-generation execution.** Ygramul measures branded search outcomes (Lever 9). It does not pitch journalists, run podcast outreach, or execute PR strategy.
- **Local SEO and Google Business Profile management.** Outside the typical ICP. NAP consistency is covered in Lever 8, but full local SEO work (review velocity, map pack ranking, GBP optimization) is a separate discipline.
- **Paid search and SEM.** Different practice entirely.
- **Lifecycle marketing — email, push, retention.** Different practice entirely.

The exclusions are deliberate. Doing one thing well is more valuable than doing five things adequately.

### Calibration on current state

This document describes the framework as designed. Some components operate today across active engagements. Others are partially built and being instrumented. Where a lever's chapter describes capabilities still being developed — particularly Lever 10's auto-research loop — the chapter says so plainly.

Ygramul is a working framework that is designed to learn from each engagement. It is not a finished product. The published Claude Skills (Schema Detector, AIO Cascade) are the open-source surface; the proprietary surface is improving with use.

### Where this sits relative to other published work

Ygramul is published in dialogue with adjacent technical SEO and GEO frameworks. Mike King's writing at iPullRank covers the technical SEO landscape with depth. Aleyda Solis publishes process-oriented diagnostic frameworks. The SEJ and SMX communities have been documenting the field for two decades. None of these prescribe a sequenced lever framework with auto-research as the primary differentiator. That gap is where Ygramul sits.

---

## Lever 1 — Crawl Architecture

The site-level work that determines how a search engine's crawler navigates the site as a whole. Lever 1 is concerned with what gets crawled, how often, and whether crawl budget is spent on URLs that matter or wasted on URLs that don't.

### What success looks like

The crawler reaches every URL that should be indexed, on a cadence appropriate to that URL's update frequency, without wasting crawl budget on parameter variants, infinite spaces, or phantom URLs generated by JavaScript framework artifacts. Server logs show a crawl distribution that matches the site's actual content priority. The indexation rate — valid URLs that are actually indexed, divided by valid URLs that should be — is high and stable.

### Signal categories

- robots.txt directives and parameter handling rules
- XML sitemap coverage versus crawled URL coverage
- Crawl frequency by URL pattern (server log analysis)
- Phantom URL generation patterns (JS framework prefetch, parameter pollution, faceted navigation)
- Crawl path efficiency (depth from homepage, internal link discoverability)
- Indexation rate trend (Google Search Console Page Indexing report)
- Crawl budget allocation between commercial pages, navigational pages, and waste

### Why this lever sits at position 1

Everything downstream depends on the crawler reaching the right URLs at the right cadence. If Lever 1 is broken, the most important page on the site might not be indexed. The cleanest schema is never parsed. The most polished content is ignored. Optimization at any other lever assumes this one is solved. When Lever 1 is broken, work at Levers 2 through 9 is wasted budget.

### Pattern observed in practice

On one engagement, a Next.js App Router prefetch behavior was generating 195,000 phantom URLs against 1,500 real pages — a 130x multiplier. Crawl budget had been silently consumed for months. The standard crawl tools showed only the canonical URLs; the phantom surface was visible only in server logs and in the GSC "Crawled — currently not indexed" bucket. A three-layer fix (robots.txt parameter blocking, canonical hardening, internal link suppression for prefetch routes) reduced phantom URLs by 71% in the first month. This is the kind of finding that's invisible in a check-the-robots-txt audit and obvious in a server-log audit.

### Common failure modes

- **robots.txt treated as a binary.** Auditors check whether it exists. They don't audit whether the parameter handling rules have evolved with the site's URL surface. New framework features ship; crawl waste accumulates silently.
- **Sitemap segmentation missing.** A single 50,000-URL sitemap obscures coverage gaps. Segmented sitemaps — by URL pattern, section, or template — surface gaps immediately.
- **Phantom URLs dismissed as minor.** Parameter pollution and prefetch artifacts can multiply the URL surface 100x. The cost is invisible in standard crawl tools and only appears in log analysis or in the GSC "Crawled — currently not indexed" bucket.
- **Server logs never analyzed.** Crawl behavior is inferred from third-party tools rather than read directly from where the crawler actually visited. Diagnoses based on inferred behavior miss the real waste.

---

## Lever 2 — Canonical Architecture

The decisions about which URL patterns are authoritative for which content, and how those decisions are signaled to search engines. Lever 2 covers both the strategic layer (what the canonical URL structure should be) and the implementation layer (canonical tags expressing that structure on each page).

### What success looks like

Every page has exactly one canonical URL. That URL is the one that should rank. The canonical signal is consistent across canonical tags, internal links, sitemaps, hreflang annotations, and structured data. Locale variants resolve cleanly. Pagination canonicalizes to the right targets — typically self-canonical, not to page 1. Filter and sort URL variants either canonicalize to the parent category or are blocked from indexation entirely. Duplicate content patterns are caught before they reach production.

### Signal categories

- Canonical tag presence and accuracy across templates
- Locale prefix handling (`/en/`, `/fr/`, etc.) and double-locale bugs
- Pagination canonical strategy (self-canonical versus rel=canonical to page 1)
- Filter and sort URL canonical handling
- Cross-domain canonical signals (where applicable)
- Canonical-versus-internal-link consistency (the canonical points to URL X but internal links point to URL Y)
- hreflang and canonical alignment

### Why this lever sits at position 2

Canonical decisions are upstream of every other on-page signal. The canonical tag, the redirect strategy, the schema markup, the internal link target — all implement decisions that were made (or should have been made) at the canonical architecture level. If the architecture is wrong, downstream signals contradict each other. Search engines either pick a target you didn't intend or split signals across multiple URLs and rank none of them well.

This is also why Lever 2 sits before Lever 3 (Page Technical Signals). The per-page implementation in Lever 3 cannot precede the architecture decisions in Lever 2.

### Pattern observed in practice

Framework defaults produce canonical bugs that are invisible in single-page audits and obvious at scale. On one site, locale-aware canonical generation was producing `/en/en/products` style double-prefix canonicals on a subset of pages — affecting maybe 5% of the URL surface, but those 5% were among the most commercially valuable pages. The bug was generated by the framework's interaction with a custom routing rule. Fixing the routing rule resolved the canonical issue and recovered indexation on several hundred high-value URLs. The pattern: framework canonical generation shipped by competent frontend developers using sensible defaults is frequently wrong at scale.

### Cross-lever interaction

Canonical bugs almost always interact with Lever 1 (Crawl Architecture). When the crawler discovers a phantom variant of a canonical URL, the canonical tag is the signal that prevents indexation drift. When canonicals are wrong, crawl waste compounds because the crawler keeps revisiting variants. The standard pattern: fix canonicals first (Lever 2), then validate crawl recovery (Lever 1).

### Common failure modes

- **Framework canonical defaults shipped without audit.** Next.js, headless CMS systems, and locale-aware frameworks ship canonical generation that breaks in subtle ways at scale. The bug is invisible until the site is crawled at scale.
- **Pagination canonicalizing to page 1.** A common pattern in older SEO advice that Google has explicitly walked back. Pages 2, 3, 4 should be self-canonical or use proper pagination markup, not collapse to page 1.
- **Filter/sort URLs treated inconsistently.** Some filters get canonicalized; some don't; some are blocked in robots.txt; some are noindexed. Without a documented strategy, every team makes a different decision.
- **Canonical decisions made by developers without SEO input.** The canonical tag is a one-line piece of HTML, but the decision behind it is strategic. When that decision is made by a frontend developer choosing a sensible default, it's frequently wrong.

---

## Lever 3 — Page Technical Signals

The page-level technical signals the crawler evaluates each time it reaches a URL. Lever 3 is concerned with whether the page itself sends the right signals to be indexed, ranked, and understood — separate from the site-level decisions in Levers 1 and 2.

### What success looks like

Every page returns the right HTTP status code. Renders consistently in raw HTML and rendered DOM. Loads quickly enough that its quality is evaluable. Declares its language correctly. Marks up its entities and content type with valid schema. Is mobile-friendly without a separate mobile experience. Indexability directives — noindex, X-Robots-Tag — are deliberate and audited.

### Signal categories

- HTTP status code distribution (2xx, 3xx, 4xx, 5xx ratios across the site)
- Redirect chain depth and 307/302/301 patterns at the per-URL level
- hreflang annotations and reciprocal alignment
- Schema and structured data (JSON-LD validity, completeness, type coverage)
- Core Web Vitals (LCP, INP, CLS) measured through field data and lab data
- JavaScript rendering parity (rendered DOM matches raw HTML for critical content)
- Mobile rendering and responsive design signals
- HTML structure (heading hierarchy, semantic markup, meta tags)
- Indexability directives (noindex, X-Robots-Tag, meta robots)

### Why this lever sits at position 3

This lever implements the architecture decisions from Lever 2 at the page level. The canonical strategy from Lever 2 expresses itself here as canonical tags on every page. The locale strategy expresses itself as hreflang annotations. Lever 3 is also where most of the work covered by traditional "technical SEO audits" actually lives. It sits at position 3 because if Levers 1 and 2 are broken, fixing Lever 3 signals is rearranging deck chairs.

### Pattern observed in practice

JavaScript rendering parity gaps are the most common Lever 3 issue and the easiest to miss. On one engagement, the default crawl reported "no titles detected" on 7 of the top 30 pages. The titles were present in browser. They were being added to the DOM after the initial HTML response by a client-side framework. A re-crawl with JavaScript rendering enabled showed the titles correctly. The site looked fine in browser; it was being indexed without titles for months. The pattern: JS-rendered critical content is invisible to default crawls and to many audit workflows. The fix isn't on the page — it's in the audit methodology.

### Common failure modes

- **JS rendering parity gaps go undetected.** Critical content (titles, schema, internal links) is added to the DOM after the initial HTML response. Default crawls miss this. Only crawls with JavaScript rendering enabled and properly configured catch the gap.
- **Core Web Vitals treated as a Lighthouse score instead of a field-data signal.** Lab data and field data often disagree. Optimizing for the lab score while field data degrades is common.
- **Schema implemented inconsistently across templates.** Article schema on some posts, none on others. Product schema with missing required fields. Person schema for authors but no `sameAs` to their LinkedIn or external profiles. Inconsistent implementation is treated as no implementation by validators.
- **Redirect chains accumulate over years.** A 2018 URL redirects to a 2020 URL redirects to a 2023 URL. Each hop costs crawl efficiency and dilutes link equity. Chains of 4+ hops are common on sites that have gone through multiple migrations without redirect map maintenance.

---

## Lever 4 — Keyword Strategy & Opportunity Modeling

The work of identifying which keywords matter, why they matter, and how their pursuit should be sequenced. Lever 4 translates ICP clarity into a keyword universe, scores that universe by commercial value and competitive feasibility, and produces a roadmap that other levers execute against.

### What success looks like

The keyword universe is documented and segmented by intent (informational, commercial, transactional, navigational, brand) and by funnel stage. Every keyword carries a commercial value score and a feasibility score. An explicit opportunity ranking exists. A quarter-by-quarter roadmap is produced and revisited monthly as performance data lands and as the keyword landscape shifts.

### Signal categories

- Keyword universe coverage (categories of intent represented and missing)
- Keyword opportunity scoring (commercial value × feasibility)
- Search volume trends and seasonal patterns
- SERP feature presence per query (AI Overviews, featured snippets, video, local pack)
- Competitive density (how many sites are credibly targeting each query)
- Keyword cannibalization (multiple URLs targeting the same query)
- Branded versus non-branded query share

### Why this lever sits at position 4

By this point in the sequence, the technical foundation (Levers 1–3) is solid enough that ranking signals can land. Now the question becomes: rank for what? Lever 4 produces the roadmap that drives Lever 5 (content) and Lever 6 (programmatic). Without Lever 4, content production is uncoordinated — pages get written based on what individual writers find interesting, not based on what would compound the site's organic visibility.

**ICP clarity is a prerequisite.** Keyword opportunity scoring depends on knowing what the ideal customer cares about. Where ICP isn't documented, surfacing that gap is the first finding from this lever. The work to develop ICP itself is brand strategy, not Ygramul scope.

### Common failure modes

- **Keyword universe scoped only to high-volume head terms.** The body and the long tail — where actual commercial activity often lives, and where AI-search query patterns are emerging — gets ignored.
- **Search volume treated as commercial value.** A 50,000-volume informational query is not more valuable than a 500-volume bottom-funnel query. Scoring that ignores intent and funnel stage produces roadmaps that don't move the business.
- **Roadmap built once and never revisited.** The keyword landscape changes monthly. AI Overviews appear and disappear. A quarterly-static roadmap is stale within six weeks.
- **Cannibalization goes uncaught.** Three URLs target the same query. None ranks well. The pattern was never identified at the keyword strategy level.

---

## Lever 5 — Content Production & Optimization

The work of producing content against the Lever 4 roadmap and maintaining that content as it ages. Lever 5 covers content briefs, drafting standards, on-page optimization, content decay analysis, and the surfacing of message-match and conversion-path issues.

### What success looks like

Content shipped against the roadmap ranks for its target queries. Holds rank against incumbents. Refreshes on a cadence appropriate to its content type. Briefs are detailed enough that drafting produces consistent quality regardless of who writes. Content decay is monitored — pages losing position over time get caught and refreshed before they drop out of the top 10. Where pages succeed at attracting traffic but fail at converting it, that gap is surfaced.

### Signal categories

- Content brief depth and ranking outcome by brief
- Content decay velocity (rate of position loss over time per URL)
- On-page optimization completeness (title, meta, H-tags, internal links, schema match)
- Topical depth versus thin-content patterns
- Message-match between query intent and page promise
- Conversion-path friction signals (high-traffic, low-engagement pages)
- Content freshness signals (lastModified, dateModified, content updates)

### Why this lever sits at position 5

Content is what Levers 1–4 enable to rank. The technical foundation makes it findable. The canonical architecture makes it indexable. The keyword strategy makes it deliberate. Without those upstream levers solved, content work doesn't compound.

### Common failure modes

- **Briefs too thin to produce consistent output.** Writers fill in gaps from their own intuition. Quality varies wildly by writer. Documented brief standards are high-leverage work that's rarely prioritized.
- **Content decay treated as a content problem when it's often a SERP feature problem.** A page lost rank not because it got worse but because Google added an AI Overview that captures the click. Refreshing the page doesn't fix this. Understanding the new SERP shape does.
- **Optimization stops at the title tag.** Modern on-page work includes schema, internal link integration, content-section structure, entity coverage, and AI-search opener blocks. A check-the-title-and-meta workflow is incomplete.
- **Conversion friction ignored or treated as a CRO problem in isolation.** A page that ranks but doesn't convert is sometimes a content problem — the page promised something the user didn't get. Surfacing this gap is Lever 5 work; closing it is CRO and lives outside Ygramul.

---

## Lever 6 — Programmatic SEO

The work of identifying repeatable content patterns that warrant production at scale, building templates that produce quality output at that scale, and managing the technical and editorial integrity of the resulting page surface. Lever 6 covers location pages, comparison pages, glossary pages, integration pages, and any other template-based production where the value is in the *coverage* across instances.

### What success looks like

Programmatic page surfaces grow the site's keyword coverage in commercially valuable ways without degrading the site's overall quality signal. Each programmatic page is differentiated enough to avoid being treated as duplicate content. Templates produce content that's genuinely useful, not just keyword-stuffed scaffolding. The programmatic surface integrates cleanly with the rest of the site's information architecture (Lever 7) and respects the canonical strategy (Lever 2).

### Signal categories

- Template pattern identification (which patterns warrant programmatic production)
- Per-instance differentiation (does each generated page have unique value?)
- Programmatic content coverage versus query-pattern coverage gaps
- Quality-signal monitoring (does the programmatic surface degrade the site's overall ranking power?)
- Template performance drift (do early instances rank? do later instances rank? what changed?)
- Canonical and indexation behavior on programmatic surfaces

### Why this lever sits at position 6

Programmatic SEO depends heavily on upstream levers. The canonical architecture (Lever 2) must handle template-driven URL patterns. The keyword strategy (Lever 4) must identify the patterns worth productizing. The content standards (Lever 5) must be encoded into the template. Run programmatically without those dependencies solved, and a single bad template multiplies quality issues across thousands of pages.

This is also why Programmatic SEO is its own lever rather than a sub-concern of Lever 5. Designing a template, validating it on a small batch, and then scaling production has a different character than producing individual pieces of content.

### Common failure modes

- **Templates produce thin content at scale.** A "best [X] in [Y]" template that's 40% boilerplate, 30% repurposed product data, and 30% AI-generated filler ranks for nothing. Scaling at the cost of per-instance quality is the most common failure pattern.
- **Programmatic surface bypasses Lever 2.** Templates ship with default canonicals pointing at themselves, ignoring the canonical strategy. Faceted programmatic pages create thousands of near-duplicate URLs.
- **Quality drift goes unmonitored.** Template instances 1–500 rank well; instances 501–5,000 don't. Without per-instance ranking monitoring, the drift is invisible until total traffic drops.
- **Programmatic without content-quality investment.** The fundamental insight of programmatic SEO is that template + data = content at scale. Skipping the content-quality investment in the template makes the data fill emptiness instead of value.

---

## Lever 7 — Internal Link Architecture

The work of designing how the site's pages link to each other — both for crawler distribution and for the flow of authority through the site graph. Lever 7 covers internal link discoverability, anchor text patterns, hub-and-spoke topology, and the resolution of orphan pages.

### What success looks like

Every commercially valuable page is reachable from the homepage in three or fewer clicks. Every page links to topically related peers. Those links use anchor text that describes the destination accurately. Hub pages aggregate authority and distribute it to the cluster pages they govern. Orphan pages — pages that no internal link points to — don't exist on commercially valuable URL patterns. The internal link graph is intentional, not accidental.

### Signal categories

- Click depth from homepage per URL
- Orphan page detection by template
- Anchor text distribution and diversity by destination URL
- Hub-and-spoke topology consistency (do hub pages actually link to all their spokes?)
- Inbound internal link count per URL (a proxy for site-internal authority)
- Cross-template linking patterns (does the blog link to product pages? does the documentation link to feature pages?)
- Anchor text relevance to destination content

### Why this lever sits at position 7

By this point, the content asset library exists. The keyword strategy (Lever 4) has identified the destinations that matter. The content production work (Lever 5) and programmatic work (Lever 6) have produced the pages. Internal linking is the layer that connects all of this into a coherent site graph. It can only operate on what exists. Building the link graph before the content asset library exists is wasted effort because the graph keeps having to reroute as new pages ship.

### Common failure modes

- **Internal linking treated as a navigation problem instead of an authority distribution problem.** The header navigation links to the same five pages from every URL. The body of every page links to nothing else internal. Authority concentrates in the navigation targets and starves everything else.
- **Anchor text generic and uninformative.** "Click here," "learn more," "read our blog" — anchor text that doesn't describe the destination tells the crawler nothing about topical relevance.
- **Orphan pages on programmatic surfaces.** Templates ship without integration into the site graph. The resulting pages have no internal links pointing at them. They might be in the sitemap, but they're isolated.
- **Hub pages exist but don't actually link to all their cluster pages.** The hub is supposed to aggregate authority and distribute it. When it links to only the most prominent six cluster pages and ignores the next forty, the long tail of the cluster never benefits from the hub's authority.

---

## Lever 8 — Authority, Trust & GEO Visibility

The work of building the site's recognition by external systems — both classical search authority signals and AI-search citation behavior. Lever 8 covers entity infrastructure, organizational legitimacy markers, author credibility (E-E-A-T), inbound link quality, and visibility in AI-search surfaces (Google AI Overviews, Perplexity, ChatGPT search, Gemini).

### What success looks like

The site is recognized as the authoritative source for its topic area, by both classical search engines and AI-search systems. Author entities are properly defined, with `sameAs` links to external profiles and verifiable credentials surfaced in schema. Organizational legitimacy is established — clear About content, contact transparency, NAP consistency where applicable, security signals appropriate to the YMYL exposure of the content. The site is cited by AI Overviews and large language models for queries in its topic area, not just blue-link-ranked. Inbound links are earned from credible sources rather than bought from low-quality networks.

### Signal categories

- Author entity infrastructure (Person schema, `sameAs` links, credential surfacing)
- Organizational entity infrastructure (Organization schema, contact info, About page depth)
- E-E-A-T signals (experience, expertise, authoritativeness, trustworthiness — particularly for YMYL content)
- NAP (name, address, phone) consistency across the web
- Inbound link quality and topical relevance
- AI-search citation rate by query (how often the site is cited by AI Overviews, Perplexity, and others for queries in its topic area)
- Citation context (is the site cited as primary source, supporting reference, or competitor?)
- Brand mention sentiment and frequency in primary sources

### Why this lever sits at position 8

Authority is downstream of content. You can't be cited as authoritative on a topic if you don't have content on that topic. By position 8, the site has the technical foundation (Levers 1–3), the canonical strategy (Lever 2), the keyword roadmap (Lever 4), the content asset library (Levers 5–6), and the internal link graph (Lever 7). All of those are necessary substrates for authority to land. Authority work that precedes this substrate is unanchored — citations point at thin pages and ranking gains don't compound.

### Pattern observed in practice

E-E-A-T infrastructure work compounds slowly but reliably. On one engagement focused on a subject-matter expert with deep external credentials but minimal on-site author infrastructure, the work involved: building a dedicated author hub page, implementing Person schema with `sameAs` to verified external profiles (LinkedIn, Wikipedia, professional associations), surfacing credentials in author bylines on every article, and connecting external citations back through the author entity rather than the publication entity. Within 90 days, AI Overview citations appeared on queries in the expert's topic area where none had existed previously. The pattern: AI-search citation often follows entity-graph clarity more than it follows content quality alone.

### Common failure modes

- **E-E-A-T treated as a checkbox instead of as entity infrastructure.** Adding an author byline isn't E-E-A-T. Building author entities — Person schema, verifiable credentials, `sameAs` links to external profiles, individual author pages with topical authority — is. The shortcut version produces no signal.
- **AI-search citation work treated as separate from classical authority work.** It isn't. The same primary-source signals that make a site rank well for blue links also make it citable by AI-search systems. Treating GEO as a separate workstream produces duplicated effort and contradictory signals.
- **Inbound link work treated as the whole of authority.** Backlink campaigns, especially from low-quality networks, produce poor signal at best and penalties at worst. Authority is a portfolio: links matter, but so do brand mentions, primary-source citations, schema-encoded entity relationships, and content that earns linking organically.
- **Organizational entity infrastructure ignored.** Service businesses neglect their own About pages, contact pages, NAP consistency, and Organization schema. The site is treated as a marketing surface rather than as an entity in a knowledge graph. The knowledge graph treats it accordingly.

---

## Lever 9 — Brand & Search Demand Generation

The long-arc work of growing demand for the brand itself — branded search volume, share of voice for category terms, brand mention frequency, and the demand-side keyword universe that feeds future ranking opportunities. Lever 9 operates on multi-year timescales and runs in parallel to engagement work, not sequenced after it.

### What success looks like

Branded search volume grows over time, faster than the category's overall growth. The brand owns share of voice for category-defining terms even when not directly ranking for those terms (because users search for the brand first). The demand-side keyword universe — questions, problems, jargon used by the ICP — grows the addressable surface for future content work. The brand is cited and mentioned in primary sources, podcasts, conferences, and adjacent industry coverage.

### Signal categories

- Branded search volume trend
- Branded versus non-branded query share
- Share of voice for category-defining terms
- Brand mention frequency in primary sources
- Demand-side keyword universe expansion (new questions, new jargon, new problem framings entering the search landscape)
- Direct and referral traffic share
- Brand authority signals (Wikipedia presence, knowledge panel completeness, Google entity recognition)

### Why this lever sits in the long-arc grouping

Brand demand generation does not respond to single-engagement work on the timescales engagement levers operate on. Lever 1's crawl waste fixes can show indexation recovery in 30 days. Lever 4's keyword strategy work can show ranking shifts in 90 days. Brand demand growth compounds over 12 to 36 months and depends as much on the quality of all the upstream levers as on dedicated brand work itself.

This is why Lever 9 sits in parallel rather than sequenced last. Effective engagements start brand demand measurement on day one, not at month 12. The work compounds quietly while engagement levers do their faster-feedback work.

### Common failure modes

- **Branded search treated as a vanity metric instead of a leading indicator.** Branded search volume is one of the strongest leading indicators for organic traffic durability. A site growing branded search is more defensible against algorithm shifts than a site relying on non-branded traffic alone.
- **Brand work treated as out of scope for SEO methodology.** PR, podcast outreach, and conference speaking are not classical SEO disciplines. Their downstream effects on branded search and category authority are measurable in SEO metrics. Surfacing where these effects are happening — and where they aren't — is appropriate Ygramul work even when the execution is handled outside.
- **Confusing brand demand with brand awareness.** Brand awareness can grow without producing branded search volume. Brand *demand* is specifically the signal of users actively seeking the brand.
- **Neglecting the demand-side keyword universe.** New jargon and new problem framings enter the search landscape continuously. Sites that listen for these build their content roadmaps against next quarter's demand. Sites that don't, build against last quarter's.

---

## Lever 10 — Auto-Research & Outcome Measurement

The cross-engagement work of measuring what shipped, scoring its outcomes, and feeding the resulting patterns back to update the rules used in Levers 1 through 9. Lever 10 is the framework's learning loop. It operates continuously across the full client base and is what allows Ygramul to sharpen with use rather than going stale.

### Calibration on current state

The auto-research loop is *designed and partially operational*. Outcome measurement on individual findings happens today across active engagements. The cross-engagement pattern recognition layer — where findings from one engagement inform recommendations on another — is being instrumented, not yet running at full scale.

The framework is honest about this. Ygramul is a working framework that is *designed to learn*. It is not yet a system that has learned across hundreds of engagements. That state is the goal. It is not the current reality.

### What success looks like

Every recommendation produced by Levers 1–9 is tied to a measurable hypothesis. Outcomes are tracked at consistent cadences (typically 30, 60, and 90 days post-implementation). Findings that consistently predict outcomes get reinforced in the methodology's rules. Findings that consistently fail to predict outcomes get demoted or removed. The version of Ygramul applied to a new engagement is more accurate than the version applied to one a year ago, because cumulative measurement has updated the framework's priors.

### Signal categories

- Per-finding hypothesis tracking (what was predicted to move?)
- Outcome scoring (Win, Neutral, Regression — based on impressions, CTR, position, conversion proxies)
- Pattern recognition across engagements (which finding categories predict outcomes most reliably?)
- Rule update cadence (how often do framework priors shift?)
- Cross-vertical pattern detection (do findings that work in SaaS also work in publishing? in commerce? where do they not?)
- Calibration drift (are the framework's predictions becoming more or less accurate over time?)

### Why this lever sits as the cross-engagement layer

Lever 10 is recursive. Its outputs update the rules used by Levers 1 through 9 in subsequent engagements. This isn't a sequential position. It's a feedback layer that observes everything else and modifies the framework over time.

This is the lever the README points at when it says Ygramul is *designed to learn from each engagement so the rules sharpen with use rather than going stale*. It is what differentiates a methodology from a checklist. A checklist runs the same way regardless of outcome history. A methodology with auto-research updates its own rules as evidence accumulates.

### Pattern the loop is designed to produce

A recommendation category — for example, "add Person schema for content authors" — generates findings across multiple engagements. Outcomes get measured 30/60/90 days after implementation. After enough measured outcomes, a pattern emerges: the recommendation produces strong AI-search citation lift on engagements where the author has existing external authority signals (verified LinkedIn, external publications, professional associations) and minimal lift on engagements where the author is anonymous or has no external footprint. The methodology updates: Person schema additions get flagged as high-confidence when external authority signals are present, low-confidence when they aren't. The next engagement runs on the updated rule.

This is the loop in operation. It produces conditional rules rather than universal ones. It updates priors based on measured outcomes rather than on consensus opinion.

### Common failure modes

- **Recommendations shipped without measurable hypotheses.** A finding says "fix this" without specifying what should move. When the fix ships, there's no way to score the outcome. No scoring, no learning, no rule update.
- **Outcome measurement on too short a horizon.** A 7-day check on a fix that compounds over 90 days underrates slow-acting work and overrates fast-acting work. Auto-research that doesn't respect realistic feedback timescales produces biased rules.
- **Pattern recognition overfit to recency.** The latest 10 outcomes get weighted more heavily than the prior 100. A single bad month in algorithm noise causes the framework to discard rules that were working. Discounting must be deliberate, not implicit.
- **Auto-research treated as a backend process invisible to engagements.** When the framework updates its rules but those updates aren't surfaced to engagement work, the learning is lost. Auto-research is most valuable when its outputs land back in active audits as updated priors and revised severity weightings.

---

## How findings move through the framework

Most real findings cross levers. A canonical loop on a programmatic page is both a Lever 2 (Canonical Architecture) issue and a Lever 6 (Programmatic SEO) issue. A schema gap on author pages is both a Lever 3 (Page Technical Signals) issue and a Lever 8 (Authority, Trust & GEO Visibility) issue.

When a finding crosses levers, name both. Sequence the fix by dependency order: *"Issue at Lever X compounds with issue at Lever Y. Fix Y first, then validate X recovery."* The dependency order resolves the sequencing question — fix the upstream lever first, then check whether the downstream issue persists.

This is not a flaw in the framework. It's how SEO work actually works at scale. Document the cross-lever finding explicitly so that ambiguous findings get tagged on both seats rather than forced into one.

---

## What ships next

This document describes the framework as it stands today. It will change as the auto-research loop runs across more engagements and surfaces patterns that update the rules. That's the design.

The published Claude Skills implement narrow slices of this framework:

- **[Schema Detector](https://github.com/IvanNon/schema-detector-skill)** — addresses Lever 3 (Page Technical Signals) at single-URL granularity, with structured-data audit logic
- **[Ygramul AIO Cascade](https://github.com/IvanNon/ygramul-aio-cascade)** — addresses Lever 5 (Content Production & Optimization) for AI-search opener blocks, using a 14-judge editorial cascade

The proprietary surface — the agents used in active engagements — implements broader workflows across multiple levers in sequence. Those agents are documented for clients but not made public. The value is in the integrated system, not in any individual agent's prompts.

---

> All views shared here are my own personal work. This repository does not represent the views, strategies, or official work product of any current employer or client.
