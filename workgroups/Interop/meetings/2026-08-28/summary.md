# SEDI Interop Working Group — Summary
**Date:** 2026-08-28

> The personal data collected in this meeting is classified as a public record and may be made available to the public as provided by the Government Records Access and Management Act (Utah Code § [63G-2-201](https://le.utah.gov/xcode/Title63G/Chapter2/63G-2-S201.html)).

---

## Discussion

### Recap: Previous Session — Guardianship Data Model

The group recapped the prior session's work on a technology-agnostic guardianship data model developed against Utah SB 142 (2025). Components identified: identity of guardian, identity of ward, attributes of the guardian-ward relationship, guardian scope of action, and ward scope of action — each potentially carrying separate issuers and revocability. The modeled scenario involved a multi-generational family (aging grandparent, digitally native parent, teenager, young child).

This session's focus shifted to evaluating `did:webs` through the lens of requirements rather than technical mechanics — framed to bridge the technical and policy worlds.

### did:webs Technical Overview

`did:webs` is a DID method that combines `did:web` (DNS-based resolution) with an AID (autonomic identifier from the KERI ecosystem) as the method-specific identifier. Key properties:

- **Two resolution paths:** A `did:webs` document can resolve as a standard `did:web` document (public key only, no KERI awareness) or as a full KERI-anchored document with key event log references. The relying party chooses which to evaluate based on their security requirements.
- **Interoperability bridge:** Systems without KERI support can verify credentials using standard `did:web` semantics; KERI-aware systems can access the full key event log for stronger guarantees. Prior art: the vLEI "web vLEI" approach used this pattern for CBP interoperability.
- **Multisig support:** The `did:web` extension allows multiple keys with a threshold — key management not possible in standard `did:web`.
- **Development maturity:** Several years of development; relatively mature for a DID method.

Core framing: the real difference between `did:web` and `did:webs` is the AID and its associated key event log — the source of the additional guarantees the group evaluated below.

### Requirements: Plain Language

The group derived the following requirements for a long-lived, portable identity system capable of supporting SEDI:

**Long-lived, stable identifiers ("perpetual identity")**
- Required for both humans (citizens) and organizations (state agencies, departments)
- For organizations, DNS domains are a natural fit; for individuals, wallet-based or subdomain approaches are more practical
- Proposed organizational structure: a root of trust at the state administration level, with delegated identifiers at the division/department level (the department issuing guardianship credentials is distinct from the one issuing food handler permits)

**Compatible with DNS, but not dependent on it**
- DNS is appropriate for discovery and connection, not as a security foundation
- DNS was designed for trusted academic networks; security mechanisms were retrofitted. Known weaknesses include DNS cache poisoning, BGP hijacking, and certificate spoofing
- DNS security extensions (DNSSEC) exist but are not broadly or reliably deployed; the group noted that current best practices around DNS security remain vulnerable to the same underlying issues
- Consensus: DNS for discovery is acceptable; DNS as sole security mechanism is not

**Portable**
Two distinct dimensions captured:
1. *Cross-DNS-domain portable* — an identifier moves from one domain to another without losing continuity (e.g., `asu.edu` → another host)
2. *Cross-infrastructure portable (vendor lock-in resistant)* — not dependent on any particular infrastructure provider; the identifier survives provider migrations

The AID (method-specific identifier) is what is truly portable — DNS domain names are aliases on top of it, not the identity itself.

**Historically resolvable**
- A credential must remain verifiable after the issuer rotates keys
- `did:web` fails here: key rotation removes the prior public key from the DID document, making previously issued credentials unverifiable
- `did:webs` addresses this via the KERI key event log, which preserves the full history of key state and supports cryptographic proof of the key that was active at issuance

**Perpetually verifiable credentials**
- State-issued credentials (birth certificates, guardianship credentials) must not require reissuance on cryptographic rotation schedules
- The web PKI ecosystem is moving toward 45-day certificate lifetimes; applying this model to citizen wallets at scale is unworkable
- Short crypto periods create churn pressure that pushes architecture toward centralization — wallet providers absorb the rotation burden, which undermines portability

**Resilient to cryptographic migration**
- Must survive algorithm transitions, including post-quantum migration
- Post-quantum migration urgency was raised explicitly: adversaries are currently capturing encrypted traffic for future decryption once quantum capabilities mature ("harvest now, decrypt later"). Migration cannot wait for a future deadline.
- The broader web ecosystem is moving toward hybrid post-quantum certificates (Merkle tree certificates, dual-key hybrids), but non-browser systems (firmware, IoT, embedded infrastructure) represent a large unresolved migration problem — these devices cannot be easily updated and are not covered by CAB Forum mandates
- KERI's key event log is designed to support algorithm agility over the lifetime of an identifier

**Why start with cryptography and key management?**
Addressed as a foundational question: any system that does *not* start with cryptography requires trusted third parties — which means the identity is ultimately controlled by the third party, not the individual. Shorthand: "not your keys, not your ID."

Note on key loss: a fault-tolerant key management system (as in KERI's design) separates identifier control from any single key. The identifier persists through key rotation and recovery, so loss of an individual key does not mean loss of the identity.

**User-controlled fraud signals (tabled)**
- Raised in the context of proof of control and proof of presentation
- Distinct from verifier-side fraud detection: allows the holder to detect that they are being impersonated, rather than requiring the verifier to catch impersonation
- Noted as important to prevent a new class of derived PII signal brokers ("continuous identity" / behavioral signal aggregation)
- Deferred as out of scope for this discussion; captured for a future session

### Witness Infrastructure and X.509 Evaluation

Toward the close of session, two additional topics were introduced:

**Witness infrastructure compatibility**
- Proposed as a requirement: compatibility with witness/observer infrastructure — examples include certificate transparency logs and KERI witnesses
- Rationale: provides an additional mechanism to mitigate DNS shortcomings without full dependency on DNS

**X.509 infrastructure as an alternative path**
- A question was posed to the group: can all of the requirements established in this session be satisfied using existing X.509 infrastructure primitives (including OCSP)?
- The counterargument: X.509 lacks true portability. Certificate Authorities conflate public key verification, endpoint verification, and identity — whereas decentralized infrastructure separates these concerns. X.509 identifiers are bound to CAs and cannot be migrated across infrastructure.
- The group agreed the question is worth a rigorous engineering evaluation rather than dismissal
- Action assigned: conduct an earnest engineering analysis of an X.509-based system against the same requirements, to determine whether the approach is tractable or intractable

---

## Decisions

- **Requirements approach:** `did:webs` requirements will be documented in plain language oriented toward policy audiences and relying parties, not raw technical mechanics
- **DNS positioning:** DNS is appropriate for discovery; it is not sufficient as a security foundation for identity credentials
- **User-controlled signals:** Important but out of scope for the `did:webs` requirements discussion; captured for a future session
- **Meeting rescheduled:** Next week's meeting will be skipped due to travel (GDC) and the US Labor Day holiday; group will resume on the existing calendar slot two weeks out

---

## Action Items

| Item | Owner | Due |
|------|-------|-----|
| Engage a DNS security expert to document why DNS-only approaches are insufficient for identity security | Group | Next meeting |
| Conduct engineering analysis of an X.509-based system against the established requirements | Spruce ID | Next meeting |
| Continue `did:webs` requirements documentation in shared whiteboard | Moderator | Next meeting |

---

## Next Meeting

**Date:** 2026-09-11 (skipping 2026-09-04 due to travel/Labor Day)
**Topics:** X.509 feasibility analysis; continue `did:webs` requirements; post-quantum migration requirements
