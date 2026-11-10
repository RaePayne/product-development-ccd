# Corum Clear Dispense 9.5.3 — Release Notes

**Release date:** [To be defined]
**Upgrade notes:** [To be defined]

## New features

- **Ward and Ward code for BESTMED integration.** You can now set up Wards within a Facility, give each Ward a Ward code, and assign patients to a Ward. Ward details are available to BESTMED through LOTS_MMS.
- **Registered Nurse prescriber type.** Registered Nurse is now available as a PBS Prescriber Type.
- **Robot stock sync frequency.** A new pharmacy setting lets you choose how often robot stock is synchronised.

## Improvements

- **Faster recovery after a service restart.** Database compression now runs straight after the service restarts.
- **Better database performance.** Further SQL improvements, based on issues seen at pharmacies, for smoother day-to-day operation.
- **More accurate robot stock.** Stock levels now stay in step with the robot when packs are opened, orders contain multiple barcodes, items are output manually, or packs are input. Duplicate robot status requests are also avoided.

## Fixes

- **eScripts:** Virtual repeat forms now show the current patient's details instead of old ones.
- **eScripts:** Quantity now fills automatically when the prescription supplies it in the extended quantity field.
- **eRx medication charts:** Charts can now be dispensed on the day the chart or chart item is created.
- **Schedule 8 compounded items:** Dispensing is no longer allowed once the item reaches its six-month expiry.
- **Robot stock:** Products missing from the daily stock update are now set to zero robot stock.
- **SafeScript:** Fixed an internal error loop that occurred when a product had no strength.
- **Top Drug report:** The script count now shows the number of scripts actually dispensed, not the number of repeats prescribed.
- **PBS item type:** Fixed the PBS item type changing unexpectedly on dispense.
- **Early supply:** Corrected PRF values where early supply fell on the threshold.

---

<!-- INTERNAL ONLY — delete this section before publishing -->

## Internal reference (ADO work items)

| Release note | ADO item |
|---|---|
| Ward and Ward code | User Story 68216 |
| Registered Nurse prescriber type | User Story 67792 |
| Robot stock sync frequency | User Story 66943 |
| Database compression after restart | User Story 66034 |
| SQL improvements | User Story 68140 |
| Robot stock accuracy (Rowa) | Bug 68239 |
| Virtual repeat form patient details | Bug 64456 |
| Quantity from QuantityExtended | Bug 65321 |
| eRx chart same-day dispensing | Bug 68179 |
| Schedule 8 compounded expiry | Bug 66107 |
| Robot stock set to zero | Bug 66924 |
| SafeScript no strength loop | Bug 66940 |
| Top Drug report script count | Bug 66954 |
| PBS item type change | Bug 66971 |
| PRF early supply threshold | Bug 66867 |
