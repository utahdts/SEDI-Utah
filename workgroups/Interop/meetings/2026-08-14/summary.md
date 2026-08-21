# SEDI Interop Working Group — Summary
**Date:** 2026-08-14

---

## Attendees


---

## Discussion

### Consortium Timeline

The August 31 deadline is approaching. The National Governors Association requested a two-week extension due to end-of-August government office closures during the congressional recess. Holding the deadline could yield participation from all 50 states. 

### Policy Alignment

The Full Faith and Credit Clause has generated significant interest among participants. Non-mDL states are beginning to align around this as a policy framework.

### KERI Conference 2026 Resources

Videos and presentations from KERI Conference 2026 are available, including a session on bridging KERI to the DID world. Slides are to be shared with the group.

- [Videos](https://keri.foundation/confs/2026/videos/#keri-bridge-to-the-did-world-jonathan-rayback)
- [KERI Bridge to the DID World — Jonathan Rayback (PDF)](https://keri.foundation/confs/2026/videos/KERICONF26/presentations/Jonathan%20Rayback%20%EF%BD%9C%20KERI%20Bridge%20to%20the%20DID%20World%20%EF%BD%9C%20KERI%20Conference%202026.pdf)

### Technology Risk Discussion: KERI/ACDC

A substantive debate took place on the maturity and readiness of the KERI/ACDC stack.

**Concerns raised:**
- The technology is theoretically strong but untested at scale
- Gaps exist between architectural design and real-world communication/implementation; those gaps are not yet fully mapped
- Individual ideas within KERI (e.g., pre-rotation of keys) are well-regarded, but the framework as a whole is rigid and has not been stress-tested in production environments
- Cryptographic problems historically reduce to key management — and key management is where unknowns concentrate

**Arguments in favor:**
- Key theft detection within a standard is a meaningful differentiator; existing approaches (including OAuth) have well-documented key management vulnerabilities
- did:webs benefits from alignment with W3C verifiable credentials and their adoption volume
- Most implementation challenges are foreseeable, not unknown — they require time investment, not fundamental rework
- Post-quantum requirements are likely to create significant problems for other architectural approaches; KERI's design is better positioned

**General tone:** Broad support for the SEDI direction, alongside honest acknowledgment that known implementation work remains. One participant characterized Utah's approach as a "moonshot" — bringing all relevant parties to the table.

### W3C and mDL Influence

The group discussed whether SEDI could meaningfully influence W3C or mDL standards. One view is that influence is unlikely on a timely basis; another is that it depends on the nature of the proposed changes. No conclusion reached.

### Industry Posture

A major identity verification vendor noted they have not yet adopted either the KERI/ACDC or mDL standard, reflecting the broader market's wait-and-see stance.

### Documentation and GitHub Access

GitHub access and documentation sharing for the interop group was raised as an open item. Resolved as of 2026-08-18.

---

## Decisions

- Next session will be structured around a specific real-world use case to ground technical discussions in concrete functionality requirements by component.

---

## Action Items

| Item | Owner | Due |
|------|-------|-----|
| Share KERI Conference 2026 slides with group | Sam | ASAP |
| Identify and prepare real-world use case for next session | Group | Next meeting |

---

## Next Meeting

**Topics:** Work through a specific real-world use case; identify functionality requirements by component
