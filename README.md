# Ygramul Methodology

A working framework for technical SEO and GEO (Generative Engine Optimization) — organized around seven levers, grounded in a primary-source Codex, and designed to learn from each engagement so the rules sharpen with use rather than going stale.

---

## The name

Ygramul takes its name from the spider in Michael Ende's *The Neverending Story* — a nod to the fact that search crawlers are, themselves, spiders.

Built by [Ivan Nonveiller](https://www.linkedin.com/in/ivannonveiller/) — enterprise SEO/GEO strategist.

---

## What it contains

Ygramul is a personalized data-driven framework that's designed to learn which optimizations actually move the needle for a specific site. Every recommendation generates a hypothesis, every hypothesis gets tested against measured outcomes, and every test updates the rules that drive the next round of audits.

- **Seven levers** — sequenced categories of work covering crawl, canonical, keyword strategy, content, programmatic, authority/GEO, and analytics
- **A primary-source Codex** — curated reference library of leaks, patents, papers, and antitrust testimony, used as a RAG layer for every audit
- **An auto-research loop** — four-step cycle (baseline → implementation → evaluation → update) that's designed to refine the rules from each engagement
- **A specialized agent layer** — focused agents for triage, execution, measurement, keyword research, content briefs, and content optimization
- **Two open-source skills** — Schema Detector and AIO Cascade, the public surface of the agent layer
- **A proprietary playbook layer** — implementation guides, prompts, and rejection-criteria framework, available only through engagements

It is the methodology used at [Rush Media Agency](https://rushmediaagency.com) for enterprise SEO and GEO work.

---

## Why this instead of a checklist audit

Most SEO audits are one-time deliverables. A senior consultant runs the crawl, surfaces a hundred findings, prioritizes them, hands over the report, and walks away. Twelve months later, another audit surfaces most of the same findings. The work repeats faster than it gets fixed.

Ygramul is structured as a system instead of a deliverable. Findings are tied to hypotheses, hypotheses get tested against measured outcomes, and outcomes update the rules that drive the next round. The version of the methodology applied to a new client should be more accurate than the version applied to one a year ago, because every engagement contributes to refining what the framework knows.

This is what makes it AI-native rather than AI-assisted. Without AI, the loop would be theoretical. With AI, it becomes operationally realistic.

---

## The seven levers

Each lever is a category of work that contributes to organic visibility, with its own diagnostic signals, decision criteria, and measurement model.

The levers are sequenced. Optimizing for AI citation before fixing crawl waste is wasted effort, because the citation signals can't reach pages the crawler isn't indexing reliably. Running programmatic SEO before fixing canonical architecture multiplies the problem rather than solving it. The order matters.

The seventh lever — performance analytics and auto-research — is what makes the framework different from a checklist. Findings from the first six don't just produce tickets. They produce hypotheses, and the hypotheses are designed to be tested against measured outcomes so the rules can be updated.

---

## The Codex

Underneath the levers sits the Codex, a curated library of primary sources that grounds the recommendations Ygramul produces.

Most SEO advice circulates as inherited wisdom. *Google likes X* gets repeated for years without anyone being able to point at why. The Codex is the discipline of insisting that recommendations have citations — a leaked document, a patent, a peer-reviewed paper, a piece of antitrust testimony, a Search Central page. When a finding says *missing dateModified weakens freshness signals*, the Codex tells you which source supports that claim and how strong the evidence is.

The Codex is implemented as a vector database used as a RAG layer for audits, briefs, and recommendations. The architecture is published. The source list is not.

---

## The agent layer

Ygramul is operated through specialized agents — each focused on a single lever or workflow, each grounded in the Codex.

The published Claude Skills are the open-source surface:

- **[Schema Detector](https://github.com/IvanNon/schema-detector-skill)** — single-URL structured data audit, Lever 6 entity-anchor work
- **[Ygramul AIO Cascade](https://github.com/IvanNon/ygramul-aio-cascade)** — Lever 4 AI Overview opener block generation through 14 specialized editor-judges

The proprietary surface — used in active engagements but not published — includes agents for technical SEO triage, execution planning, measurement, keyword opportunity modeling, content brief generation, and content optimization. These are documented for clients but not made public, because the value is in the integrated system, not in any individual agent's prompts.

---

## What this repository documents

This repo is the canonical source for the Ygramul methodology — the philosophy, the seven levers, the relationship between human judgment and AI execution. It does not contain the implementation playbooks, the agent prompts, or the rejection-criteria framework that paying clients receive.

If you're a senior SEO or GEO practitioner, the chapters that follow this README are where the substance lives. If you're trying to recreate Ygramul from this repo alone, you'll get the architecture but not the engine.

---

## Contributing

If you've worked on something at this intersection — technical SEO, GEO, AI search — and have notes, pushback, or evidence that contradicts something written here, I'd want to hear it. Open an issue first for anything bigger than a typo fix.

---

## License

MIT. Use it, adapt it, cite it. Attribution appreciated.

---

## About the author

**Ivan Nonveiller** — enterprise technical SEO and GEO strategist. 10+ years optimizing search for brands including Walmart, AutoTRADER, Ferrari, Maserati, Ritz-Carlton, Sotheby's, and BetterSleep. Based in Montréal.

- LinkedIn: [ivannonveiller](https://www.linkedin.com/in/ivannonveiller/)
- Agency: [rushmediaagency.com](https://rushmediaagency.com)
- Companion skills: [Ygramul AIO Cascade](https://github.com/IvanNon/ygramul-aio-cascade) · [Schema Detector](https://github.com/IvanNon/schema-detector-skill)

---

> All views shared here are my own personal work. This repository does not represent the views, strategies, or official work product of any current employer or client.
