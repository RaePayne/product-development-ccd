> **Last updated:** 2026-10-05
> **Owner:** Rae (Product Manager)
> **Status:** Draft — mandatory transition; delivery details to be confirmed

# Business Case — eRx API Integration (CCD)

**Source:** [CPR-61](https://corumhealth.atlassian.net/browse/CPR-61) and product-owner clarification. eRx is decommissioning its adapter service; all dispense vendors must transition to its REST API before March 2027. All CCD sites are in scope. Delivery scope, cost, and detailed cutover requirements still need confirmation.

---

## Strategy & Objective

Transition CCD from eRx's adapter service to its REST API before the adapter is decommissioned. This is a non-negotiable continuity requirement affecting every CCD site; without the transition, those sites risk losing eRx connectivity.

---

## Situation

eRx is decommissioning its adapter service and requires all dispense vendors to use its REST API before March 2027. CCD currently depends on the adapter service [current implementation details to be confirmed]. The exact cutoff date and impact of service loss have not yet been documented; failure to transition puts eRx connectivity at all CCD sites at risk.

---

## Solution

Replace CCD's adapter-service connection with an integration to eRx's REST API, validate the end-to-end workflows, and transition every CCD site before the adapter is decommissioned. Confirm API requirements, implementation scope, test coverage, rollout sequence, rollback approach, and exact deadline with eRx and engineering.

---

## Customer / Market

**Target customer:** All CCD sites and the pharmacies and staff relying on eRx connectivity.

**Scale / risk if not done:** All CCD sites are affected. A supplied customer-count dashboard shows 51 CCD customers; confirm whether customer count maps one-to-one to sites. Failure to migrate before eRx decommissions its adapter service risks loss of eRx connectivity across the customer base. Quantified operational, support, and commercial impact are [To be defined].

**Alternatives customers have:** No alternative for CCD is confirmed. Any temporary workaround, alternative integration path, or service continuity option must be confirmed with eRx; the required destination is its REST API.

---

## Market Validation

The need is a mandatory supplier-driven transition, not a discretionary customer-demand hypothesis. Product-owner clarification states that eRx is decommissioning its adapter service and requires all dispense vendors to transition to its REST API before March 2027.

- Confirm written eRx notice, exact decommissioning date, and technical transition requirements.
- Confirm CCD's current adapter-service dependency and identify all affected sites.

---

## Strategic Alignment

- Preserves eRx connectivity for all CCD sites beyond the adapter-service decommissioning.
- Meets the supplier's mandatory transition requirement for all dispense vendors and avoids a preventable service-continuity gap.

---

## Challenges / Risks

- The fixed pre-March 2027 deadline leaves limited time for discovery, development, end-to-end testing, and rollout; confirm the exact cutoff date and a delivery plan immediately.
- API access, documentation, compatibility, certification/testing expectations, and eRx support dependencies must be confirmed.
- A failed or late cutover could interrupt eRx connectivity across all CCD sites; plan staged validation, monitoring, communications, and rollback or contingency options.
- Site count, implementation effort, and the cost of service disruption are not yet quantified.

---

## Development Effort / Cost

**Confidence:** Low for effort and cost; the need and all-site scope are confirmed.

| Phase | Scope | Effort | Notes |
|---|---|---|---|
| Discovery and planning | Confirm written eRx requirements, exact cutoff date, current CCD dependency, site inventory, and migration/test plan | [To be defined] | Urgent; schedule backwards from the confirmed decommissioning date |
| Delivery and rollout | Implement the REST API integration, complete end-to-end validation, and migrate all CCD sites | [To be defined] | Estimate, phasing, and rollback/contingency plan require engineering and eRx input |

---

## Value / Benefit

**Confidence:** High that continuity risk must be avoided; low for quantified financial value.

The primary value is avoiding loss of eRx connectivity across all CCD sites and maintaining continuity of the affected pharmacy workflows after the adapter is decommissioned. This is a mandatory continuity investment rather than a revenue-growth initiative. Quantify avoided disruption, support impact, and any commercial exposure once site counts and operational data are available.

---

## Key Success Metrics

Track readiness against the confirmed eRx decommissioning date. Candidate measures:

- 100% of CCD sites transitioned to the REST API and validated before March 2027; confirm exact cutoff date.
- eRx REST API end-to-end transaction success: target [To be defined] and no material regression against the current service.
- No loss of eRx connectivity attributable to the adapter-service decommissioning.

---

## Next Steps

- Product Management (Rae) — obtain written eRx notice, exact decommissioning date, REST API requirements, and vendor transition expectations — due date: urgent.
- Engineering owner [To be assigned] — confirm current CCD dependency, site inventory, feasibility, estimate, testing, rollout, and contingency plan — due date: urgently, scheduled against the eRx cutoff.
- Product Management and Engineering — agree milestones and track readiness to ensure every CCD site transitions before the cutoff — owners/dates [To be confirmed].
- Product Management — quantify avoided disruption and update the case as site and cost data becomes available — due date [To be defined].

---

## Overall Assessment

**Positive**

This transition is non-negotiable: eRx is decommissioning its adapter service and requires all dispense vendors to move to its REST API before March 2027. All CCD sites are affected, and not completing the migration risks loss of eRx connectivity. Proceed with delivery planning immediately; confirm the exact cutoff, API requirements, site inventory, delivery estimate, and contingency plan while protecting enough time to validate and transition every site.
