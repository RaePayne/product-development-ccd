> **Brand:** Happen
> **Last updated:** 2026-06-03
> **Owner:** Ruby Launder
> **Status:** Final

# Guide for AI — How to Write Functional Requirements Documents

## Purpose of This Guide

This guide teaches AI assistants how to produce high-quality Functional Requirements Documents (FRDs). It is modelled on a real-world FRD written for a reporting and analytics module within a data portal product. Every structural convention, tone decision, and content pattern described below is drawn directly from that reference document.

An FRD describes **what a system should do and how it should behave** from the perspective of its users and the business. It is not a technical design document (which describes *how* to build it) and it is not a PRD (which describes *why* to build it). The FRD sits between the two: it takes the product goals from the PRD and translates them into specific, testable, implementable behaviours.

---

## Document Structure

Every FRD should follow a consistent section structure. The sections below are listed in the order they should appear. Not every section will be equally long for every project — a simple feature may have a short Scope section and a long Acceptance Criteria section — but every section should be present, even if brief.

### 1. Title

A single line identifying the product, system, or module and the feature area covered.

**Format:** `Functional Requirements Document — [Feature Area]`

Followed by the full module name in bold. This anchors the reader immediately: they know which product and which part of that product this document covers.

**What to get right:**

- Be specific. "Reporting & Analytics" is better than "Reports". "Checkout & Payment Processing" is better than "Purchasing".
- If the FRD covers a sub-module within a larger product, name both: the product and the module.

**Example:**

```
# Functional Requirements Document — Reporting & Analytics

**Jim2 Business Engine — Reporting & Analytics**
```

### 2. Overview

Three paragraphs that answer three questions, in this order:

1. **What exists today?** Describe the current state honestly and specifically. Name the screens, tools, or workarounds that users rely on today. Mention what is broken, missing, or fragmented. This grounds the reader in reality and justifies the work.

2. **What is the broader context?** Explain the operational landscape that surrounds this feature. What other systems, teams, or workflows interact with it? What pain points exist outside the product that this feature addresses?

3. **What does this FRD define?** State clearly what the document covers, what it replaces, and how it relates to other product documents (PRDs, technical specs, etc.).

**What to get right:**

- Be blunt about the current state. If the existing feature is a placeholder that does nothing, say so. If teams rely on spreadsheets and manual processes, say so.
- Name real tools, real team roles, and real workflow problems. Vague language like "the current experience is suboptimal" is useless — say "the Generate button performs a loading animation but produces no output."
- The third paragraph should make the document's relationship to other artefacts explicit. An FRD does not exist in isolation.
- If the feature integrates into existing screens, name those screens here and forward-reference Section 6 (Integration with the Existing Product). The Overview establishes *that* integration is needed; Section 6 specifies it.

### 3. Scope

A clearly divided section with three sub-parts:

**In scope:** A bullet list of what this FRD covers. Be specific enough that a reader can tell exactly which screens, features, workflows, and user types are included. Include platforms, navigation paths, and feature names.

**Out of scope:** A bullet list of what this FRD explicitly does *not* cover. This is just as important as the in-scope list. It prevents scope creep during development and manages expectations for stakeholders who might assume certain features are included. Each out-of-scope item should briefly explain *why* it is excluded (e.g., "future phase", "handled by another module", "not supported on this platform").

**Metadata block:** After the scope lists, include a short metadata block covering:

- Impacted brand(s) or product(s)
- Impacted module(s) or navigation area(s)
- Platform (web, mobile, desktop, etc.) and any platform-specific notes (e.g., "desktop-first, responsive to tablet")
- Existing screens touched — the existing screens/modules this feature modifies, or "None — self-contained" if it introduces no changes to existing screens

**What to get right:**

- Out-of-scope items should be things that a reasonable reader *might* assume are in scope. Do not list obviously unrelated features.
- The metadata block prevents the common problem of an FRD that describes features without ever stating where they live in the product.

### 4. Assumptions

A numbered list of assumptions made during the creation of this FRD. These are things that were assumed to be true based on available context, the PRD, domain knowledge, or reasonable inference — but have not been explicitly confirmed by stakeholders, customers, or technical investigation.

Surfacing assumptions early ensures that stakeholders can validate or challenge them before they become embedded in the business rules, UI specifications, or acceptance criteria. Assumptions are not the same as requirements. A requirement says "the system must do X." An assumption says "we are assuming X is already true, and if it is not, this FRD needs to be revised."

**Rules:**
- List every assumption that influenced the FRD's scope, business rules, UI design, or acceptance criteria
- Be specific — not "we assume the system can handle it" but "we assume the existing product table includes a `barcode` column that is populated for all active items"
- Common assumption categories: data availability, existing infrastructure, licensing, team capacity, user behaviour, and organisational decisions
- If an assumption is later confirmed, move it out of this section (it becomes a stated fact in the relevant section)
- If an assumption is invalidated, update the affected sections of the FRD and log the change
- Mark each assumption with a status: **Unvalidated** (default), **Confirmed**, or **Invalidated**
- This section must always exist — if there are genuinely no assumptions, state that explicitly: *"No assumptions — all requirements in this FRD have been directly confirmed by stakeholders or validated through technical investigation."*

**Format:**

1. **[Short assumption headline]** — [Detailed description of what is being assumed and why.] `Status: Unvalidated`
2. **[Short assumption headline]** — [Description.] `Status: Unvalidated`

**Example:**

> 1. **Existing product table includes barcode data** — The `products` table has a `barcode` column that is populated for all active items. The export logic relies on this field being present and non-null. If barcodes are stored in a separate table or are frequently missing, the export filtering logic needs revision. `Status: Unvalidated`
> 2. **Processing Host runs continuously** — The on-premises Processing Host service runs as a Windows service and is not shut down during business hours. Scheduled exports depend on the service being available at the configured interval. `Status: Unvalidated`

### 5. Terminology

A table of domain-specific terms, abbreviations, and concepts that appear in the document.

**Format:** Two-column table — Term (bold) and Definition.

**What to get right:**

- Include every abbreviation used anywhere in the document. If you write "PO" in section 6, it must be defined here.
- Include domain terms that a developer or designer unfamiliar with the business would not know. "Job Status" or "CardFile" means nothing to someone outside the Jim2 ecosystem; define it.
- Definitions should be concise (one or two sentences) but precise. Include examples where they clarify meaning (e.g., "the central work unit in Jim2 linking a customer, stock, labour, and billing into a single record").
- Do not include general software terms (API, UI, modal) unless the project uses them in a non-standard way.

### 6. Integration with the Existing Product

Describes how this feature attaches to, modifies, or coexists with screens, navigation, and workflows that **already exist in the product**. Section 7 (UI / Interaction Specifications) describes the *new* surface this feature introduces; this section describes the *seam* between the new surface and what is already there.

"Existing product" means Jim2 (or the relevant Happen product) as it is built today — not a system being replaced. This section is about where the new feature bolts onto the live product, not about replicating an older tool.

**This section is required whenever the feature touches an existing screen, navigation element, permission, or workflow.** If the feature is entirely self-contained (a brand-new module with its own entry point and no links from existing screens), state that explicitly: *"Self-contained — this feature introduces no changes to existing screens. It is reached only via its own navigation entry, specified in Section 7."*

**Annotated screenshot(s) of the existing product:** For every existing screen the feature touches, embed a screenshot of the current screen, annotated to mark three things:

- **Entry points** — where the user enters the new feature from (a new button, menu item, tab, ribbon action, or right-click action)
- **Modified regions** — existing components that change (a new column in an existing grid, an added filter, a new status badge)
- **Unchanged regions** — explicitly marked, so engineering knows what *not* to touch

Screenshots are directional only — they capture the current state and locate the seam. They are not a pixel target, and the new surface is still designed to the product's own design system, not to the screenshot.

**Integration points table** — one row per touchpoint:

| Existing screen / element | Location (nav path) | Change required | New or modified |
|---|---|---|---|
| Job List | Jobs module toolbar | Add "Quick Quote" button to the toolbar action row | Modified |
| Left navigation tree | Global navigation | Add "Scheduling" item under the Jobs group | New |

**Navigation & entry-point behaviour:** For each entry point, specify what the user clicks, what opens (a new screen, dialog, docked panel, or tab), and how the user returns to where they came from.

**State & data hand-off:** Describe what context carries across the seam — e.g., "launched from a Job row, the new screen pre-loads that Job Number and displays the linked CardFile."

**Coexistence rules:** State what happens to the existing behaviour. Does the new feature replace an existing action, sit alongside it, or gate it behind a security role or feature flag? If an existing control now behaves differently, say so explicitly.

**What to get right:**

- Mark unchanged regions, not just changed ones. The most common integration defect is the new feature displacing, relabelling, or breaking an existing control — the FRD must state what stays put.
- Name real screens, nav paths, and component locations, using the product's own conventions (Jim2 modules, CardFile, Job, etc.).
- Every modified existing screen should have a corresponding `AC-INT-*` acceptance criterion in Section 13 that verifies the existing surface still works.
- Do not restate the new screen's full UI here — that belongs in Section 7. This section only covers the join.

### 7. UI / Interaction Specifications

This is typically the longest section. It describes every screen, component, and interaction flow the user will encounter, in enough detail that a designer could produce wireframes and a developer could build a working prototype without further clarification.

**How to structure this section:**

Break it into numbered sub-sections, one per screen, flow, or major interaction pattern. A natural ordering is:

1. The landing page or entry point for the feature
2. The primary workflow (e.g., generating a report, creating an order)
3. The result or output view (e.g., viewing the generated report)
4. Secondary workflows (e.g., scheduling, sharing, exporting)
5. Supporting interactions (e.g., AI integration, notifications)

**For each screen or flow, specify:**

- **Layout:** How the page is structured (columns, panels, toolbars). Reference existing design patterns in the product where applicable.
- **Components:** Every element on the page — titles, breadcrumbs, inputs, buttons, cards, tables, filters, toggles, badges, icons. For each component, specify its content, styling cues (size, colour tokens, font weight), and behaviour.
- **Interaction behaviour:** What happens when the user clicks, types, hovers, or submits. Describe the sequence of events step by step.
- **Default values and states:** What is pre-selected or pre-populated when the screen first loads. What does the empty state look like. What does the loading state look like.
- **Variations by context:** If the same screen behaves differently depending on the data type, user role, or prior action, describe each variation. Tables are an effective way to show parameter defaults that vary by context.

**What to get right:**

- Be exhaustively specific about components. Do not write "a filter section" — write "Filter pills: 'All Jobs', 'Open', 'In Progress', 'Completed', 'Invoiced'". Do not write "some action buttons" — write "Action row: 'New Job' (primary button), 'Export' (secondary button), '⋯' overflow menu (Print, Duplicate, Archive)."
- Reference the product's existing design system by name. If the product uses specific colour tokens (e.g., Jim2 Blue `#2E76BC`, Jim2 Orange `#FD9727`), component patterns (metric cards, data tables, status badges), or icon sets, reference them. This ensures visual consistency and reduces design ambiguity.
- Use tables for structured variations. When parameters, defaults, or column definitions vary by type, a table communicates this more clearly than prose.
- Describe the composition of complex views. For a report viewer, do not just say "the report is displayed" — list the sections in order, describe each section type (metrics row, data table, chart panel, summary card), and specify which sections appear for each report type.

### 8. Business Rules

Numbered rules that govern how the system processes data and makes decisions. These are the "if this, then that" statements that encode business logic.

**How to organise:**

- Start with **General** rules that apply across the entire feature.
- Then group rules by **sub-feature or domain** (e.g., Claims Reconciliation, Scheduling, Export). Use subheadings.
- Number rules sequentially across the entire section (not restarting per sub-group).

**What a good business rule looks like:**

- It is a single, testable statement.
- It specifies the condition and the expected behaviour.
- It includes concrete thresholds, formulas, or values where applicable.
- It references specific fields, statuses, or entities by name.

**Examples of good business rules:**

> A stocktake line is flagged as a "variance" when the difference between counted quantity and expected quantity exceeds a configurable threshold (default: 5% or $50, whichever is greater).

> Job Margin = (Total Invoiced Amount) — (Total Parts Cost + Total Labour Cost + Total Overhead Allocation). Displayed as both dollar value and percentage.

> Scheduled report outputs are retained for 90 days. After 90 days, only the metadata (title, date, parameters) is retained; the generated file is deleted.

**What to get right:**

- Business rules must be precise enough to implement without interpretation. "Discrepancies are highlighted" is not a business rule. "A claim line is flagged when the variance exceeds $50 or 5%, whichever is greater" is.
- Include formulas and calculations. Do not say "the margin is calculated based on costs" — say "Job Margin % = ((Invoiced Amount — Total Cost) / Invoiced Amount) × 100, rounded to one decimal place."
- Rules about data retention, access control, and default values belong here.

### 9. Data Requirements

A structured description of what data the feature reads and writes.

**Sub-sections:**

**Data consumed (read):** A table with columns for Data Entity, Fields Required, and Source. This tells the development team exactly which data the feature depends on and where it comes from.

**Data created (write):** A table with columns for Data Entity, Fields, and Notes. This describes any new data the feature produces (e.g., schedule records, history logs, user preferences).

**Validation rules:** A bullet list of constraints on data inputs (e.g., date range limits, required fields, enum restrictions).

**What to get right:**

- Field lists should be specific. "Job data" is not useful — "Job Number, Customer Name, Job Status, Parts Cost, Labour Cost, Total Cost, Invoiced Amount, Margin %" is.
- Name the data source for every consumed entity. This prevents assumptions about where data comes from and surfaces integration dependencies early.
- Validation rules should be expressed as constraints, not aspirations. "Start date must be before or equal to end date. Date range cannot exceed 24 months."

### 10. API & Integration Points

A description of the APIs and external services the feature interacts with. This section can be intentionally high-level if the API architecture is still being defined — state this explicitly rather than inventing specifics.

**For each integration point, describe:**

- What it does (one sentence)
- Whether it is internal or external
- What it accepts and what it returns (at a conceptual level, not a schema level)
- Whether it already exists or needs to be built

**What to get right:**

- This is not an API specification. It is a requirements-level description of what integrations are needed. The technical team will design the actual API contracts.
- If the feature reuses existing APIs, say so. This reduces the perceived scope of work.
- Call out integrations that require coordination with other teams (e.g., email services, AI backends, third-party systems).

### 11. Database & Storage

A brief description of new database tables, storage mechanisms, or data persistence requirements.

**For each new table or store, describe:**

- What it stores
- Key indexing or query considerations
- Retention policy (if applicable)

**What to get right:**

- Be explicit about what is *new* versus what already exists. State clearly if the feature does not require migrating or modifying existing data.
- Mention storage considerations for large outputs (e.g., generated files stored as blobs or in object storage).
- This is not a database schema. It is a requirements-level description of storage needs.

### 12. Error Handling & Validation

A table mapping error scenarios to expected system responses.

**Format:** Two-column table — Scenario and System Response.

**What to get right:**

- Cover the most likely and the most impactful error scenarios. Think about: timeouts, empty results, invalid inputs, permission failures, size limits, service unavailability, and ambiguous user actions.
- System responses should be specific. Do not write "show an error" — write the exact error message text, whether a retry is offered, and whether the error is logged.
- Include what happens when AI or automated components encounter ambiguity (e.g., the AI assistant asks a clarifying question rather than guessing).

### 13. Acceptance Criteria

Testable statements in **Given / When / Then** format that define when each feature is considered complete.

**How to organise:**

- Group by feature area using subheadings (e.g., Report Library, Report Generation, Scheduling, Export).
- If the feature touches existing screens (Section 6), include an **Integration** group (`AC-INT-*`) that verifies the new feature does not break, displace, or relabel the existing surface it attaches to.
- Each criterion gets a unique ID code (e.g., `AC-RL-01`, `AC-RG-02`) consisting of a prefix for the group and a sequential number.
- Present as a checkbox list so criteria can be tracked during QA.
- Every acceptance criterion must include a **Status** tag: `Status: New` (default — needs to be built) or `Status: Currently Supported` (already implemented — documented for context only).
- **Currently Supported** criteria must still be fully documented so that engineering and QA have complete context of existing behaviour, but BMAD agents and developers should treat them as reference material and skip them during implementation planning.

**Format for each criterion:**

```
- [ ] **AC-XX-01:** Given [precondition], when [user action or system event], then [expected outcome]. `Status: New`
```

```
- [ ] **AC-XX-02:** Given [precondition], when [user action or system event], then [expected outcome]. `Status: Currently Supported`
```

**What a good acceptance criterion looks like:**

- It describes one behaviour, not several.
- The precondition is specific enough to reproduce.
- The action is a single, observable event.
- The expected outcome is verifiable — you can look at the screen or the data and confirm it either happened or did not.

**Examples of good acceptance criteria:**

> **AC-RL-01:** Given the user types in the search input, when 2 or more characters are entered, then the report cards are filtered in real time to show only those whose title or description matches the search text. `Status: Currently Supported`

> **AC-EX-01:** Given an Excel export is triggered, when the file is downloaded, then it contains a "Report Info" sheet with the report title, generated by, generated at, parameters, and data freshness timestamp. `Status: New`

> **AC-SC-01:** Given a scheduled report fails to generate, when the first attempt fails, then the system retries after 30 minutes. If the retry also fails, the schedule status is set to "Error" and the user is notified. `Status: New`

> **AC-INT-01:** Given the user is on the existing Job List, when they open the toolbar action row, then a "Quick Quote" button appears to the right of the existing "New Job" button, and the existing button is not moved, relabelled, or disabled. `Status: New`

**What to get right:**

- Every business rule from section 8, every UI behaviour from section 7, and every modified existing screen from section 6 should have at least one corresponding acceptance criterion. If a behaviour has no AC, it cannot be tested. If a behaviour cannot be tested, it will be built wrong.
- Be specific about data, thresholds, and labels. "Then the report is displayed" is weak. "Then the columns match: Stock Code, Description, Qty on Hand, Unit Cost, Total Value, Last Received Date..." is strong.
- Include ACs for edge cases and error paths, not just the happy path.

### 14. Edge Cases

A table of unusual, boundary, or unexpected scenarios and the system's expected behaviour in each.

**Format:** Two-column table — Scenario and Expected Behaviour.

**What to get right:**

- Think about: missing data, zero values, concurrent users, large datasets, deleted or removed entities, partial data, feature interactions, and time boundary conditions.
- The expected behaviour should always describe what the user *sees*, not just what the system does internally. "The stock item row appears with 0 qty on hand and is not hidden, so the user can see which items have been fully consumed" is better than "the system returns zero."
- Edge cases are not bugs — they are design decisions. This section documents those decisions before development begins, preventing arguments later.

### 15. Dependencies & Constraints

**Dependencies:** A list of other systems, services, modules, or data sources that this feature requires to function. For each, explain *what* the dependency is and *why* it matters (e.g., "Report accuracy is directly tied to data freshness and completeness").

**Constraints:** A list of technical, design, or operational limitations that the development team must work within. These include browser support requirements, performance targets, design system mandates, and data freshness limitations.

**What to get right:**

- Dependencies should surface risks. If the reporting module depends on a data pipeline that is unreliable, the FRD should say so.
- Constraints should include measurable targets where possible. "Report generation should complete within 30 seconds for standard reports" is actionable. "Reports should be fast" is not.

### 16. Open Questions

A numbered list of unresolved decisions that affect the requirements but have not yet been answered by stakeholders.

**What to get right:**

- Each question should be specific and actionable. "What about security?" is a bad open question. "Should reports be schedulable for delivery to non-portal users (e.g., board members who don't have portal logins)?" is a good one.
- Open questions should describe the trade-off or decision at stake, not just pose a vague topic. Provide enough context that a stakeholder can answer the question without reading the entire document.
- Open questions are not a sign of incomplete work — they are a sign of mature requirements thinking. No FRD can resolve every decision; this section captures what remains.

### 17. References

A list of source materials, screenshots, prototypes, existing documents, and related artefacts that informed the FRD or that readers should consult alongside it.

Include the source files and locations for the annotated existing-product screenshots used in Section 6, so they are version-controlled and can be refreshed when the existing screens change — rather than pasted once and forgotten.

---

## Writing Principles

These principles apply across every section of the FRD.

### Be specific to the point of being boring

The single most important quality of a good FRD is specificity. Every vague statement is a future argument between a developer, a designer, and a product manager. Write as if the reader has never seen the product, has no access to the team, and must build the feature using only this document.

Instead of "the report includes relevant data," write "the columns match: Job Number, Customer Name, Job Status, Parts Cost, Labour Cost, Total Cost, Invoiced Amount, Margin %, Completion Date."

### Use the product's own language

Reference existing design patterns, colour tokens, component names, route paths, and UI conventions by their actual names. This makes the FRD immediately actionable for the team building the product and ensures visual and behavioural consistency.

### Show, don't just tell

Use tables for structured information (parameter defaults, data fields, error scenarios). Use numbered sequences for multi-step flows. Use checkbox lists for acceptance criteria. Use sub-sections for screen-by-screen specifications. The format should match the content type.

### Write for three audiences simultaneously

An FRD will be read by product managers (who care about scope and business rules), designers (who care about layout, components, and interaction), and developers (who care about data, APIs, error handling, and logic). Every section should be clear to all three, even if some sections are more relevant to one audience than the others.

### State what does not happen

Out-of-scope lists, empty states, zero-value rows, error messages, and edge case behaviours are as important as the happy path. A feature is defined as much by what it does *not* do as by what it does. If a member has no data, does the row disappear or show $0? The FRD must answer this.

### Cross-reference between sections

Business rules in section 8 should correspond to acceptance criteria in section 13. UI specifications in section 7 should reference terminology from section 5. Data requirements in section 9 should align with the fields described in section 7. Integration points in section 6 should each have an `AC-INT-*` criterion in section 13. The sections are not independent essays — they are facets of the same feature, and they should reinforce each other.

### Maintain a neutral, authoritative tone

An FRD is not a pitch, a tutorial, or a conversation. It is a reference document. Write in present tense for how the system should behave ("the system retries after 30 minutes") and past tense for the current state ("the prototype lacks any ability to view, filter, or export reports"). Avoid hedging language ("maybe", "ideally", "it would be nice if"). Either something is a requirement or it is an open question — there is no middle ground.

---

## Common Mistakes to Avoid

**Writing requirements as solutions.** "Use a React modal with a z-index of 999" is an implementation detail, not a requirement. "A modal appears with report parameters" is a requirement. The FRD says *what*; the technical design says *how*.

**Forgetting the empty and error states.** If you describe what happens when a report generates successfully but not what happens when it fails, when it returns no data, or when the user does not have permission, the FRD is incomplete.

**Listing features without describing interactions.** "The report is filterable" is not a UI specification. "A filter row below headers allows column-level text/range filtering" is. "Export is supported" is not a UI specification. "'Export' (dropdown: Excel, PDF, CSV)" with a description of what each format contains is.

**Mixing scope levels in the same document.** An FRD should cover a coherent feature area at a consistent level of detail. If one section describes button colours and another section says "the system handles data," the document is uneven. Aim for uniform depth across all sections.

**Omitting the terminology section.** Domain-specific language is the most common source of misunderstanding between business stakeholders and development teams. If the FRD uses any term that a new team member would not immediately understand, it must be defined.

**Writing acceptance criteria that are not testable.** "The report should look good" is not testable. "The report displays 7 cards in a 2-column grid with title, description, last generated timestamp, and action buttons" is. Every AC must be something a QA engineer can verify by looking at the screen or querying the data.

---

## Checklist Before Finalising

Use this checklist to review an FRD before considering it complete:

- [ ] Every section from 1 through 17 is present, even if some are brief.
- [ ] The Overview honestly describes the current state, the broader context, and what the FRD defines.
- [ ] In-scope and out-of-scope are explicitly listed. Out-of-scope items include a reason.
- [ ] Every abbreviation and domain term used in the document is defined in the Terminology table.
- [ ] Every existing screen the feature touches is shown in an annotated screenshot with entry points, modified regions, and unchanged regions marked — or the feature is explicitly declared self-contained.
- [ ] The integration points table lists every touchpoint with its nav path/location and whether it is new or modified.
- [ ] Coexistence rules state what happens to existing behaviour (replaced / alongside / gated).
- [ ] At least one `AC-INT-*` criterion verifies the existing surface is not broken by the new feature.
- [ ] Every screen and interaction flow is described with specific components, labels, styles, and behaviours.
- [ ] Tables are used for parameter defaults, data fields, and error scenarios.
- [ ] Business rules include specific thresholds, formulas, and conditions — not vague statements.
- [ ] Data requirements list specific field names and sources, not abstract entity names.
- [ ] Error handling covers timeouts, empty results, invalid input, permission failures, and size limits.
- [ ] Every business rule and UI behaviour has at least one acceptance criterion.
- [ ] Acceptance criteria follow Given/When/Then format and are individually testable.
- [ ] Edge cases cover missing data, zero values, large datasets, concurrent users, and boundary conditions.
- [ ] Dependencies identify integration risks, not just component names.
- [ ] Constraints include measurable performance targets.
- [ ] Assumptions are stated as conditions that, if false, require rework. Each has a status (Unvalidated / Confirmed / Invalidated).
- [ ] Open questions are specific, actionable, and provide enough context to be answered independently.
- [ ] The document cross-references between sections (ACs reference business rules; UI specs reference terminology; data requirements align with UI field lists).