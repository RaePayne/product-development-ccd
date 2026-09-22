> **Brand:** All
> **Last updated:** 2026-05-08
> **Owner:** Ruby Launder
> **Status:** Final

# Business Case — Template

This template defines the standard format for all business cases across this repo. Each initiative requiring investment consideration should have a business case in `strategy/` before it is added to the roadmap.

The format mirrors the Strategy Card used in executive roadmap reviews. Every section maps directly to a section on the Strategy Card.

---

## How to Use This Template

1. Copy this structure into a new file in `strategy/`
2. Name the file `business-case-[initiative-slug].md` (e.g., `business-case-expand-jim2-api.md`, `business-case-warehouse-mobile.md`)
3. Replace all `[placeholder]` text with initiative-specific content
4. Mark any sections that are not yet known as `[To be defined]` — do not delete sections
5. Set the **Overall Assessment** (Positive / Negative / Neutral) and the **Confidence** level for Dev Cost and Revenue based on current information
6. Update the metadata header (`Last updated`, `Status`) every time the file is edited

---

## Template

```markdown
> **Brand:** [Brand name]
> **Last updated:** [YYYY-MM-DD]
> **Owner:** [Name]
> **Status:** [Draft / In Review / Approved / Rejected]

# Business Case — [Initiative Name]

---

## Strategy & Objective

[What is this initiative and why are we considering it? 2–3 sentences. Include the primary strategic reason — e.g., attrition risk, new revenue, competitive gap, platform requirement.]

---

## Situation

[What do we have now and what is missing? Describe the current state, the gap, and the trigger event that makes this timely. 2–4 sentences.]

---

## Solution

[What is the proposed approach? Keep this high-level — this is not a spec. 2–3 sentences or a short bullet list. Reference any scope document or SDD if one exists.]

---

## Customer / Market

**Target customer:** [Who is this for — specific customer, segment, or both]

**Size of market / attrition at risk:** [ARR at risk, new ARR opportunity, or PS revenue potential]

**Key competitors / alternatives:** [What is the customer's alternative if we don't deliver]

---

## Market Validation

[What are customers or internal stakeholders telling us? How have they validated the need? Use bullet points. Each bullet should be a specific signal — a quote, a named customer action, a confirmed data point. Not generic claims.]

- [Specific validation signal — who said what, or what action confirmed demand]
- [Specific validation signal]
- [Specific validation signal]

---

## Strategic Alignment

[How does this align with Happen's strategy? What are the key value drivers beyond the immediate revenue? Use bullet points.]

- [Alignment point — e.g., reduces custom work debt, enables partner channel, unblocks roadmap item]
- [Alignment point]
- [Alignment point]

---

## Unfair Advantage

[What gives us an edge here that a competitor or alternative cannot easily replicate?]

- [Advantage — e.g., existing platform capability, customer relationship, cost asymmetry]
- [Advantage]
- [Advantage]

---

## Challenges / Risks

[What are the key risks to this initiative? Be specific — generic risk lists are not useful.]

- [Risk — include likelihood and impact where known]
- [Risk]
- [Risk]

---

## Development Effort / Cost

**Confidence:** [High / Somewhat confident / Low]

| Phase | Scope | Effort | Cost Estimate |
|---|---|---|---|
| Phase 1 | [What is included in Phase 1] | [Weeks / months, # resources] | [$X — based on $Y/hr × Z hrs] |
| Phase 2 | [What is included in Phase 2 — ongoing or follow-on] | [Estimate] | [Estimate or TBD] |

**Assumptions:** [Key assumptions the estimate relies on — e.g., "based on IF-01 and IF-02 only; full 7-flow scope not yet estimated"]

---

## Revenue Model & Forecast

**Confidence:** [High / Somewhat confident / Low]

| Revenue Type | Detail | 2025 / Current | 2026 Forecast |
|---|---|---|---|
| Attrition prevented (ARR) | [Customer and ARR at risk] | $[X] | $[X] |
| PS revenue | [Engagement scope and rate] | $[X] | $[X] |
| New ARR | [If applicable] | — | $[X] |
| Other | [API licence, recurring fees, etc.] | [TBD / $X] | [TBD / $X] |

---

## Key Success Metrics

[How will we know this has succeeded? Be specific — name the metric and the target value.]

- [Metric — e.g., "$150K ARR retained (Blue Connections IT)"]
- [Metric — e.g., "Phase 1+2 delivered by end Q3 2026"]
- [Metric — e.g., "PS revenue collected: $X"]
- [Metric — e.g., "API gap list reduced: X fields added to core"]

---

## Next Steps

[What needs to happen before a go/no-go decision can be made, and what happens after?]

- [Action — owner — due date]
- [Action — owner — due date]
- [Action — owner — due date]

---

## Overall Assessment

**Positive / Negative / Neutral**

[One paragraph. Summarise the investment logic: what makes this worth doing (or not), what the key condition is for proceeding, and what the risk of inaction is.]
```

---

## Section Guide

| Section | Required? | Notes |
|---|---|---|
| Strategy & Objective | Yes | Why this exists — the strategic trigger |
| Situation | Yes | Current state and the gap |
| Solution | Yes | High-level proposed approach |
| Customer / Market | Yes | Who this is for and the financial stake |
| Market Validation | Yes | Specific signals only — no generic claims |
| Strategic Alignment | Yes | Beyond immediate revenue |
| Unfair Advantage | Yes | What we have that others don't |
| Challenges / Risks | Yes | Specific risks, not a generic list |
| Development Effort / Cost | Yes | Phase breakdown with confidence level |
| Revenue Model & Forecast | Yes | Attrition prevention counts as revenue |
| Key Success Metrics | Yes | Named metrics with target values |
| Next Steps | Yes | Actions, owners, dates |
| Overall Assessment | Yes | Positive / Negative / Neutral with rationale |

---

## Naming Convention

`business-case-[initiative-slug].md` — examples:
- `business-case-expand-jim2-api.md`
- `business-case-warehouse-mobile.md`
- `business-case-pos.md`
- `business-case-bluecon-integration.md`
