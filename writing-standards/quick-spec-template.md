 Quick Spec Template

> This template defines the structure for every quick spec. A quick spec is a lightweight product specification for small-to-medium features — equivalent to a single epic with 1-5 stories. It captures the problem, solution, and 1-2 use cases (with embedded functional decisions) in a single document.
>
> **When to use a quick spec instead of the full PRD + FRD pipeline:**
> - The feature is small enough to describe in one document (1-5 stories)
> - It doesn't require new personas, customer research, or multiple user flows
> - The functional decisions are few and can be stated directly
> - It can be scoped and built within a single epic
>
> **When to use the full pipeline instead:**
> - The feature requires multiple user flows or 3+ use cases
> - Multiple business rules need formal documentation
> - New UI screens or significant UX work is required
> - Customer research, personas, or phased rollout is needed
>
> **Tone:** Clear, direct, specific. Same standard as a PRD — real examples, real customer context, testable criteria. Being short does not mean being vague.
>
> **Language:** Australian English.
>
> **Deliverables — spec + wireframe (always both):** Every product quick spec is its own folder, `quick-spec-[slug]/`, holding two files:
> 1. `quick-spec-[slug].md` — this spec, written first.
> 2. `quick-spec-[slug]-wireframe.html` — a low-fidelity wireframe, created second (mandatory). It lays out the screens behind the use cases so they're concrete and easy to discuss. Single self-contained HTML (inline CSS/JS, no dependencies), one quick pass — not the 2-3 concept variants a full project's `design/explorations/` uses.

---

## Template Structure

Every quick spec must follow this structure:

---

````markdown
# [Feature Name]

> **Brand:** [Brand name]
> **Last updated:** [YYYY-MM-DD]
> **Owner:** [Name]
> **Status:** [Draft / In Review / Approved / In Progress / Done]

## Summary

1-2 paragraphs covering:

- **What is the problem?** Ground it in real customer behaviour — who experiences this, what they do today, and why the current state is painful.
- **What is the solution?** One clear statement of what this feature will do.
- **Who benefits and how?** Name the customer type and the specific outcome they get.

Write this as if explaining the opportunity to someone who just walked into the room. Use real customer names and real scenarios where available.

---

## Scope

**In scope:**
- [Specific feature, screen, workflow, or behaviour included]
- [Be precise — name the screens, actions, and user types]

**Out of scope:**
- [What is explicitly excluded — with a brief reason why]
- [Things a reader might reasonably assume are included but are not]

---

## Works With Existing Product

1-2 paragraphs describing how this feature fits into the product that already exists. Quick specs almost always extend or modify something already built — make the integration explicit so a developer understands what they're *touching*, not just what they're *adding*.

Cover:

- **What already exists** that this feature builds on, extends, or sits alongside — name the specific screens, modules, data, or workflows (and link to the relevant PRD/FRD where one exists)
- **What changes** for the existing product — new entry points, modified screens, altered behaviour
- **What stays the same** — existing behaviour that must be preserved, and anything this feature must not break

If a use case below relies on functionality that is already built, tag it `Status: Currently Supported` so engineering treats it as reference context rather than new work.

**Example:**
> This extends the existing **Supplier Pricing** screen (Stock module) rather than adding a new screen. The markup action appears as a new "Apply markup" button in the existing supplier toolbar. Existing per-product manual price editing is unchanged — manually locked prices continue to take precedence and are excluded from bulk markup. No changes to the promotional pricing engine, which continues to override the calculated sell price as it does today.

---

## Assumptions

A numbered list of assumptions. If none, state that explicitly.

1. **[Short headline]** — [What is being assumed and why.] `Status: Unvalidated`

---

## Use Cases

1-2 use cases covering the core functionality. Use the expanded format. Group by functional area if there are two distinct areas; otherwise a single group is fine.

Each use case should include acceptance criteria AND any critical functional decisions as **Decisions** entries. Functional decisions are the non-obvious "how should this work" choices — design and business logic that could reasonably go multiple ways. Embedding them directly in the use case keeps everything in one place.

### [Functional Area Name]

#### UC-[SLUG]-[NUMBER]: [Short descriptive title]

`Status: New`

**As a** [specific role], **I want to** [specific action] **so that** [specific outcome].

**Acceptance Criteria:**
- [Criterion — specific, testable. Include field names, validation rules, system behaviour.]
- [Criterion — include what happens on success AND what happens on failure or edge cases.]
- [Criterion]

**Decisions:**
- **[Decision question?]** — [Chosen approach.] *Why:* [Brief rationale.]

**Notes:** [Optional — additional context, constraints, or dependencies for this use case.]

---

**Example:**

### Price Adjustments

#### UC-PRC-001: Apply a percentage markup to a supplier's catalogue

`Status: New`

**As a** venue purchasing manager, **I want to** apply a percentage markup to all products from a selected supplier **so that** my sell prices stay profitable without updating each product individually.

**Acceptance Criteria:**
- I can select a supplier from the supplier list and enter a markup percentage (0.01% to 999.99%)
- The system previews the calculated new prices for all affected products before I confirm
- The preview shows: product name, current price, new calculated price, and the dollar difference
- I can exclude individual products from the preview before confirming
- On confirm, all non-excluded products are updated immediately
- Products with a locked price (manually overridden) are excluded from the markup and shown separately in the preview with a "locked" indicator
- If no products exist for the selected supplier, the system shows an empty state: "No products found for [Supplier Name]"
- The system logs who applied the markup, when, and the percentage used

**Decisions:**
- **Should price changes apply immediately or require approval?** — Changes take effect immediately on save. No approval workflow. *Why:* Target customers are single-site operators who manage their own pricing. An approval step adds friction without value for this segment.
- **How are rounding rules applied to calculated prices?** — Banker's rounding (round half to even) to the nearest cent. *Why:* Consistent with the existing pricing engine. Avoids cumulative rounding bias across large catalogues.

**Notes:** This does not affect promotional pricing. Promotions always override the calculated sell price.

---

## Wireframe

A low-fidelity wireframe ships alongside this spec to make the use cases concrete and easy to discuss. Build it from the use cases above, as the second step — after the spec is written.

- [Wireframe — [Feature Name]](quick-spec-[slug]-wireframe.html)

The wireframe is a single self-contained HTML file (inline CSS/JS, no dependencies) at low fidelity — one quick pass, not the 2-3 concept variants a full project uses. It lives in this spec's folder as `quick-spec-[slug]-wireframe.html`.

---

## Open Questions

Unresolved decisions that affect the feature. If none, state that explicitly.

- [ ] [Specific question — include who needs to answer if known]
- [ ] [Question — describe the trade-off at stake]

Or:

*(No open questions at this time.)*

---

## References

Links to source material, related documents, or existing specs that informed this quick spec.

- [Reference 1](relative/path)
- [Reference 2](relative/path)
````

---

## Rules for Writing Quick Specs

1. **Same quality bar as a PRD, less breadth** — A quick spec is shorter because the feature is smaller, not because the writing is lazier. Every statement must be specific and testable.
2. **Functional decisions live inside use cases** — Critical "how should this work" choices belong in the **Decisions** block under each use case. This keeps context together and avoids a developer jumping between sections.
3. **1-2 use cases maximum** — If you need more than two use cases, the feature likely needs the full PRD + FRD pipeline. The use cases you include should be comprehensive — a developer should be able to build from the acceptance criteria and decisions without follow-up questions.
4. **Scope must be tight** — A quick spec with a broad scope is a PRD in disguise. The in-scope list should be concrete and the out-of-scope list should cut off anything that could cause scope creep.
5. **Always state how it works with the existing product** — Quick-spec features rarely live in isolation; they extend or modify something already built. The **Works With Existing Product** section must make clear what's being touched, what changes, and what must not break. Tag use cases that rely on already-built functionality as `Status: Currently Supported`.
6. **Always pair the spec with a wireframe** — Every product quick spec is delivered as a folder containing the spec and a low-fidelity wireframe (`quick-spec-[slug]-wireframe.html`). Write the spec first, then build the wireframe as the second step — a single self-contained HTML file (inline CSS/JS, no dependencies), one quick pass, that lays out the screens behind the use cases so they're easy to discuss. A quick spec is not complete without its wireframe.
7. **Don't skip assumptions** — Quick specs are often written with less stakeholder review than full PRDs. Surfacing assumptions is even more important here.
8. **Use terminology from the dictionary** — Same rule as PRDs. Never introduce a term that isn't defined in the terminology dictionary or in the spec itself.
9. **Cross-reference, don't duplicate** — If a related PRD or FRD already defines context, link to it. Don't reproduce content.
10. **Write in Australian English** — colour, organisation, programme (unless referring to a software program).
