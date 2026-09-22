# Roadmap Scratchpad Template

> This template defines the structure for every Roadmap Scratchpad. A Roadmap Scratchpad is a **brand-level**, **lightweight** high-level planning view used to size scope, surface gaps, and stage a phasing pass for a brand's near-term build. It is **not a delivery plan** — it is the rough-order-of-magnitude artefact a PM uses to reason about who is building what, in what order, and roughly when.
>
> **When to use a roadmap scratchpad:**
> - You need to see the whole brand's near-term build at a glance — workstreams, owners, rough effort, sequencing
> - You need to stress-test resourcing — does the critical path actually fit, who sits idle, where the bottlenecks are
> - You need to pull a phasing pass together before committing to a delivery plan
>
> **When NOT to use one:**
> - You need a sequenced, MMP-scoped plan for a specific multi-project initiative — use an [implementation plan](./implementation-plan-template.md) instead
> - You need a cross-functional commercial readiness tracker — that's a Readiness Plan (no template, lives in `implementation-plans/`)
> - You need PRD/FRD-level functional detail — those live per-project under `[brand]/project-[project-name]/`
>
> **Format:** Rough-order-of-magnitude effort (W / M) — never story points or finished-engineering-day estimates. One Mermaid Gantt chart per owner with a shared date axis. Per-workstream tables of Feature / Sub-items / Effort. Roll-up table linking workstreams to owners.
>
> **Tone:** Direct, sizing-oriented, candid about uncertainty. Flag SPIKEs explicitly. Flag TBDs explicitly. State assumptions plainly so they can be challenged.
>
> **Language:** Australian English.
>
> **Location & filename:** Markdown (`.md`) at `strategy/[brand]-roadmap-scratchpad.md`. One scratchpad per brand — not per initiative, not per project.
>
> **Owner column rule:** Every owner named in the document (in Gantt sections, roll-up tables, workstream tables, or sequence notes) must resolve to a short name defined in the brand's team file (`strategy/[brand]-team.md`). Use first-name-plus-initial when first-name is ambiguous (e.g. "Mark R" / "Mark M"). Do NOT restate the team mapping inline.

---

## Template Structure

Every roadmap scratchpad must follow this structure:

````markdown
> **Brand:** [Brand name]
> **Last updated:** [YYYY-MM-DD]
> **Owner:** [Name — the PM accountable for this scratchpad]
> **Status:** Draft | In Review | Approved

# [Brand] Roadmap Scratchpad

Lightweight high-level planning view of [the work in scope — e.g., "the work needed to retire the legacy server platform" or "the major workstreams to get to Cloud POS MMP"]. Used to size scope, surface gaps, and stage a phasing pass — not a delivery plan.

## Problem & goal

- **Problem:** [One sentence — the thing this body of work exists to solve]
- **Goal:** [One sentence — the outcome that signals "done enough"]

## Assumptions

- **Start date:** [YYYY-MM-DD]. [State anything assumed-complete before day 1 — e.g., "Infrastructure is assumed complete before day 1 — not shown as a Gantt bar. Detail retained in the [Section name] section below for reference."]
- **Resourcing (confirmed):**
  - **[Owner short name]** ([Full name], [Role]) — [pace: e.g. "full-time" / "2 days per week (~0.4 FTE)" / "full-time on her piece only"]. [One-line workstream summary — what they own end-to-end, what order, why this sequence.]
  - [Repeat per owner. If an owner runs the critical path, say so explicitly.]
  - [For part-time owners, state the calendar-duration multiplier — e.g. "Calendar duration is 2.5× the full-time estimate (a 2W effort task takes him 5 calendar weeks)."]
- [State the methodology floor — e.g. "No BMAD, no testing — floor estimate, not the optimistic case."]
- Effort in the workstream tables below is **full-time effort** (W / M). Owner-by-owner calendar duration in the Gantt reflects each person's actual availability.
- **Real dependencies that matter:** [Bullet the few cross-workstream dependencies that drive sequencing — e.g. "infrastructure before all data work, SIMS Liquor file SPIKE before direct ingestions". Keep this short — only the dependencies that actually change the order.]
- [Any other framing assumption — e.g. "'0 days' applications are POS systems that need no migration work to keep running" or "Board back-port is the immediate driver (at least September 2026) — sequencing favours infrastructure and SIMS first."]

## Gantt (one chart per person, shared date axis)

Critical path = **[Owner short name]**, starting [YYYY-MM-DD]. [State anything assumed-complete and not shown.] [Other owners] run in parallel; [state whether they extend the serial timeline]. [Note any visual conventions — e.g. "The N direct ingestions are collapsed into a single grouped bar to keep the charts readable — the per-task breakdown lives in the workstream tables below."]

All charts share the same date axis ([Month YYYY] – [Month YYYY]), so months line up vertically between them. Each chart includes a Reference section with a "Project end" milestone at [YYYY-MM-DD] (and the first chart also has a "Project start" milestone at [YYYY-MM-DD]) to anchor the axes to the same range.

### [Owner short name] ([pace label]) — [optional: critical path]

```mermaid
%%{init: {'gantt': {'barHeight': 32, 'barGap': 6, 'fontSize': 14, 'sectionFontSize': 16, 'leftPadding': 320, 'topPadding': 50, 'gridLineStartPadding': 40, 'useMaxWidth': false}}}%%
gantt
    title [Owner short name] ([pace label])
    dateFormat YYYY-MM-DD
    axisFormat %b %y
    tickInterval 1month
    excludes weekends

    section [Owner short name] tasks
    [Task name] ([effort])                    :tag1, YYYY-MM-DD, [duration]
    [Task name] ([effort])                    :tag2, YYYY-MM-DD, [duration]

    section Reference
    Project start              :milestone, YYYY-MM-DD, 0d
    Project end                :milestone, YYYY-MM-DD, 0d
```

[Repeat one Gantt block per owner. Include the `Project start` milestone only on the chart for the owner who starts earliest; include `Project end` on every chart so axes align.]

> **Sequence:** [One paragraph — the narrative of who hands what to whom, where idle windows exist, and why. State explicitly any residual gaps that could only be closed by reallocating work between owners.]

> **SPIKEs:** [List any items flagged as SPIKE — confirm scope before committing to the durations shown.]
> **TBDs:** [List anything explicitly out of scope or pending — e.g. "Integration API for promotions is out of scope. Infrastructure is assumed complete pre-day-1 (not on the chart)."]

## Roll-up

| Workstream | Owner | Rough effort | Notes |
|---|---|---|---|
| [Workstream name] | [Owner short name or "—" if pre-assumed] | [~XM or XW] | [One-line note — what it is, what gates it, why it sits where it does] |
| [Workstream name] | [Owner short name] | [~XM or XW] | [Note] |
| **Project total** | — | **~XM** | [Total calendar window, what drives the start, what drives the end, what residual idle remains] |

## [Workstream A — e.g. "Infrastructure" or "SIMS data — Supplier Information Management"]

[Optional 1-line description of what this workstream contains.]

| Feature | Sub-items | Effort |
|---|---|---|
| [Feature name] | [Sub-items, comma-separated] | [XW or XM, mark SPIKE / TBD if applicable] |
| [Feature name] | — | [XW or XM] |

## [Workstream B]

| Feature | Sub-items | Effort |
|---|---|---|
| [Feature name] | [Sub-items] | [Effort] |

[Repeat one table per workstream. Workstream sections are flat — no nesting. Order them by the sequence in the Gantt.]

## [Items requiring no migration work — optional]

[Use this section for assets that remain in scope but require no build effort — e.g. legacy POS systems that keep running, third-party integrations that just need a connection check. List so they aren't forgotten.]

| System | Effort |
|---|---|
| [System name] | 0 days |
| [System name] | [If a small connection-check task is needed, state it here] |

## [Cross-cutting concern — e.g. legacy export, migration tooling, account portal — optional]

> [Optional clarifying note — e.g. "Named 'cloud' but not actually a cloud product — exports to the venue."]

| Feature | Sub-items | Effort |
|---|---|---|
| [Feature name] | [Owner / dependency note] | [Effort] |

## Parking lot

[Things explicitly deferred. Bulleted, one-liners. No effort estimates — these are not in scope.]

- [Deferred item]
- [Deferred item]

## Other context

[Bullets capturing the nuance that explains the sequence — not in the Gantt, but a reader needs to know. Examples:]

- **[Risk / dependency label]:** [What it is, when it lands, what it depends on, what to flag for review.]
- **[Resourcing assumption label]:** [Something about an owner's working pattern that affects the calendar — e.g. "Mark M's 2 days/week assumed to fall on consistent fixed days (e.g. Mon-Tue) so each calendar-week block runs continuously rather than fragmenting. Confirm before locking dates."]
- **[Sequencing trade-off label]:** [Where idle time was deliberately filled, what the residual gap is, what could close it.]
- **[Out-of-scope-but-needed label]:** [Something not yet sequenced that probably needs to be — flag for the next planning pass.]

## Open questions / TBD

- [Open question — call out the SPIKEs that need confirming before commitment]
- [Open question — call out the TBD placeholders that need proper sizing]
- [Open question — call out the cross-team decisions still pending]
- [Phasing/MMP not yet defined — needs a prioritisation pass against [the next external driver, e.g. the September 2026 board back-port deadline]]
````

---

## Notes for filling out the template

**Be honest about effort.** This is a sizing artefact, not a commitment. Use W and M and round generously. If something is a SPIKE, mark it `(SPIKE)`. If something is `(TBD)`, leave the placeholder and add it to the Open questions section.

**One owner per task.** Every Gantt bar, every roll-up row, every workstream-table row resolves to exactly one named owner (or `—` for pre-assumed work that has no owner because it's already complete). Never list joint owners.

**Calendar duration ≠ effort.** Effort is full-time-equivalent (W / M). Calendar duration is what actually appears on each owner's Gantt bar and reflects that owner's availability. State the multiplier explicitly for part-time owners in the Assumptions section.

**Critical path is a person, not a workstream.** Identify the owner who is on the critical path and say so in plain English. The sequence narrative below the Gantts should explain where idle windows exist and why other workstreams were pulled forward to fill them.

**Workstream sections are flat.** No nesting, no sub-tables. If a workstream has internal structure, capture it in the Sub-items column.

**SPIKE and TBD are not the same.** A SPIKE has a placeholder duration but the work is in scope. A TBD has no duration because the work hasn't been scoped at all. Both belong in the Open questions section.

**Update the "Last updated" date on every edit.** Roadmap scratchpads decay fast — a stale scratchpad is worse than no scratchpad.
