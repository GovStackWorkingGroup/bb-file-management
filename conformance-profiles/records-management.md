---
title: Records Management profile
---

# Records Management profile

## Why choose this profile?

Choose Records Management when documents are evidence of what the administration decided and did. A record is edited only by the people assigned to each step of a predefined process, is fixed when the process ends, and changes afterwards only by adding traceable versions. It belongs to a class of the organisation's classification scheme, is kept as long as the law requires, and is then destroyed or transferred to an archive after an authorised decision. Every action on it, including who viewed it, is recorded.

The profile includes File Management, so every record is also stored, versioned, findable and protected as in that profile.

## Example use cases

- **A building permit decision.** Case officer A drafts the decision, structural engineer B adds the safety conditions, head of unit C approves it, and the decision is finalized and fixed.
- **Evidence received as submitted.** The application form an applicant submits is declared a finalized record on receipt.
- **Retention and disposition.** When the case is closed, the case file's retention period starts. When it ends, a records manager reviews the file and approves its destruction or its transfer to the archive.
- **Handover to the archive.** Records no longer in active use move to the organisational archive, and later go to the central archive as a transfer package with their metadata, process history and activity trail.
- **Exchange between administrations.** A ministry sends a signed decision to another agency through the Information Mediator, and the agency registers it as received.
- **A document wallet.** A citizen's wallet refers to an issued certificate; a bank fetches it from its source with the citizen's consent and checks that it is still valid.

## Functionalities

| Functionality | From profile | Requirements | REQUIRED | RECOMMENDED |
|---|---|---|---|---|
| [Document Storage](../requirements/document-storage.md) | File Management | 19 | 10 | 9 |
| [Metadata and Search](../requirements/metadata-and-search.md) | File Management | 17 | 3 | 14 |
| [Access Control](../requirements/access-control.md) | File Management | 9 | 4 | 5 |
| [Document Sharing](../requirements/document-sharing.md) | File Management | 7 | 0 | 7 |
| [Integration and Events](../requirements/integration-and-events.md) | File Management | 6 | 0 | 6 |
| [Usage Reporting](../requirements/usage-reporting.md) | File Management | 5 | 0 | 5 |
| [Records Capture](../requirements/records-capture.md) | Records Management | 11 | 7 | 4 |
| [Records Processes](../requirements/records-processes.md) | Records Management | 20 | 10 | 10 |
| [Classification and Retention](../requirements/classification-and-retention.md) | Records Management | 11 | 7 | 4 |
| [Archival Preservation](../requirements/archival-preservation.md) | Records Management | 6 | 1 | 5 |
| [Records Audit Trail](../requirements/records-audit-trail.md) | Records Management | 10 | 1 | 9 |
| [Inter-agency Document Exchange](../requirements/document-exchange.md) | Records Management | 2 | 0 | 2 |
| [Issued Document Access](../requirements/issued-documents.md) | Records Management | 9 | 0 | 9 |
| **Total** | | **132** | **43** | **89** |

## Actors relevant for testing

All actors of the File Management profile, plus:

| Actor | Kind | Role in tests | Functionalities |
|---|---|---|---|
| Step assignee | Person | Edits, reviews, approves or signs a record in process when the step is assigned to them; receives step notifications | Records Processes |
| Records manager | Person or system | Declares records, configures document types, classification schemes and retention schedules, places legal holds, approves disposition | Records Capture, Classification and Retention, Archival Preservation |
| Process engine or automated agent | System | Drives process steps through the Service API on a person's behalf | Records Processes, Records Audit Trail |
| Other administration's document management system | System | Sends and receives records in the exchange envelope through the Information Mediator | Inter-agency Document Exchange |
| Issuing service and requester gateway | System | Reads issued records and their checksums, creates grants, fetches issued documents | Issued Document Access |

## Interfaces

All interfaces of the File Management profile, plus:

| Interface | Counterpart | Direction | Functionalities | Type | Contract defined in |
|---|---|---|---|---|---|
| Document Management API | Service application, records manager, process engine, automated agent, issuing service | Inbound | All Records Management functionalities | Service API | This specification, `resources/api` (to be written) |
| Web interface | Step assignee | Both | Records Processes (PRC-7, PRC-12, PRC-17) | User interface | This specification |
| Records events | Event subscriber | Outbound | Records Processes (PRC-15), Issued Document Access (DOC-7) | Event | This specification |
| Exports | Administrator, security monitoring | Outbound | Records Audit Trail (ACT-4, ACT-8), Issued Document Access (DOC-8) | File | This specification; IETF RFC 5424 |
| Records renditions and signature containers | Archive, e-Signature BB | Both | Records Capture (REC-10, REC-11) | File | ISO 19005 (PDF/A); ETSI EN 319 162-1 (ASiC) |
| Archival transfer packages | Central government archive | Outbound | Archival Preservation (RET-8, RET-13, RET-14) | File | E-ARK SIP specification |
| Document exchange envelope | Other administration's document management system, through the Information Mediator | Outbound send, inbound receipt | Inter-agency Document Exchange | Consumed API | `govstack:spec:bb:information-mediator`; envelope specification to be agreed |
