# Ward and Ward Code

> **Brand:** Corum Health Services (CCD)
> **Last updated:** 2026-10-30
> **Owner:** Raelene Payne
> **Status:** Draft

## Summary

BESTMED is building a connector between its medication-management system and CCD, and the connector is nearly complete. It is now blocked from testing because CCD has no concept of a Ward: Facilities can be created under the Medication Institution details, but there is nowhere to define Wards or assign patients to them (confirmed by Alex Moiseenko, 29 October 2026). BESTMED uses Ward and Ward code throughout its product — mapping and syncing, packing, and what staff see in the Facility — and in LOTS and every other dispense integration the Ward comes from the dispense system, so BESTMED cannot readily work around it. A mutual customer cannot go live until this is resolved.

This feature adds Wards to CCD: Wards within each Facility (each with a name and a Ward code), a Ward assignment on each patient, and Ward and Ward code exposed through LOTS_MMS, including when a patient moves Ward. It follows LOTS behaviour where possible so BESTMED can reuse its existing connector logic.

**Who benefits:** BESTMED (unblocks connector testing and go-live for the shared customer) and the pharmacy staff at that customer, who see consistent Ward information across both systems.

---

## Scope

**In scope:**
- Create, view, edit and delete Wards within a Facility, each with a Ward name and a Ward code
- Assign a patient to a Ward, and move a patient from one Ward to another
- Expose Ward and Ward code for each patient and each Ward through LOTS_MMS, including updates when a patient moves Ward or a Ward is edited or deleted

**Out of scope:**
- Using Wards to change CCD packing, labelling, reporting or other dispensing behaviour — the request is for data and interface parity; any CCD-side use of Ward is a later decision
- Migrating or back-filling Ward data for existing patients — Wards are entered after release (see Open Questions)
- Changes to how LOTS handles Wards — LOTS is the reference, not a change target
- Other integration partners — only the BESTMED use case is validated

---

## Works With Existing Product

**What already exists.** CCD supports creating Facilities under the Medication Institution details; there is no Ward concept (no Ward entity, no patient Ward assignment). The LOTS_MMS interface database already carries a Wards table (`YourRef`, `FacilityRef`, `IsDeleted`, `RowVersion`, `LastUpdated`, `WardRoomNumber`) and a `WardRef` on each patient that cross-references a Ward's `YourRef`, so the interface shape for linking a patient to a Ward and a Ward to a Facility is already defined. Source: `LOTS_MMS_CreateDB.sql` in the CCD codebase.

**What changes.** The Facility details gain a Wards section for managing Wards. The patient record gains a Ward field limited to the Wards of the patient's Facility. CCD populates the LOTS_MMS Wards table and each patient's `WardRef`, and LOTS_MMS must additionally carry the Ward name and Ward code, which the existing Wards table does not (see Open Questions).

**What stays the same.** Existing Facility creation, patients without a Ward, and all current LOTS_MMS columns and consumers must keep working unchanged. A patient with no Ward must continue to be valid.

---

## Assumptions

1. **LOTS parity is the target** — BESTMED's connector reads Ward the same way it does for LOTS, so matching LOTS field semantics lets BESTMED reuse its logic. `Status: Unvalidated`
2. **Ward code is unique within a Facility** — the code is how BESTMED maps and syncs Wards, so duplicates within one Facility would cause mis-mapping. Uniqueness across Facilities is not required. `Status: Unvalidated`
3. **A patient belongs to at most one Ward at a time, and that Ward belongs to the patient's Facility** — consistent with the LOTS_MMS Patients view, which derives the Facility from the Ward. `Status: Unvalidated`
4. **Ward is optional on a patient** — existing patients and non-Facility patients have no Ward. `Status: Unvalidated`
5. **Deleted Wards are retained as soft-deleted rows in LOTS_MMS** — the existing `IsDeleted` column says an obsolete Ward is flagged, not removed, so consumers can see the change. `Status: Unvalidated`

---

## Use Cases

### Ward Management

#### UC-WRD-001: Manage Wards within a Facility

`Status: New`

**As a** pharmacy staff member administering a Facility, **I want to** create, view, edit and delete Wards, each with a Ward name and Ward code, **so that** the Facility's Wards are defined in CCD and can be used by integrated systems.

**Acceptance Criteria:**
- The Facility details show a Wards list for that Facility: Ward name, Ward code, and number of patients assigned
- I can add a Ward by entering a Ward name and a Ward code; both are required
- Ward code must be unique within the Facility; a duplicate shows the error "Ward code [code] is already used in this Facility" and nothing is saved
- I can edit a Ward's name and code; patients assigned to it stay assigned
- I can delete a Ward that has no patients assigned; it is flagged as deleted in LOTS_MMS (`IsDeleted`) rather than removed
- Deleting a Ward that has patients assigned is blocked with the message "[n] patients are assigned to this Ward. Move them to another Ward first."
- A Facility with no Wards shows the empty state "No Wards yet. Add a Ward to assign patients."
- Each create, edit or delete is reflected in LOTS_MMS with updated `LastUpdated` and `RowVersion`, so BESTMED's sync picks it up
- The system records who changed a Ward and when

**Decisions:**
- **Can a Ward with patients be deleted?** — No, it is blocked until the patients are moved. *Why:* Silent un-assignment would change patient data in BESTMED without anyone deciding to, and a safety-critical packing context favours an explicit step.
- **Hard delete or soft delete?** — Soft delete (`IsDeleted`). *Why:* Matches the existing LOTS_MMS design, where obsolete Wards must not be removed so integrated systems can detect the change.

**Notes:** Whether to carry the Ward code into the existing `WardRoomNumber` or `HealthStreamCode` fields, or add new columns, is an Open Question.

---

### Patient Ward Assignment

#### UC-WRD-002: Assign a patient to a Ward and expose it through LOTS_MMS

`Status: New`

**As a** pharmacy staff member, **I want to** assign a patient to a Ward and move them to another Ward when they relocate, **so that** CCD and BESTMED both show the patient's current Ward.

**Acceptance Criteria:**
- The patient record has a Ward field, enabled when the patient belongs to a Facility; the dropdown lists only that Facility's active Wards, showing Ward name and Ward code
- Ward is optional; I can save a patient with no Ward
- I can change a patient's Ward at any time; the previous Ward is replaced, not kept alongside
- On save, LOTS_MMS reflects the new Ward for that patient (`WardRef`) and the patient's `LastUpdated` and `RowVersion` change, so BESTMED sees the move
- Ward name and Ward code for the patient's Ward are available through LOTS_MMS
- If I change a patient's Facility, the Ward is cleared and I'm prompted to choose a Ward in the new Facility, because the Ward must belong to the patient's Facility
- A patient can be removed from a Ward (set to none) and LOTS_MMS reflects the cleared Ward
- If the selected Ward was deleted by another user before save, the save fails with "This Ward is no longer available. Choose another Ward."

**Decisions:**
- **What happens to the Ward when a patient changes Facility?** — It is cleared and the user is prompted to pick a new one. *Why:* A Ward only exists within one Facility; carrying it across would break the Ward-to-Facility link.
- **Is Ward history kept?** — Not in this release; only the current Ward is exposed. *Why:* BESTMED asked for updates on moves, not a history. Revisit if BESTMED needs an audit trail.

**Notes:** Depends on UC-WRD-001 for Wards to exist.

---

## Wireframe

- [Wireframe — Ward and Ward Code](quick-spec-ward-and-ward-code-wireframe.html)

Single self-contained low-fidelity HTML file covering UC-WRD-001 and UC-WRD-002.

---

## Open Questions

- [ ] **Interface shape** — The existing LOTS_MMS Wards table has no Ward name or Ward code column (it has `WardRoomNumber`, and the Quantum_Connect version has `HealthStreamCode`). Which columns does BESTMED's LOTS connector read for ward name and code, and do we add columns or reuse existing ones? Alex Moiseenko / BESTMED to confirm.
- [ ] **LOTS reference behaviour** — Confirm how LOTS handles Ward code uniqueness, deleting a Ward with patients, and Ward on a patient who changes Facility, so CCD matches. Owner: Alex Moiseenko.
- [ ] **Existing data** — Does the shared customer need Wards loaded in bulk (import) rather than entered one by one? Ask Ben Kelland.
- [ ] **Timing** — The customer's go-live date and BESTMED's required test date are unknown. Ben has proposed a meeting next week to work through scope and timing.
- [ ] **Customer** — Name of the mutual customer, for context in the Summary. Ask Ben Kelland.

---

## References

- Email thread "Corum Clear Dispense & LOTS Dispense Integrations" — Ben Kelland (BESTMED), request of 29 October 2026; Alex Moiseenko confirmation of 29 October 2026; Ben's original query of 26 October 2026
- LOTS_MMS interface schema: `Infrastructure/Installers/Corum.Installer.Database.LOTS_MMS/LOTS_MMS_CreateDB.sql` (CCD codebase)
- [CCD terminology dictionary](../terminology-dictionary/ccd-terms.md)
