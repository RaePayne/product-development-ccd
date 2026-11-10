# Corum Health Services (CCD) — Product Development

This repository is the source of truth for **CCD** (Corum Clear Dispense) product documentation: PRDs, FRDs, design specs, go-to-market material, and CCD-scoped strategy. Corum's other products, LOTS and RPM, each have their own separate product-development repo — this one does not cover them.

It does **not** contain code. CCD's codebase lives in a separate repo (`CorumClear CCD Repo` locally, cloned from Azure DevOps — `Corum Dispense/Dispense`) — see [Boundary with the CCD Codebase](CLAUDE.md#boundary-with-the-ccd-codebase-do-not-mix-these-up) in `CLAUDE.md` for where the line sits.

## Using This Repo with Claude Code

Open this folder in Claude Code. The BMAD skills referenced below (`bmad-product-brief`, `bmad-create-prd`, etc.) are available globally — no local install is needed in this repo.

For the full set of rules — folder structure, document pipeline, naming conventions, and the codebase boundary — read [CLAUDE.md](CLAUDE.md). This README is just the quick orientation.

### Typical workflow for a new project

| Stage | Skill / command | What it produces |
|---|---|---|
| Discovery | `bmad-product-brief` | An early evaluation before committing to a build |
| Small feature | `bmad-quick-dev` or a manually written quick spec | `writing-standards/quick-spec-template.md` |
| Larger feature | `bmad-create-prd` → `bmad-prd` | `prd/prd-[project-name].md`, following `writing-standards/prd-template.md` |
| "What do I do next?" | `bmad-help` | Recommends the next step based on what already exists |

## Repository Structure

```
product-development-ccd/
├── CLAUDE.md                    ← Full rulebook — read this before writing any doc
├── README.md                    ← This file
├── design-system/               ← brand.md (company-wide identity — covers LOTS/RPM too)
├── strategy/                    ← CCD-scoped strategy docs + ccd-team.md (owner names)
├── terminology-dictionary/      ← ccd-terms.md — read before writing any document
├── writing-standards/           ← Templates — read the matching one before creating a new doc type
└── project-[name]/               ← One folder per project (product-brief/, prd/, frd/, design/, architecture/, gtm/ as needed)
```

## Current Projects

[eRx API Integration (CPR-61)](project-erx-api-integration/).
[CPR-98](project-cpr-98/).

## Known Gaps (as of 2026-09-23)

- No `product-design-overview.md` or `design-system.md` yet — nothing has reached the UI/prototype stage.
- `terminology-dictionary/ccd-terms.md` is entirely placeholders — fill in definitions as terms come up in real work.
- `design-system/brand.md` is duplicated across all three product repos (`product-development-corum`, `product-development-ccd`, `product-development-rpm`) rather than centralised. Same open question as noted in the others: worth deciding whether it should live somewhere shared and be referenced instead of copy-pasted. If it's ever edited, remember to update every copy until that's resolved.
