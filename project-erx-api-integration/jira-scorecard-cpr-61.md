> **Last updated:** 2026-10-05
> **Owner:** Rae (Product Manager)
> **Status:** Draft — mandatory transition; delivery details still to be confirmed

# JIRA Score Card: CPR-61 eRx API Integration (CCD)

The score card values for [CPR-61](https://corumhealth.atlassian.net/browse/CPR-61). Each text field is limited to 255 characters in JIRA. This summary reflects the confirmed transition driver and is condensed from the [business case](business-case-erx-api-integration.md).

| Field | Value |
|---|---|
| Strategy & Objective | Migrate CCD from the eRx adapter service to its REST API so all CCD sites retain eRx connectivity after the adapter is decommissioned. Complete the transition before March 2027. |
| Situation | eRx is decommissioning its adapter service. All dispense vendors must transition to the eRx REST API before March 2027; otherwise CCD sites risk losing eRx connectivity. |
| Solution | Replace CCD's adapter-service integration with eRx's REST API, then test and transition every CCD site before the adapter is decommissioned. Detailed scope and cutover plan remain to be confirmed. |
| Target Market | All CCD sites and the pharmacies and staff relying on eRx connectivity. |
| Market Size | 51 CCD customers are shown in the supplied customer-count dashboard; all CCD sites are in scope. Customer count is not confirmed to equal site count. |
| Key Competitors | All dispense vendors must make the same transition; timely completion is necessary to maintain eRx service continuity. |
| Key Success Metrics | Transition and validate all CCD sites before March 2027; avoid loss of eRx connectivity. Confirm exact cutoff date and API transaction targets. |
| Market Validation | Mandatory external transition: eRx is decommissioning its adapter service and requires all dispense vendors to use its REST API before March 2027. |
| Unfair Advantage | CCD's existing customer footprint makes a complete, coordinated migration essential; no unique competitive advantage is confirmed. |
| Challenges / Risks | Fixed pre-March 2027 deadline, REST API readiness, integration/testing effort, and coordinating migration across all CCD sites; exact cut-off date and plan need confirmation. |
| Revenue Confidence | **0** |
| Overall Verdict | **Positive** |
| Financial Value | **Cost Avoidance** — avoids loss of eRx connectivity across CCD sites; quantify exposure and confirm this JIRA dropdown value. |
