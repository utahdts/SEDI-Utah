# SEDI Interop Working Group — Summary
**Date:** 2026-09-11

> The personal data collected in this meeting is classified as a public record and may be made available to the public as provided by the Government Records Access and Management Act (Utah Code § [63G-2-201](https://le.utah.gov/xcode/Title63G/Chapter2/63G-2-S201.html)).

---

## Discussion

### Recap: Guardianship Framework

The group re-grounded in the guardianship model built from Utah SB 142: guardian, ward, their relationship, and separately-issuable/revocable scopes of action for each. Running examples included a digitally native parent with aging parents, a teenager with a phone, and a child without one.

This session's focus: given the guardianship model, what technology (did:webs, KERI/ACDC, etc.) can actually implement it, and what are we solving for at the identifier layer.

### Long-Lived Identifiers and Relationships

The core requirement isn't just key lineage — it's binding **issuances** to that key lineage so they're *perpetually verifiable*, which is what makes stable delegation chains (needed for guardianship) possible. DNS lacks a stable binding, so its delegation chains are fragile.

A caution was raised against framing this as a checklist of technical characteristics: the real target is **perpetual identity** as a concept, not a fixed list of technical properties — any such list will always be incomplete. Related: the group hasn't yet modeled the *relationships between* pieces of evidence (e.g., evidence about a guardian must be provably related to evidence about the ward), and the VC data model doesn't support this kind of chaining natively.

The current model was framed as a "baseline that won't survive contact with an agency" (e.g., DHS) — real-world deployment is expected to surface more requirements; the goal is to get as close to a general-purpose framework as possible now.

Guardian *status* and guardian *authorizations* must be separable and independently revocable — e.g., custody changing from joint to sole doesn't remove guardian status but does change scope. This maps to RBAC-style credentials: issuing agencies define what a guardian can/cannot do, revocable independently.

Working definition: a guardianship relationship = guardian + ward + scope of action + the authority that granted it.

### Perpetually Verifiable Relationships

Relationships/issuances need to be as long-lived as the real-world relationship they represent (e.g., a guardianship can last the ward's whole childhood), and should only become invalid through **deliberate legal/administrative action** (e.g., a divorce filing), never through incidental technical expiration (e.g., an MDL's 30-day crypto-driven expiry). Legal and human-decided status should govern relationship validity — not technical/key-management mechanics.

A related subtlety: it's not just that credentials shouldn't *expire* for technical reasons — their **trust profile** shouldn't silently degrade either. Example: an X.509 cert's initial issuance may be well-governed, but renewal via ACME/OIDC often isn't audited the same way, so trust quietly erodes across renewal cycles.

### did:webs Technical Overview

did:webs merges did:keri with did:web — it is essentially did:keri under the hood, with the ability to derive a did:web view at any point for interoperability with did:web-only systems.

- **Key event log (KEL):** provides cryptographically verifiable key history — the root of trust for everything anchored to that AID (autonomous identifier).
- **Transaction event log (TEL):** a second hash-chained log, anchored to the KEL, used to track state for things like ACDC (credential) registries — enables revocation/issuance/state-change tracking without the KEL itself needing to know the content. Comparable to blockchain rollups/side chains, but for identity state rather than currency.
- Anything anchored to a KEL (issuances, relationships, transactions) inherits its perpetual-verifiability properties — this is the piece missing from the working diagram, which currently shows only "key state."

### Privacy / Correlation

A question was raised about how KELs/TELs avoid becoming a correlation vector for holders. Three mechanisms address this:

- **Bulk issuance:** partitioned sets of identifiers/logs per context — SEDI-scale example discussed: ~100 unique AIDs per person, unique AID per set (similar in spirit to Apple/Google's ~10 signing keys per mDoc), so presentations in different contexts can't be linked. Comparable to "tokenized credentials" in the OIDC-VC world.
- **Bulk updates:** registries are updated in batches so an observer/validator can't correlate individual state changes to specific presentations, decorrelating verifier from issuer.
- **Perfect forward privacy:** because registry state updates are blinded, a past verifier can't determine current state — addressing a privacy gap most revocation-registry designs don't solve.

### Applying This to Guardianship

The TEL would hold the live state of a guardianship relationship (active, revoked, modified) and separately the state of ward permissions (e.g., social media access), each independently issued and revocable, anchored back to the same KEL for security inheritance. Relationship existence should be modeled independently of the privileges attached to it (a separate credential type). Medical/legal power of attorney was discussed as an example of a specialized "transaction class" using the same mechanism, with no state involvement required at that layer.

### Durability, Evidence, and System-of-Record Design

A question was raised about how the ecosystem manages ACDC durability/availability, since a TEL only holds *hashes* of ACDCs, not the credentials themselves. ACDCs are managed by immutable, self-describing **schemas** — each schema carries a cryptographic identifier (a "SAID," self-addressing identifier), so credential *types* are independently verifiable without a central registry. ACDCs also support **nested partial disclosure** (in addition to selective disclosure) — a Merkle-tree-like structure where sections of a credential can be represented purely by hash and expanded/disclosed later, so full credential contents don't need to be passed around.

Key framing that emerged: the KERI/ACDC design is solving for an **ideal system of record that behaves like a distributed database** — a different design goal than what MDOC, VC, or SD-JWT ecosystems set out to solve (those optimize for wallet presentation, not durable evidentiary record-keeping). This distinction — system-of-record vs. wallet-presentation format — may explain much of the historical friction between different identity communities.

The system also supports lightweight/ephemeral use (e.g., signing an HTTP API request with current key state, no durable record needed) without requiring a full system-of-record setup; did:webs offers a did:web-compatible bridge for interoperability with parties that don't use KERI at all. Perpetual identifiers mean reputation persists across key rotations "for free" — contrasted with DNS/PKI-style systems where the identifier *is* the public key, so reputation resets on every rotation.

---

## Decisions

- **System-of-record vs. presentation format:** Recognized as two distinct design goals (durable evidentiary record-keeping vs. mobile wallet presentation) — likely explains prior cross-community friction between KERI/ACDC, MDOC, and VC/SD-JWT approaches.
- **Guardianship relationship vs. privileges:** Confirmed these must be modeled as separable, independently-revocable constructs.
- **X.509 evaluation:** Will take a brief, bounded look next session rather than a deep dive, since the group leans toward it not being a viable path.

## Action Items

| Item | Owner | Due |
|------|-------|-----|
| Examine individual AID privacy properties and avoiding persistent correlators | Group | Next meeting |
| Brief evaluation of X.509 infrastructure against KERI/ACDC guarantees (bounded scope) | Group | Next meeting |
| Read Daniel Hardman's white paper (Provenant/telecom work) on DNS-as-root-of-trust tradeoffs | Group | Next meeting |
| Continue defining what a guardianship credential looks like from the state's perspective, keeping relationship and privilege separate | Wayne Chang / SEDI Program | Next meeting |

## Next Meeting

**Date:** 2026-09-18
**Topics:** Individual AID privacy/correlation properties; brief X.509 feasibility look; continued guardianship credential definition (state's perspective)
