> **Last updated:** [YYYY-MM-DD]
> **Owner:** [Name]
> **Status:** [Draft / In Review / Approved / Rejected]

# Business Case — Template

This template defines the standard format for a business case: the investment argument for an initiative
before it's committed to. Use it for anything big enough to need a deliberate go/no-go decision — not for a
routine requirement (those go through `scope-analysis`/`write-requirement` instead).

---

## How to Use This Template

1. Copy this structure into a new file, e.g. `product/requirements/<slug>/business-case.md` or alongside the
   related case in `product/cases/<ADO#>-<slug>/`.
2. Name the file `business-case-[initiative-slug].md`.
3. Replace all `[placeholder]` text with initiative-specific content.
4. Mark any sections that are not yet known as `[To be defined]` — do not delete sections.
5. Set the **Overall Assessment** (Positive / Negative / Neutral) and the **Confidence** level for Dev Cost and
   Revenue/Value based on current information.
6. Update the metadata header (`Last updated`, `Status`) every time the file is edited.

---

## Template

```markdown
> **Last updated:** [YYYY-MM-DD]
> **Owner:** [Name]
> **Status:** [Draft / In Review / Approved / Rejected]

# Business Case — [Initiative Name]

---

## Strategy & Objective

[What is this initiative and why are we considering it? 2–3 sentences. Include the primary reason — e.g.,
a support/attrition risk, a compliance requirement, a competitive gap, a platform/infrastructure need.]

---

## Situation

[What do we have now and what is missing? Describe the current state, the gap, and the trigger event that
makes this timely. 2–4 sentences.]

---

## Solution

[What is the proposed approach? Keep this high-level — this is not a spec. 2–3 sentences or a short bullet
list. Reference any requirement/quick-spec doc if one exists.]

---

## Customer / Market

**Target customer:** [Who is this for — a segment of pharmacies, a specific site, all sites]

**Scale / risk if not done:** [Sites affected, support burden, compliance exposure, or churn risk]

**Alternatives customers have:** [What a pharmacy does today without this — manual workaround, a competing
dispense system, a Delphi CCD legacy path]

---

## Market Validation

[What are pharmacies, POs, or support telling us? How has the need been validated? Use bullet points. Each
bullet should be a specific signal — a quote, a named site's issue, a confirmed data point. Not generic
claims.]

- [Specific validation signal]
- [Specific validation signal]

---

## Strategic Alignment

[How does this align with Xumi's direction? Bullet points.]

- [Alignment point — e.g., reduces support load, unblocks a roadmap dependency, required for conformance]
- [Alignment point]

---

## Challenges / Risks

[Specific risks — not a generic list.]

- [Risk — include likelihood and impact where known]
- [Risk]

---

## Development Effort / Cost

**Confidence:** [High / Somewhat confident / Low]

| Phase | Scope | Effort | Notes |
|---|---|---|---|
| Phase 1 | [What is included] | [Weeks / months, # developers] | [Assumptions the estimate relies on] |
| Phase 2 | [Follow-on scope, if any] | [Estimate] | [Estimate or TBD] |

---

## Value / Benefit

**Confidence:** [High / Somewhat confident / Low]

[What does succeeding here actually get Xumi/the pharmacy — reduced support calls, avoided churn, a
compliance box ticked, faster dispensing. Quantify where possible; be explicit where it's not quantifiable.]

---

## Key Success Metrics

[Specific metric and target value.]

- [Metric]
- [Metric]

---

## Next Steps

[What needs to happen before a go/no-go decision, and what happens after?]

- [Action — owner — due date]

---

## Overall Assessment

**Positive / Negative / Neutral**

[One paragraph. Summarise the investment logic: what makes this worth doing (or not), the key condition for
proceeding, and the risk of inaction.]
```

---

## Section Guide

| Section | Required? | Notes |
|---|---|---|
| Strategy & Objective | Yes | Why this exists — the trigger |
| Situation | Yes | Current state and the gap |
| Solution | Yes | High-level proposed approach |
| Customer / Market | Yes | Who this is for and what's at stake |
| Market Validation | Yes | Specific signals only — no generic claims |
| Strategic Alignment | Yes | Beyond the immediate ask |
| Challenges / Risks | Yes | Specific risks, not a generic list |
| Development Effort / Cost | Yes | Phase breakdown with confidence level |
| Value / Benefit | Yes | What succeeding here is worth |
| Key Success Metrics | Yes | Named metrics with target values |
| Next Steps | Yes | Actions, owners, dates |
| Overall Assessment | Yes | Positive / Negative / Neutral with rationale |

---

## Naming Convention

`business-case-[initiative-slug].md` — examples:
- `business-case-aged-care-consolidated-billing.md`
- `business-case-odoo-pos-resync.md`
- `business-case-claims-module-rewrite.md`
