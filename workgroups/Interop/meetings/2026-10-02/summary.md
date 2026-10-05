# SEDI Interop Working Group — Summary
**Date:** 2026-10-02

> The personal data collected in this meeting is classified as a public record and may be made available to the public as provided by the Government Records Access and Management Act (Utah Code § [63G-2-201](https://le.utah.gov/xcode/Title63G/Chapter2/63G-2-S201.html)).

---

## Discussion

### Policy Landscape and Legislative Strategy

An update was shared on the broader policy environment: outside the identity community, digital identity is not yet a top-of-mind issue for most industry groups or legislators, even those focused on privacy and AI. No federal legislation on digital identity or AI is expected in the near term. Two framings were proposed as potential hooks for policymaker attention: the security exposure of license-plate-reader camera systems (illustrating that key-management weaknesses affect things as well as people), and the emerging "portable memory" concept — the idea that personal AI agents acting on an individual's behalf require portable, user-controlled identity. The next round of state-level digital-identity legislation nationally is trending toward a more detailed, capabilities-and-outcomes-based governance framework.

### AAMVA and MDL Credential Scope

The group discussed the state of engagement with the mobile driver's license (MDL) community. There is continued tension between SEDI's direction and some MDL stakeholders' concerns about scope. A specific architectural question was raised: could an MDOC-based MDL credential be considered a SEDI credential, provided it meets SEDI's legal requirements (e.g., anti-surveillance and compromise-detection mechanisms)? One proposal distinguished the *identification* function of an MDL — which could fall under SEDI policy — from the *driver-licensing* function, which would remain under DMV authority. The group also discussed that governance models built around a DMV-centric association may not extend naturally to non-DMV-issued credentials (e.g., student or veteran IDs) or to relying parties outside the DMV ecosystem, such as financial institutions.

### Digital Backpack and Transaction-Type-Based Interoperability

The group revisited the "digital backpack" framing for SEDI: interoperability does not require a single, unified credential format. Instead, guardrails should be defined based on transaction type — distinguishing perpetual (long-lived) from ephemeral (temporary) transactions — with a defined mechanism for linking other systems' transactions back to SEDI for legal enforceability. It was noted that SEDI can be realized using MDOC and other formats, and that building bridges to existing credential communities (MDL, MDOC, W3C Verifiable Credentials, the European Commission's framework) is necessary to avoid an exclusionary outcome. The requirements document circulated by the group previously was cited as a useful basis for a cross-community technical target.

### Key Management vs. Credential Format

A recurring architectural point was reinforced: credential *format* is not the primary interoperability challenge — *security policy and key management* are. Frequent key or certificate rotation tends to create a centralizing force, since it requires an ongoing relationship with the issuing authority to maintain validity. Credentials designed for long-lived (perpetual) use paired with a revocation-based control model create a decentralizing force instead, since revocation requires a deliberate, accountable action rather than routine reissuance. The group discussed how legacy PKI rotation practices — a holdover from certificate-authority norms rather than a requirement of the credential itself — can undermine the security properties SEDI is designed to provide, and cautioned against adopting those practices solely to appear more interoperable with existing systems. It was also noted that superficially similar key-management approaches can differ in which specific exploits they protect against, so similarity alone is not sufficient grounds for treating two approaches as interchangeable.

### Standards Engagement Strategy: IETF and W3C

The group discussed an in-progress IETF draft focused on key-management properties (rotation, compromise detection) independent of credential format. Feedback suggested the current draft's scope — intended to apply across people, devices, applications, and AI agents — may be broader than necessary, and that existing DID methods and credential formats should be evaluated against the draft's requirements before concluding new standards work is required. Separately, the group noted that the W3C DID Methods Working Group charter (pending a vote within the week) already includes did:webs, and discussed the relative value of pursuing IETF standardization versus concentrating effort in the W3C track. The consensus was to pursue multiple standards tracks in parallel rather than choosing one, since different stakeholder communities place different weight on each body's standards.

### Summit Planning: Technical Interoperability Session

The group discussed adding a technical workshop session to the upcoming SEDI summit, bringing together representatives from different standards communities (W3C, KERI/Trust Over IP, MDL, IETF) to address what interoperability concretely requires in this space. The session is intended to demonstrate that SEDI is pursuing a competitive, multi-standard approach rather than being tied to a single technology. To be effective for a technical audience, the session should feature concrete progress and examples rather than general discussion.

---

## Decisions

- **Multi-track standards strategy confirmed:** The group will continue pursuing both IETF and W3C standards tracks in parallel rather than consolidating on one, given differing stakeholder expectations across standards bodies.
- **Summit workshop:** A technical interoperability workshop session (not a main-stage session) will be added to the SEDI summit agenda, bringing together representatives from multiple standards communities.

## Action Items

| Item | Owner | Due |
|------|-------|-----|
| Narrow the scope of the in-progress IETF key-management draft and recruit additional co-sponsors ahead of the next submission window | SEDI Program | Next meeting |
| Continue contributing to iteration of the IETF key-management draft | Group | Ongoing |
| Finalize and add a technical interoperability workshop session to the SEDI summit agenda | SEDI Program | Before summit |

## Next Meeting

**Date:** 2026-10-09
**Topics:** Continued discussion of credential-format interoperability requirements and standards engagement strategy.
