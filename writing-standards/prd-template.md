> **Brand:** Happen
> **Last updated:** 2026-05-18
> **Owner:** Ruby Launder
> **Status:** Final

<!-- 2026-05-18 — Heading convention updated: use `## Functional Requirements / Use Cases` instead of bare `## Use Cases`. Reason: BMAD format-detection validators (Step 2, Step 10) scan for "Functional Requirements" / "Features" / "Capabilities" as the canonical Level-2 anchor; the combined heading satisfies BMAD while preserving the Happen "use cases = functional requirements" convention. -->


# PRD Template

> This template defines the exact structure for every `prd.md` file. Follow this structure exactly. Do not add, remove, or reorder sections unless a section is genuinely not applicable — in which case mark it as "[Not applicable — reason]".
>
> **Tone:** Clear, direct, written for a mixed audience (stakeholders, designers, developers). Lead with context and customer reality. Use real examples, real customer names where available, and real scenarios — not abstract descriptions. Write as if explaining the problem to a smart colleague who has no context.
>
> **Length:** As long as it needs to be. Don't pad, but don't skip detail that matters. Pain points should feel real. Use cases should be exhaustive enough that a developer can build from them without follow-up questions.

---

## Template Structure

Every `prd.md` must follow this structure:

---

````markdown
# [Feature/Module Name]

> **Brand:** Happen
> **Project:** [Project name and path, e.g. happen/project-payroll/prd]
> **Last updated:** [YYYY-MM-DD]
> **Owner:** [Name]
> **Status:** [Draft / In Progress / Final]

## Introduction

2-4 paragraphs that set the scene. This is the most important section — it should give a reader full context without needing to read anything else first.

Cover:
- What the problem is, grounded in real customer behaviour (not abstract)
- Who experiences this problem and how they deal with it today (the messy reality)
- What the customer's #1 priority actually is (based on research, not assumptions)
- What this module/feature will provide as a solution — one clear summary sentence

Write this as if you're explaining the opportunity to someone who just joined the team. Use specific customer names, specific examples, and specific pain — not generalities.

**Example (from Jim2 Reporting):**
> Businesses like Total Pumps want a clear, reliable way to see how their stock, jobs, and purchasing are tracking — without calling support to set up a report. Today, this is typically done via a mix of exported Excel files, manual VLOOKUP across stock and sales data, and ad-hoc analysis from accounting — making it slow, error-prone, and impossible to get a consistent picture of the business. Total Pumps' #1 priority is trusting the numbers they see on screen without needing to cross-check in a spreadsheet.

---

## Assumptions

A numbered list of assumptions made during the creation of this PRD. These are things that were assumed to be true based on available context, domain knowledge, or reasonable inference — but have not been explicitly confirmed by stakeholders, customers, or technical investigation.

Surfacing assumptions early ensures that stakeholders can validate or challenge them before they become embedded in the design, use cases, or architecture.

**Rules:**
- List every assumption that influenced the PRD's scope, design, or acceptance criteria
- Be specific — not "we assume the system can handle it" but "we assume the Processing Host has outbound internet access on port 21 for FTP connections"
- If an assumption is later confirmed, move it out of this section (it becomes a stated fact in the relevant section)
- If an assumption is invalidated, update the affected sections of the PRD and log the change
- Mark each assumption with a status: **Unvalidated** (default), **Confirmed**, or **Invalidated**
- This section must always exist — if there are genuinely no assumptions, state that explicitly: *"No assumptions — all requirements in this PRD have been directly confirmed by stakeholders or validated through research."*

**Format:**

1. **[Short assumption headline]** — [Detailed description of what is being assumed and why.] `Status: Unvalidated`
2. **[Short assumption headline]** — [Description.] `Status: Unvalidated`

**Example:**
> 1. **FTP is the only supported delivery mechanism** — Myfoodlink only accepts product catalogue files via FTP upload. There is no API, webhook, or alternative integration method available. This assumption is based on the current operator workflow and has not been confirmed directly with Myfoodlink. `Status: Unvalidated`
> 2. **Operators have a single default price point** — Each product has exactly one default (non-promotional) price in Impos, drawn from the default price point. Products with multiple non-promotional price tiers are not expected. `Status: Unvalidated`

---

## Scope

Optional but recommended for any PRD that defines a component with a meaningful boundary against other components. Two subsections:

- **In scope (this project owns)** — bullet list of capabilities, surfaces, and concerns the project owns. Be specific. Each bullet should be a thing engineering will build or maintain.
- **Out of scope (other components or future work)** — bullet list of capabilities that *look like* they belong here but don't, each named with the component or future workstream that actually owns it. This is the misroute-prevention list — it stops engineering from accidentally building into the wrong boundary.

Place this section **after Assumptions** so readers know what's assumed before they read what's in/out. Omit only if the PRD covers a feature with no contestable boundary against other components.

---

## Linked PRDs

List other PRDs that are tightly coupled to this project. These are PRDs that engineering and AI agents **must review** before starting work on this project — because changes in one directly affect the other.

Only include PRDs with a genuine dependency or overlap (shared data models, shared UI surfaces, upstream/downstream data flows, or features that must be coordinated). Do not list every PRD in the product — only the ones where misalignment would cause problems.

| Linked PRD | Relationship | Why It Matters |
|------------|-------------|----------------|
| [PRD name](relative/path/to/prd.md) | [e.g. Upstream dependency / Shared data model / Shared UI surface / Must ship together] | [One sentence explaining the specific coupling — what breaks or conflicts if this PRD is ignored.] |

**Rules:**
- Use relative links to the linked PRD file
- Keep the "Why It Matters" column specific — not "they're related" but "both write to the `stock_transactions` table and share the variance calculation logic"
- If there are no linked PRDs, state that explicitly: *"No linked PRDs — this project is self-contained."*
- Update this section whenever a new dependency is discovered during development
- Linked PRDs should be reviewed in full (not just skimmed) before beginning design or implementation work on this project

**Example:**

| Linked PRD | Relationship | Why It Matters |
|------------|-------------|----------------|
| [Stock Management](../project-stock-management/prd/prd-stock-management.md) | Shared data model | Both projects read/write `stock_items` and `stock_transactions`. Variance thresholds defined in Stock Management affect reporting in this module. |
| [Purchase Orders](../project-purchase-orders/prd/prd-purchase-orders.md) | Upstream dependency | This module's "expected quantity" calculation depends on received PO data. Changes to PO receipt workflow directly affect stock take accuracy. |

---

## Terminology

A table of domain terms specific to this module/feature. Only include terms that a reader needs to understand this PRD. For terms that apply across the whole product, reference the terminology dictionary instead.

| Term | Definition |
|------|-----------|
| **[Term]** | [Clear, specific definition. Include examples where helpful. If a term has sub-types or categories, list them within the definition.] |
| **[Term]** | [Definition] |

**Rules:**
- Bold the term name in the first column
- Definitions should be specific enough that two people reading them would understand the same thing
- Include real-world examples where they clarify meaning (e.g. "e.g. Dicker Data, Ingram Micro, Synnex")
- If a term has a common abbreviation, include it (e.g. "Purchase Order (PO)")
- If a term is easily confused with another, clarify the difference

---

## Key Success Metrics

Bullet list of measurable outcomes that define whether this module/feature is successful. These should be specific enough to track but may include placeholders for exact targets (e.g. "within X days").

Mix of:
- Adoption metrics (who's using it, how often)
- Data quality metrics (completeness, accuracy)
- Efficiency metrics (time saved, manual steps eliminated)
- Business outcome metrics (ROI improvement, volume uplift)

**Example:**
> - Number of customers generating reports without requesting support assistance.
> - ≥ 90% of stock variances identified within one business day of stocktake completion.
> - Reduction of time to reconcile PO receipts from hours (manual counting) to < 10 minutes (scan-to-receive).

---

## Primary Customer

Who is this for? Name the customer type and describe them specifically — not just a role title, but what they do, what they need, and why they need it.

**Format:**

[Customer type] (e.g. [real company names]) who:

- [What they do that's relevant]
- [What they need]
- [What they're currently stuck with]

### Primary Users at the [Customer Type]

Bullet list of the specific roles/job titles who will use this module day-to-day.

- [Role 1]
- [Role 2]
- [Role 3]

---

## Pain Points

Numbered list of the real problems customers face today. Each pain point gets a heading and supporting detail underneath.

**Rules:**
- Lead with the pain, not the solution
- Use real quotes or paraphrased customer language where available
- Include specific examples of the messy workarounds they use today
- Include the types of questions they struggle to answer

**Format:**

### 1. [Pain point headline — short, descriptive]
- [Supporting detail]
- [Real example or customer question]
- [Impact of this pain]

### 2. [Pain point headline]
- [Supporting detail]

---

## Design

### User Flow: [Flow Name]

**Primary User:** [Role name] ([additional context about this user, e.g. "no dedicated analytics team"])

#### Flow Steps

Walk through the end-to-end flow step by step, numbered. For each step, describe:
- What the user does
- What the system shows/does in response
- What decisions the user makes

Use indented bullets under each numbered step for detail.

**Format:**

**1. [Step Name]**
- [What the user does]
- [What the system shows]

**2. [Step Name]**
- [User action]
- [System response, including specific data/fields shown]

...continue through to end state.

**[N]. End State**
- [What the user now has/knows/can do]
- [What happens next]

---

### Alternative Paths

Short-form descriptions of alternate ways users might move through the flow. One line per path.

**Format:**

**Path A: [Path Name]**
[Step] → [Step] → [Step] → [Step] → End

**Path B: [Path Name]**
[Step] → [Step] → [Step] → End

---

### Key Decision Points

Numbered list of the critical decisions users make during the flow. Each includes the options they're choosing between.

1. **[Decision]** ([Option A, Option B, Option C])
2. **[Decision]** ([Option A, Option B])

---

### Success Criteria

Checkmark list of what "done" looks like from the user's perspective. Each criterion should be testable.

- ✓ [User can do X within Y timeframe]
- ✓ [User can see Z as the primary metric]
- ✓ [User can export/share/compare in a specific way]

---

## Functional Requirements / Use Cases

Grouped by functional area. Each group gets a heading, then use cases listed underneath.

> **Heading convention.** Use the heading `## Functional Requirements / Use Cases` (not bare `## Use Cases`). BMAD format-detection validators (Step 2, Step 10) scan for `## Functional Requirements`, `## Features`, or `## Capabilities` as the canonical Level-2 functional-requirements anchor; the combined heading satisfies the validator while preserving the Happen "use cases = functional requirements" convention.

> **Use cases as functional requirements.** Include this paragraph at the top of every PRD's `## Functional Requirements / Use Cases` section so external validators (BMAD, etc.) can extract the functional-requirement set:
>
> *"Use cases serve the role of functional requirements in this PRD: each `UC-{MODULE}-###` is both a user story and a numbered functional requirement, addressable as `UC-{MODULE}-###` from the FRD, architecture, design spec, and test plan."*

**Rules:**
- Use case format: "As a [specific role], I want to [specific action] so that [specific outcome]."
- Acceptance criteria must be detailed enough that a developer can build from them and a QA can test against them without follow-up questions
- Include field lists, validation rules, system behaviours, and edge cases within acceptance criteria
- Group use cases by functional area, not by user role
- Every use case must include a **Status** tag: `Status: New` (default — needs to be built) or `Status: Currently Supported` (already implemented — documented for context only)
- **Currently Supported** use cases must still be fully documented with acceptance criteria so that engineering and QA have complete context, but BMAD agents and developers should treat them as reference material and skip them during implementation planning

### Choosing a Format

Use whichever format best fits the complexity of the use cases. Both are acceptable. You can mix formats within the same PRD if some functional areas have simple use cases and others have complex ones.

---

**Format A: Table** — best when use cases and acceptance criteria are short to medium length. Keeps things compact and scannable.

### [Functional Area Name]

| Status | Use Case | Acceptance Criteria |
|--------|----------|-------------------|
| `New` | As a [role], I want to [action] so that [outcome]. | [Criteria as a continuous paragraph. Each criterion is a sentence. Include specific fields, validation, system behaviour.] |
| `Currently Supported` | As a [role], I want to [action] so that [outcome]. | [Criteria as a continuous paragraph.] |

**Example:**

### Reporting & Export

| Status | Use Case | Acceptance Criteria |
|--------|----------|-------------------|
| `New` | As an operations manager, I want to export job profitability data so that I can use it in monthly reviews and management reporting. | I can export the job cost analysis view as Excel or PDF. I can export individual job details as Excel or PDF. Exports include: job number, customer, job status, parts cost, labour cost, total cost, invoiced amount, margin %, completion date. |
| `Currently Supported` | As a stock controller, I want to generate a stock valuation report by warehouse location so that I can reconcile physical stock against the general ledger. | I can generate a stock valuation report filtered by warehouse location and date. The report shows: stock code, description, quantity on hand, unit cost, total value, valuation method. I can export as Excel or PDF. |

---

**Format B: Expanded** — best when acceptance criteria are long, have multiple conditions, need sub-grouping, or include edge cases and notes. Easier to read and edit when there's a lot of detail.

### [Functional Area Name]

#### UC-[MODULE]-[NUMBER]: [Short descriptive title]

`Status: New`

**As a** [specific role], **I want to** [specific action] **so that** [specific outcome].

**Acceptance Criteria:**
- [Criterion 1 — specific, testable]
- [Criterion 2 — include field names, validation rules, system behaviour]
- [Criterion 3 — include edge cases]
- [Criterion 4]

**Notes:** [Optional — any additional context, constraints, or dependencies]

#### UC-[MODULE]-[NUMBER]: [Short descriptive title]

`Status: Currently Supported`

**As a** [specific role], **I want to** [specific action] **so that** [specific outcome].

**Acceptance Criteria:**
- [Criterion 1]
- [Criterion 2]

**Example:**

### Stock Take

#### UC-STK-001: Start a new stock take

`Status: Currently Supported`

**As a** stock controller, **I want to** start a new stock take for my venue **so that** I can count physical inventory and reconcile against expected levels.

**Acceptance Criteria:**
- I can create a new stock take from the Stock Takes list page
- The system pre-populates all active stock items for the venue with their expected quantities
- I can optionally select a subset of categories or locations to count (partial stock take)
- The stock take is created in Draft status and can be edited before counting begins
- Only one stock take can be in progress per venue at a time — the system prevents creating a second
- The stock take records who created it and when
- I can add notes to the stock take (e.g. "End of month count", "Spot check — spirits only")

**Notes:** Expected quantities are calculated from last finalised stock take + received POs - recorded sales - recorded wastage.

#### UC-STK-002: Count stock during a stock take

`Status: New`

**As a** stock controller, **I want to** enter counted quantities for each stock item **so that** the system can calculate variances against expected levels.

**Acceptance Criteria:**
- For each item I can enter the counted quantity in the item's unit of measure
- The system shows expected quantity alongside the entry field for reference
- I can mark an item as "not counted" with a reason (e.g. "not accessible", "item discontinued")
- The system auto-saves as I enter counts — no manual save required
- I can see a running total of items counted vs items remaining
- I can leave and return to the stock take without losing progress
- Variance is calculated and displayed in real-time as I enter counts (actual - expected)
- Negative variances (short) are highlighted visually

---

## UX/UI Requirements

For `projectType: web_app` PRDs (and any PRD with a meaningful user-facing UI), include this section. It exists so external validators (BMAD project-type checks, etc.) can find a dedicated UX/UI requirements section, while keeping the source of truth in the project's design spec.

Use this exact one-paragraph cross-reference rather than duplicating screen-level detail:

> *"The screen inventory, layouts, states, fields, validation behaviour, focus order, copy, and branding rules are defined in [design/design-spec.md](../design/design-spec.md). The design spec is the source of truth for all UX/UI requirements — this PRD does not duplicate screen-level detail. The use cases above (UC-{MODULE}-###) define the requirements each screen must satisfy; the design spec defines how each screen meets them. If the design spec and this PRD ever diverge on a UX behaviour, the design spec wins for visual/layout/interaction concerns and this PRD wins for functional/business-rule/security concerns. Responsive-layout breakpoints and the accessibility verification approach are pinned in this PRD as NFRs so they remain non-negotiable independent of design iteration."*

Rationale: the Happen pipeline mandates a separate `design/design-spec.md` as the UX source of truth, and the repo rule "Never duplicate content between docs — reference the source instead" applies. The cross-reference pattern satisfies the BMAD structural check without creating a second source of UX truth.

---

## Technical Constraints

Optional. Use this section to name platform capabilities that are load-bearing on the requirements above without re-litigating them inside use cases. Follow the outcome-based form — describe the *required capability* (e.g. "edge routing layer supporting slug-keyed path routing rules, TLS termination, HSTS, security-header configuration"), not the vendor name. The chosen vendor for each capability is recorded in the architecture doc / ADRs, not the PRD.

| Concern | Required capability (outcome) | Used by |
|---------|------------------------------|---------|
| [Concern name] | [Outcome-based capability description] | [UC IDs that depend on it] |

Rationale: PRDs that name vendors signal "decided" to downstream readers and shut down legitimate trade-off conversations during architecture. They also make the PRD brittle — any platform swap forces a PRD revision rather than an ADR.

---

## Decision Log

Optional but strongly recommended. A chronological record of significant scope, contract, or ownership decisions made during PRD evolution. Items here were previously in active use cases, scope, or assumptions but have been resolved — captured here so the rationale is preserved without polluting the buildable scope.

| Date | Decision | Rationale |
|------|----------|-----------|
| YYYY-MM-DD | [Decision in one line. Include `(Was previously UC-XXX-NNN)` or `(Was previously ...)` cross-reference when a use case was retired.] | [Short rationale — what was confirmed or what was rejected and why.] |

When a decision supersedes an earlier one, mark the earlier row with `*(Superseded YYYY-MM-DD — see entry below.)*` and add the new entry. Do not delete superseded entries.

When a Decision Log entry replaces an inline requirement, **do not duplicate the rationale inline** — the Decision Log is the sole carrier of "why this changed." Inline parentheticals like `*(Revised YYYY-MM-DD — was previously X.)*` in buildable sections should be removed when the Decision Log carries the entry.

---

## Open Questions

Bullet list of unresolved questions. If there are none, state that explicitly.

- [ ] [Question — include who needs to answer if known]
- [ ] [Question]

Or:

*(No open questions at this time)*

---

## References

Bullet list of source material, related documents, competitor products, or external links that informed this PRD.

- [Reference 1]
- [Reference 2]

When a reference points to an access-gated resource (internal Jira, Confluence, Slack archive, etc.), annotate the entry so external reviewers know it is not a missing link:

- [JIRA Idea: PR-XXX](https://happenbiz.atlassian.net/jira/polaris/projects/PR/ideas/PR-XXX) — *access-gated: requires Happen Atlassian login. The PRD itself is the authoritative product definition; the linked resource is for portfolio-roadmap traceability or supplementary context only.*
````

---

## Rules for Writing PRDs

1. **Lead with real customer context** — the introduction should name real customers, real behaviours, and real pain. Not "users need a way to..." but "Total Pumps wants a clear, reliable way to..."
2. **Terminology goes in the PRD, not just the dictionary** — include terms specific to this module directly in the doc so it stands alone. Shared terms can reference the dictionary.
3. **Pain points must feel real** — include actual customer questions, current workarounds, and the messy reality. Not "reporting is difficult" but "teams export stock data into Excel, VLOOKUP across purchase orders and sales invoices, then manually reconcile against the GL."
4. **Use cases must be exhaustive** — a developer should be able to build from the acceptance criteria without asking follow-up questions. Include specific fields, specific validations, specific system behaviours.
5. **Choose the right format for use cases** — use tables when criteria are short and scannable. Use expanded format when criteria are long or have multiple conditions. Mix formats within the same PRD if it makes sense. Both are equally valid.
6. **Design section goes in the PRD** — user flows, alternative paths, key decision points, and success criteria live here, not in a separate design doc. The design spec in the designs/ folder covers visual and interaction detail — the PRD covers the functional flow.
7. **Use terminology from the dictionary** — never introduce a term in the use cases that isn't defined in either the Terminology section of this PRD or the terminology dictionary.
8. **Cross-reference with relative links** — link to related modules, the product overview, and the requirements doc where relevant.
9. **Open questions are explicit** — if there are none, say so. An empty section looks like you forgot.
10. **Write in Australian English** — colour not color, organisation not organization, programme not program (unless referring to a software program).