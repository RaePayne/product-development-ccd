> **Brand:** All
> **Last updated:** 2026-03-13
> **Owner:** Matthew Sluggett
> **Status:** Final

# Strategy on a Page — Template

This template defines the standard format for all strategy documents across product-development repos. Each brand should have at least one product strategy on a page in its `strategy/` folder.

---

## How to Use This Template

1. Copy this structure into a new file in `strategy/`
2. Name the file `[brand]-[strategy-type]-strategy.md` (e.g., `impos-product-strategy.md`, `otd-product-strategy.md`, `impos-integration-strategy.md`)
3. Replace all `[placeholder]` text with brand-specific content
4. Keep it concise — this is a **strategy on a page**, not a strategy document. Every section should be scannable in under 60 seconds
5. Use the standard metadata header

---

## Template

```markdown
> **Brand:** [Brand name]
> **Last updated:** [YYYY-MM-DD]
> **Owner:** [Name]
> **Status:** [Draft / In Progress / Approved]

---

# [Brand] — [Strategy Type] Strategy

## Vision

[One sentence. Where are we going? This is the aspirational end state.]

## Mission

[One sentence. How do we get there? This is how we deliver on the vision day-to-day.]

---

## Where We Play

[1–2 paragraphs. Define the market, customer segment, and scope. Who do we serve? What problem space are we in? What is the current state of the business and product?]

## How We Win

| Pillar | What It Means |
|--------|---------------|
| **[Differentiator 1]** | [Why this gives us an edge — one line] |
| **[Differentiator 2]** | [Why this gives us an edge — one line] |
| **[Differentiator 3]** | [Why this gives us an edge — one line] |
| **[Differentiator 4]** | [Why this gives us an edge — one line] |

---

## Core Value Areas

[Define the key capabilities or value areas where customers get the most value and where investment will be concentrated. Use a table for scannability.]

| # | Value Area | What Customers Get | Strategic Direction |
|---|------------|--------------------|--------------------|
| 1 | **[Area name]** | [What the customer receives or experiences] | [Where this is heading — migration, automation, expansion, etc.] |
| 2 | **[Area name]** | [What the customer receives or experiences] | [Where this is heading] |
| 3 | **[Area name]** | [What the customer receives or experiences] | [Where this is heading] |

---

## Strategic Priorities

[List 3–5 priorities in order of importance. Each priority follows this format:]

### Priority 1 — [Priority Name]

**Problem:** [What's broken, missing, or constraining us today — 1–2 sentences]

**Target state:** [What good looks like when this is done — 1–2 sentences]

**Why it matters:** [Why this priority deserves investment now — connects back to vision, customers, or competitive pressure — 1–2 sentences]

### Priority 2 — [Priority Name]

**Problem:** [...]

**Target state:** [...]

**Why it matters:** [...]

### Priority 3 — [Priority Name]

**Problem:** [...]

**Target state:** [...]

**Why it matters:** [...]

---

## What We Will Not Do

[Bullet list of explicit strategic boundaries. What are we choosing NOT to pursue? This section prevents scope creep and keeps the strategy focused.]

- [Anti-goal 1 — what and why not]
- [Anti-goal 2 — what and why not]
- [Anti-goal 3 — what and why not]

---

## Measuring Success

| Metric | Why It Matters |
|--------|---------------|
| [Metric name] | [What this tells us about progress] |
| [Metric name] | [What this tells us about progress] |
| [Metric name] | [What this tells us about progress] |
| [Metric name] | [What this tells us about progress] |

---

## Supporting Reference

- [Link to SWOT analysis, brand docs, or other supporting material]
- [Link to related strategy docs]
```

---

## Section Guide

| Section | Required? | Notes |
|---------|-----------|-------|
| Vision | Yes | One sentence only |
| Mission | Yes | One sentence only |
| Where We Play | Yes | Sets the context — market, segment, current state |
| How We Win | Yes | Differentiators in table format for quick scanning |
| Core Value Areas | Optional | Use when the brand has distinct capability areas worth calling out |
| Strategic Priorities | Yes | 3–5 priorities, ordered. Each must have Problem / Target state / Why it matters |
| What We Will Not Do | Recommended | Explicit boundaries prevent scope creep |
| Measuring Success | Yes | Metrics that confirm the strategy is working |
| Supporting Reference | Optional | Links to SWOT, brand docs, related strategies |

---

## Naming Conventions

| Strategy Type | File Name Example |
|---------------|-------------------|
| Product strategy | `[brand]-product-strategy.md` |
| Integration strategy | `[brand]-integration-strategy.md` |
| Platform strategy | `[brand]-platform-strategy.md` |
| Growth strategy | `[brand]-growth-strategy.md` |
| Technology strategy | `[brand]-technology-strategy.md` |

---

## Tips

- **Be specific, not aspirational.** "Reduce manual matching hours by 50%" beats "Improve efficiency"
- **Priorities must be ordered.** If everything is a priority, nothing is
- **One page means one page.** If you can't scan it in 5 minutes, it's too long — move detail to supporting docs and link to them
- **"What We Will Not Do" is as important as what we will do.** This section prevents well-intentioned scope creep
- **Update the strategy when priorities change** — a stale strategy is worse than no strategy
