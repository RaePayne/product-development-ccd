# HI Conformance Profile Upgrade

> **Brand:** Corum Health Services (CCD)
> **Last updated:** 2026-10-30
> **Owner:** Raelene Payne
> **Status:** Draft

## Summary

The Agency has announced that HI conformance profiles 1.4 to 4.0 sunset on 30 June 2027. The HI Service Conformance Register lists Corum Clear Dispense version 8.2 (system type CIS) under HI conformance profile 4.0, so CCD loses the right to connect to the HI Service on that date unless it is re-conformed on a later profile. Without HI Service access, CCD cannot validate IHIs, HPI-Is or HPI-Os, which affects eRx/ASL dispensing workflows for every pharmacy using it.

The Agency flagged this in a 28 October 2026 letter about LOTS 3.7 (a separate product, being handled separately). That letter also sets the planning constraints: conformance test bookings close about three months before the sunset (around the end of March 2027), and rollout of the new version must be complete before 30 June 2027.

The solution is to upgrade CCD's HI Service integration to a current HI conformance profile, pass Agency conformance testing, and release the conformant version to all pharmacies in time. Pharmacies benefit by keeping uninterrupted HI-dependent dispensing.

---

## Scope

**In scope:**
- Identify the target HI conformance profile and its requirements with the Agency
- Gap analysis of CCD's current HI Service integration (IHI validation/search, HPI-I and HPI-O validation/search) against the target profile
- Changes needed to meet the target profile, and Agency conformance testing and registration of the new CCD version
- Release and rollout of the conformant version to all pharmacies before 30 June 2027

**Out of scope:**
- LOTS 3.7 reply to the Agency (separate product, due 25 November 2026)
- RPM conformance
- New HI-related features beyond what the target profile requires

---

## Works With Existing Product

CCD already integrates with the HI Service for IHI, HPI-I and HPI-O validation and search (for example `ValidateScriptHI`, the e-prescribing manager and proxy in the CCD codebase). This work modifies that existing integration only where the target profile requires; no new screens are expected.

Existing behaviour that must be preserved: current validation outcomes on scripts, patient and prescriber workflows, and HPI-O set-up for the pharmacy. Any user-visible change a profile requirement forces is to be captured as a use case once the gap analysis is done.

Ticket-level implementation detail belongs in the CCD codebase repo, not here.

---

## Assumptions

1. **Version 8.2 is the version on the register** — The register row shows 8.2 / profile 4.0; confirmed by Rae as the only CCD version listed. `Status: Validated`
2. **Profile 4.0 is the only CCD registration affected** — No other CCD versions or profiles are listed. `Status: Validated`
3. **No post-sunset grace period** — The Agency's wording states a hard sunset; none has been announced. `Status: Unvalidated`
4. **Test booking cut-off is about end of March 2027** — Derived from "approximately three months before" 30 June 2027; the exact date is to be confirmed with the Agency. `Status: Unvalidated`

---

## Use Cases

### Conformance

#### UC-HIC-001: Pharmacies keep HI Service access after the profile sunset

`Status: New`

**As a** pharmacist using CCD, **I want** CCD to remain conformant with the HI Service after 30 June 2027 **so that** I can keep validating IHIs, HPI-Is and HPI-Os when dispensing.

**Acceptance Criteria:**
- A CCD version conformant to the target HI conformance profile appears on the HI Service Conformance Register before 30 June 2027
- That version is released to, and running at, all pharmacies before 30 June 2027
- IHI, HPI-I and HPI-O validation and search behave as before, except where the target profile requires a change
- Pharmacies still on an unconformant version before the sunset are identified and contacted

**Decisions:**
- **Which profile do we target?** — [To be defined] with the Agency. *Why:* The newest profile minimises repeat work, but must be confirmed against what the Agency currently accepts for new testing.
- **Which version carries the change?** — CCD 9.3. *Why:* The updated profile requires a new CCD version; 9.3 proposed by Rae (to be confirmed against the release schedule).

**Notes:** Timeline (working backwards): gap analysis by end November 2026; build December 2026 to February 2027; book conformance testing before the cut-off (about end March 2027); release and rollout by June 2027.

---

## Wireframe

Not applicable at this stage: no screens are expected to change. If the gap analysis finds a user-visible change, add a use case and a wireframe at that point.

---

## Open Questions

- [ ] Which HI conformance profile is the target, and what are its requirements? (Rae / Agency)
- [ ] Which CCD versions are deployed at pharmacies, and how will they be moved to 9.3? (Rae / engineering)
- [ ] What is the exact conformance test booking cut-off date? (Agency)
- [ ] Does the Agency offer any extension for systems with a conformant version in testing at the sunset date? (Agency)
- [ ] Who in engineering owns the gap analysis, and what is the effort estimate? (Rae / engineering)

---

## References

- Agency letter to Raelene Payne, 28 October 2026, "Request for information - inactive versions of a HI conformant system" (Outlook)
- [HI Service Conformance Register](https://implementer.digitalhealth.gov.au/system/files/documents/hi-service-conformance-register.pdf) — entry: Corum Clear Dispense, Corum Health Pty Ltd, 8.2, CIS, profile 4.0
- [CCD terminology dictionary](../terminology-dictionary/ccd-terms.md)
