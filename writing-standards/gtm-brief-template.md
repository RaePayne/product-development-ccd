> **Brand:** All
> **Last updated:** 2026-04-24
> **Owner:** Matthew Sluggett
> **Status:** Draft

# GTM Brief Template

> **Purpose:** A lightweight, product-side handoff to the marketing team covering what's launching, who it's for, how to position it, and the visual references that support it. The GTM brief is an **input** to the full GTM plan — not a substitute for it.
>
> The brief is written by the PM once the PRD, FRD, design, and architecture are complete. It gives marketing everything they need to build the GTM plan, campaign, sales enablement, and customer-facing assets.
>
> **GTM Brief vs. GTM Plan:**
> - **Brief** (this template) — what/who/why/positioning/visuals, written by the PM, short and scannable. Typically 1–3 pages of content.
> - **Plan** (`gtm-plan-template.md`) — pricing, channels, launch phases, migration, sales enablement, metrics, risks, written by marketing, detailed and operational.

---

## At a Glance

| Field | Detail |
|---|---|
| **Module / feature name** | [Name of what's launching] |
| **Launching into** | [Product or portal it sits inside] |
| **Primary customer** | [Who buys or uses it] |
| **Target launch window** | [Date, quarter, or "To be confirmed with marketing"] |
| **One-line pitch** | [One sentence: what it is, who it's for, why they should care] |

---

## What We're Launching

[2–3 paragraphs describing what's being launched, the major capability areas in plain language, and how it connects to the broader product. Reference the PRD for full detail — don't duplicate it here.]

[If the launch bundles several distinct capability areas, list them as a short numbered list so marketing can scan them quickly.]

---

## Who It's For

| Persona | Role | What They Use It For |
|---|---|---|
| **[Persona name]** (optional: individual name from persona file) | [Their role / seniority] | [The jobs they'll do with this product] |
| | | |
| | | |

**Primary decision-maker for purchase:** [Title of the person who signs].
**Primary champion:** [The persona who advocates internally].

---

## The Problem We're Solving

| Pain Point | Why It Matters |
|---|---|
| [Specific pain the customer feels today] | [Business consequence of that pain] |
| | |
| | |

---

## Key Capabilities & Customer Benefit

| Capability | Benefit |
|---|---|
| [Capability — one line, plain English] | [What the customer actually gets from it] |
| | |
| | |

---

## Positioning

**Positioning statement (draft — for marketing to refine):**

> For [target customer] who [need / context], [product name] is the [category] that [key benefit]. Unlike [alternative], [differentiator].

**Tone:** [2–3 words describing the voice — e.g. confident, specialist, commercially fluent. Note any brand-guideline-mandated angles such as "proprietary in-house AI, not third-party AI".]

### Core Messages by Persona

| Persona | Core Message | Supporting Points |
|---|---|---|
| [Persona] | "[The one thing this persona cares about most, in their voice]" | [2–3 supporting reasons] |
| | | |
| | | |

---

## Screenshots

Visual previews of each page or major screen in the module, captured from the design prototypes. Use these as reference for marketing assets, website copy, sales decks, and demo walk-throughs.

> **How to generate:** Use a headless browser (e.g. Playwright) to capture full-page PNGs of each HTML prototype at 1440×900, 2× scale. Save under `gtm/screenshots/` with filenames matching the source HTML (e.g. `products.html` → `products.png`).

### [Screen name]
![[Descriptive alt text]](screenshots/[screen-name].png)

### [Screen name]
![[Descriptive alt text]](screenshots/[screen-name].png)

[Repeat for each key screen — order by how a user would encounter them in the product, or by marketing priority.]

---

## References

- [PRD — link](../prd/prd-[project-name].md)
- [FRD — link](../frd/frd-[project-name].md)
- [Design spec — link](../design/design-spec.md)
- [Persona — link](../../../customer-research/personas/persona-[name].md)
- [Brand guidelines](../../../design-system/brand.md)
- [GTM plan — link, once created](./[project-name]-gtm-plan.md)
