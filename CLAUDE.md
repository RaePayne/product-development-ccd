# Corum Health Services (CCD) — Product Development

This repo holds product-management documentation for **CCD** (Corum Clear Dispense) — one of Corum Health Services' products (alongside LOTS and RPM, each of which has its own separate product-development repo, its own repo-root docs, and its own distinct visual identity). PRDs, FRDs, design specs, go-to-market material, and CCD-scoped strategy all live here. It does **not** hold code or dev-cycle artifacts — see [Boundary with the CCD Codebase](#boundary-with-the-ccd-codebase-do-not-mix-these-up) below.

Everything in this repo is scoped to CCD, so there is no product-folder layer inside it — projects sit directly at the repo root. The one exception is `design-system/brand.md`, which is intentionally company-wide (it covers Corum's identity and full product suite, not just CCD) — currently duplicated between the LOTS and CCD repos rather than centralised; see the Known Gap in `README.md`.

## Repo Structure

```
product-development-ccd/
├── CLAUDE.md                        ← You are here
├── design-system/
│   └── brand.md                     ← Company-wide brand identity, positioning, and visual identity — covers LOTS, CCD, and RPM together
│   └── product-design-overview.md   ← [Not yet created] CCD-specific full UI map
│   └── design-system.md             ← [Not yet created] CCD-specific component-level visual rulebook — see writing-standards/design-system-template.md
├── strategy/                        ← CCD-scoped strategy docs
│   └── ccd-team.md                  ← Owner short-name → full name/role mapping, used by the roadmap scratchpad
├── terminology-dictionary/
│   └── ccd-terms.md                 ← Read before writing any document
├── writing-standards/                ← Templates — read the matching one before writing any doc
│   ├── prd-template.md
│   ├── frd-template.md
│   ├── quick-spec-template.md
│   ├── business-case-template.md
│   ├── strategy-on-a-page-template.md
│   ├── roadmap-scratchpad-template.md
│   ├── design-system-template.md
│   ├── gtm-brief-template.md
│   └── gtm-plan-template.md
└── project-[name]/                   ← One folder per project. Subfolders below are created only when that stage is actually reached — don't scaffold empty ones ahead of time.
    ├── product-brief/                ← Early-stage discovery/evaluation, before a PRD exists (optional)
    ├── prd/
    ├── frd/
    ├── design/
    │   └── explorations/              ← Low-fi wireframes, required before any HTML prototype
    ├── architecture/
    └── gtm/
        ├── [project]-gtm-brief.md
        ├── [project]-gtm-plan.md
        └── screenshots/
```

**Current projects:** none yet.

## Document Pipeline

Documents build on each other — later ones reference earlier ones, never duplicate:

```
Product Brief (optional) → PRD → FRD → Design Spec → Wireframe → Design HTML → Architecture → GTM Brief → GTM Plan → Launch Plan
```

| Stage | Template | Notes |
|---|---|---|
| Product Brief | — (freeform) | Early discovery/evaluation before a build decision. Use when the question is "should we do this at all," not "how do we build it." |
| Quick Spec | `writing-standards/quick-spec-template.md` | For small-to-medium features (1-5 stories) that don't need the full pipeline below — captures problem, solution, and use cases in one doc |
| PRD | `writing-standards/prd-template.md` | What & why |
| FRD | `writing-standards/frd-template.md` | Business rules & how |
| Design Spec / Wireframe / HTML | *(none yet)* | UI requirements → low-fi layout → clickable prototype. Wireframe always before prototype. |
| Architecture | *(none yet)* | Technical design |
| GTM Brief | `writing-standards/gtm-brief-template.md` | Short PM → marketing handoff |
| GTM Plan | `writing-standards/gtm-plan-template.md` | Full strategic go-to-market plan |
| Launch Plan | — (no template, marketing-owned) | Externally-facing activation plan |

For most Corum work — small, targeted fixes and features — a Quick Spec is enough; reserve the full PRD → FRD → Design → Architecture pipeline for larger, multi-flow features.

Two templates also exist for larger strategic work: `writing-standards/business-case-template.md` and `writing-standards/strategy-on-a-page-template.md`, both living under `strategy/` when used. A third, `writing-standards/roadmap-scratchpad-template.md`, gives a lightweight cross-workstream sizing view — it depends on `strategy/ccd-team.md` for owner names.

## Naming Conventions

- Project folders: `project-[name]/`, lowercase kebab-case
- PRD: `prd/prd-[project-name].md`
- FRD: `frd/frd-[project-name].md`
- GTM brief: `gtm/[project-name]-gtm-brief.md`
- GTM plan: `gtm/[project-name]-gtm-plan.md`
- Design HTML: `design/design-preview-[name].html`

## Boundary with the CCD Codebase — do not mix these up

The **CCD codebase** (a separate repo — `CorumClear CCD Repo` locally, cloned from Azure DevOps as `Corum Dispense/Dispense`, a .NET solution — `Dispense.sln`) is where actual dev-cycle work happens: ticket-driven PRDs for code changes, implementation-readiness reports, sprint-change-proposals, story files, investigations. If a BMAD workflow is run from that repo's context, its own `_bmad-output/` is the authoritative home for that output — not here.

This repo (`product-development-ccd`) is for product-management-level thinking: should we build something, what should it do for the business, how do we position and launch it. If a document is scoped to a specific ticket, a specific source file, or a release branch, it belongs in the CCD codebase repo, not here.

## General Rules

- Read `terminology-dictionary/ccd-terms.md` before writing any document. Use only the terms defined there — if a document needs a term that isn't listed, add it with a definition before using it
- Check for a template in `writing-standards/` before creating any new document type
- Keep docs concise — use "[To be defined]" placeholders rather than generic filler for sections not yet relevant
- Never duplicate content between docs — link to the source instead
- Full CRUD on every "Create" design — never spec a create-only flow
- Screenshots used as design input are directional only — extract intent, don't replicate exactly
- Australian English throughout
