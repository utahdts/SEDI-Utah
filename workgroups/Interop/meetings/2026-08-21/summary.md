# SEDI Interop Working Group — Summary
**Date:** 2026-08-21

---

## Attendees


---

## Discussion

### SEDI Summit Demo Scope

- Demo: simple use cases, including delegation
- Audience will be primarily legislators; keep the technical focus high-level instead of granular
- Planned demos include age gating, parent/child delegation; may have a "demo alley" format on day 2

### GitHub Repository

- https://github.com/utahdts/SEDI-Utah
- Enabled GitHub discussions
- All discussions are public record
    - Concern raised about trolling/hijacking - decided to proceed. Same risks exist in PRs and issues regardless.

### External Contribution

[LinkedIn article](https://www.linkedin.com/pulse/utahs-sedi-connecting-other-credential-systems-steven-mccown-e34nc) on the DID web method for interfacing with credential systems was shared.

### Guardianship Use Case Workshop

- Utah Senate Bill 142 (2025) adopted as the foundational use case for the guardianship design workshop.

**Personas established:**
- Aging grandparent (has device access but lacks capacity to manage keys or make decisions)
- Digitally native parent
- Teenager (may assume control under parental authorization constraints)

**Key distinctions:**
- Young children: parent manages keys/identifiers entirely
- Teenagers: may hold their own identifier with parental authorization constraints
- At age 18: state facilitates transfer of reputation/accounts to new identifier (emancipation process)

**Requirements surfaced:**
- Two distinct identities required: guardian and ward
- Architecture must verify a legally enforceable relationship between guardian and ward (prevent unauthorized parties acting as guardians)
- Authorization scopes — e.g., social media limited to 7–10pm; "guardian rules" vs. "ward rules" distinction
- Must handle complex custody situations (e.g., divorce, custody schedules)
- Financial delegation (e.g., managing game accounts)
- Component categorization: identity proofing, attribute proofing, establishing "edges" (relationships) between identities
- State acts as issuer endorsing guardian and ward roles

**Revocability and updatability (all credentials must support both):**
- Extending curfew, revoking access for behavioral issues, mass revocation in custody disputes
- "Reversion of control" mechanism: transfer credential to new controller rather than relying solely on a revocation registry

- Have Data Privacy Officer join next week to dive into the policy side

### Closing
- DID web interoperability with other systems is unresolved — guardianship discussion didn't address it; flagged for future sessions
- Unanimous consensus on core problem definitions validated current approach
- Next week: begin "bits and bytes" of technical implementation while staying tethered to project goals
- Framing: the group has defined the "treasure chest" — now need to build the "pirate map"

---

## Decisions

- **SEDI conference demonstration scope:** High-level only; no specific technical interop requirements for the summit demo.
- **GitHub discussions enabled:** All content on the SEDI program repository is public record.
- **Senate Bill 142 (2025)** adopted as the foundational use case for the guardianship design workshop.

---

## Action Items

| Item  | Due |
|------|-----|
| Move whimsical diagram from Spruce ID org to a location supporting group collaboration | |
| Refine AI-generated guardianship requirements into a mature design version | |
| Document requirements for component updatability and replaceability | |

---

## Next Meeting

**Topics:** Continue guardianship model; involve policy experts (Lana) to align technical design with SB 142; begin addressing DID web interoperability
