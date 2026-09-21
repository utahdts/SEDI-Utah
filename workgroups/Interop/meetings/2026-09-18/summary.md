# SEDI Interop Working Group — Summary
**Date:** 2026-09-18

> The personal data collected in this meeting is classified as a public record and may be made available to the public as provided by the Government Records Access and Management Act (Utah Code § [63G-2-201](https://le.utah.gov/xcode/Title63G/Chapter2/63G-2-S201.html)).

---

## Discussion

### Process Check-In: Requirements Before Implementation

The session opened by revisiting a recent email thread that raised a process concern: the group has been diving into a KERI/ACDC-specific implementation discussion — because it fits the guardianship use case well — before clearly articulating technology-neutral technical requirements anchored in policy. The suggested discipline: start from policy, derive technical requirements, and only then compare implementation options against those requirements. There was broad agreement with this framing, along with a related observation that guardianship, while a legitimate and legislatively-grounded focal point (SB 142), has consumed most of the group's bandwidth and left other valuable, lower-complexity use cases (e.g., vital records, licensing credentials) largely unexamined.

### System of Record vs. Verifiable Credentials

A recurring source of friction was identified: the group has been describing requirements for two distinct systems without naming the distinction — **system-of-record requirements** (where claims live in their original/golden-record state) and **verifiable-credential requirements** (portable, self-contained representations such as SD-JWT, W3C Verifiable Credentials, MDOCs, or AC/DCs). Separating these explicitly was proposed as a way to resolve disagreements that are really about which system a given requirement applies to, rather than genuine technical disagreement.

### Scope of Statements About W3C Verifiable Credentials

A concern was raised that recent sessions have been imprecise about exactly which system and identifier is under discussion, and that broad use cases (guardianship, delegation) pull every system into scope — so statements meant to apply narrowly can be heard as absolute. Specifically, a claim that W3C Verifiable Credentials "cannot" be used for the guardianship case went uncorrected in a prior session and was heard by some as excluding an entire technical community.

Clarification followed: prior discussion had identified W3C VCs as well-suited to *temporary-use* credentials, where their crypto/verifiability period is a natural match — not as unsuitable across the board. The distinction being drawn is architectural: KERI/AC-DC's **perpetually verifiable issuance** property is not something W3C VCs currently have a built-in mechanism for, which is a capability gap, not a rejection of the format. The group converged on a practical framing: since Utah cannot dictate credential format to other jurisdictions (which already use a mix of MDLs, W3C VCs, and other formats), the priority is defining concrete, technology-neutral technical requirements and letting any credential community or format demonstrate that it meets them, rather than the group declaring any technology broadly incapable.

### External Signal: Pro-Human Coalition and Rising Interoperability Bar

An update was shared from a Washington, DC event this week that produced a new "Pro-Human Coalition" (successor to Project Liberty), including a workshop on trust infrastructure for AI agents. SEDI credentials were presented there as an example of the "state-endorsed credential" paradigm and were well received. The broader takeaway offered to the group: as proof-of-personhood and AI-agent-delegation use cases mature, the bar for credential interoperability is rising, and the group should track that trajectory alongside its current use cases.

### Interoperability Strategy: Layering Formats on KERI Key Management

Because Utah cannot require every external jurisdiction and relying party to adopt KERI/AC-DC, the practical path discussed was using KERI for key management underneath, with did:webs allowing other credential formats to be layered on top for interoperability with parties that use different formats — preserving KERI's security properties for key management while still interoperating with external systems on their own terms. The group agreed that defining concrete technical requirements — rather than declaring any single DID method or credential format the winner — is what will allow multiple communities to build toward the same target and be evaluated fairly.

### Did:webs as "Common Ground": No Formal Consensus

A question was raised about whether the group had reached agreement that did:webs represents shared common ground, since it has generated comparatively little disagreement. The answer: this was surfaced informally in an earlier session but never formally ratified, and the group currently has no defined process for reaching or recording consensus. There was explicit acknowledgment that naming a specific DID method risked being read as excluding other methods (e.g., did:webvh, other DID methods in current standards work) that may also satisfy the underlying requirements. The recommended path: agree on technology-neutral requirements first, and let did:webs, did:webvh, and other methods each demonstrate how they meet those requirements — both for fairness across communities and for durability, since naming specific technologies now will not hold up over the software's expected multi-decade lifespan.

### Governance Framework vs. Technology Stack

SEDI was described as currently a governance framework, not yet a technology stack, and this group's work is part of translating one into the other. A stated design goal is avoiding a "Swiss Army knife" outcome — supporting many formats that mostly go unused — in favor of narrowing to a small number of workable options, some driven by existing market adoption and some defined by the state. Two design questions were distinguished that the group has been conflating: key management / demonstration of control (proposed as format-independent) versus the credential format itself. If control and ownership can be demonstrated independently of format, the state could accept a W3C VC, an MDOC, or an AC/DC interchangeably, provided each demonstrates the same underlying attributes — validity period, provable ownership, and a defined evidentiary basis (referencing NIST SP 800-63A evidence types). The requirements produced by this group need to be concrete and testable, and cannot be requirements Utah imposes unilaterally on other sovereign states.

### Working Group Charge and Process

A concern was raised that the group has not actually moved past relationship-forming into structured work, since there has been no persistent place to record requirements — discussion has lived in a moving email thread — and the group's charge has become unclear. The understood mandate is **interoperability**: how SEDI interfaces with external systems, not how Utah designs its own internal systems. Delegated batch issuance (bridging KERI-based issuance to other credential systems) was cited as an example of interoperability work that guardianship discussion has crowded out. There was agreement that the group remains in an early, unsettled ("storming") stage rather than a settled working rhythm.

A related point was raised that the state, not volunteer working-group participants, should own producing the requirements list, with the group critiquing and refining a state-authored draft rather than originating it. An existing draft requirements document was confirmed to already exist: deliberately protocol-agnostic, focused on cross-cutting concerns (key management, selective disclosure, organizational security controls) that any issuer or protocol would need to satisfy, with protocol/format selection intentionally deferred to separate "profile" documents. That draft is published on the SEDI implementation guide site and has since undergone legal review to correct citations, since its first pass was AI-assisted. It was also noted that the working group's scope is likely to expand — a decentralized fraud-signal use case (driven by external interest, including from the financial sector) will be announced as a related but separate line of work at the upcoming summit, meaning the group will need to explicitly delineate which topic is active at a given time.

### Path Forward: Working in the Open

The SEDI-Utah GitHub repository is live and available for the group's use. Group members should expect to interact with it as an open/public repo rather than through direct collaborator invitations, since direct invitations currently consume a paid seat; this will be revisited if members encounter access issues. The direction going forward is to build on the existing requirements draft rather than starting over, use the GitHub repo to organize discussion by work-group topic as scope expands, and move requirements and profile-document discussion into GitHub issues and pull requests between sessions rather than waiting for the weekly call.

---

## Decisions

- **Requirements baseline:** Build on the existing, legal-reviewed, protocol-neutral requirements draft already published on the SEDI implementation guide site, rather than starting a new requirements document.
- **No consensus on did:webs:** Confirmed that no formal consensus exists that did:webs is the group's common ground — it was surfaced informally but never ratified. Technology-neutral requirements will be agreed first; did:webs, did:webvh, and other DID methods will each be evaluated against those requirements.
- **Separate system-of-record from credential-format requirements:** Going forward, the group will distinguish system-of-record requirements from verifiable-credential-format requirements, and separate demonstration of control/ownership from the credential format itself, so multiple formats (W3C VC, MDOC, AC/DC) can be evaluated against a shared, technology-neutral baseline.
- **GitHub as primary working surface:** The group will move requirements and profile-document work into the GitHub repo (issues/PRs) between sessions, rather than relying on email threads or waiting for the weekly call.

## Action Items

| Item | Owner | Due |
|------|-------|-----|
| Continue building out the technical requirements document (cross-cutting, protocol-neutral) in the GitHub repo | SEDI Program | Next meeting |
| Flag any disagreement with the general requirements approach via the repo or email chain | Group | Next meeting |
| Begin drafting protocol-specific profile documents mapping requirements to implementations (did:webs, did:webvh, others) | Group | Next meeting |
| Confirm GitHub repo access approach for external collaborators; resolve any permission issues | SEDI Program | Ongoing |
| Clarify and communicate the working group's charge and scope in writing (interoperability with external systems, distinct from Utah's internal SEDI design and the emerging fraud-signal track) | SEDI Program | Next meeting |

## Next Meeting

**Date:** 2026-09-25
**Topics:** Continued build-out of the technical requirements document and start of protocol-specific profile documents in GitHub; charge/scope clarification.
