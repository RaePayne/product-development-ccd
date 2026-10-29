> **Brand:** Corum Health Services (CCD)
> **Last updated:** 2026-09-23
> **Owner:** Raelene Payne
> **Status:** Draft

# CCD Terminology Dictionary

Terms specific to Corum Clear Dispense (CCD) and the pharmacy domain. Read this file before writing any document in this repo.

**Rules:**
- Use only the terms defined here — never a synonym or alternate phrasing for a defined term
- If a document needs a term that isn't listed, add it here with a definition before using it elsewhere

---

## Product & Deployment

| Term | Definition |
|------|------------|
| **CCD** | [To be defined — Corum Clear Dispense] |
| **Corum Clear Dispense** | [To be defined] |

## Pharmacy Workflow

| Term | Definition |
|------|------------|
| **Facility** | A residential care site (for example an aged-care home) that the pharmacy dispenses medication for. Created under the Medication Institution details in CCD. |
| **Ward** | A named subdivision of a Facility (for example a wing or unit) that patients are assigned to. Not currently supported in CCD; requested by BESTMED (October 2026). |
| **Ward code** | A short identifier for a Ward, unique within its Facility, used by integrated systems to map and sync wards. |
| **[Term]** | [To be defined] |

## Integrations & Vendors

| Term | Definition |
|------|------------|
| **eRx API** | The external eRx service/API referenced by CPR-61. The provider, API product, and exact meaning of “eRx” are [To be defined] from the ticket or service documentation. |
| **BESTMED** | Corum's integration partner whose medication-management system connects to CCD through the LOTS_MMS interface database. |
| **LOTS_MMS** | The interface database through which integrated systems such as BESTMED read facility, ward and patient data from the dispense system. |
| **YourRef** | The identifier a row in the LOTS_MMS interface carries for the matching record in the dispense system (for example a ward or patient). Unique within one pharmacy, not across pharmacies. |
| **[Term]** | [To be defined] |
