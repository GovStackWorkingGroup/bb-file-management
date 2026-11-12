---
title: Records Management extension
---

# Records Management extension

## Why choose this conformance module?

Choose Records Management when documents are evidence of what the administration decided and did. A record is edited only by the people assigned to each step of a predefined process, is fixed when the process ends, and changes afterwards only by adding traceable versions. It belongs to a class of the organisation's classification scheme, is kept as long as the law requires, and is then destroyed or transferred to an archive after an authorised decision. Every action on it, including who viewed it, is recorded.

The extension covers records management only. A software solution that claims it also meets the File Management core, which stores, versions, finds and protects every record.

## Example use cases

- **A building permit decision.** Case officer A drafts the decision, structural engineer B adds the safety conditions, head of unit C approves it, and the decision is finalized and fixed.
- **Evidence received as submitted.** The application form an applicant submits is declared a finalized record on receipt.
- **Retention and disposition.** When the case is closed, the case file's retention period starts. When it ends, a records manager reviews the file and approves its destruction or its transfer to the archive.
- **Handover to the archive.** Records no longer in active use move to the organisational archive, and later go to the central archive as a transfer package with their metadata, process history and activity trail.
- **Exchange between administrations.** A ministry sends a signed decision to another agency through the Information Mediator, and the agency registers it as received.
- **A document wallet.** A citizen's wallet refers to an issued certificate; a bank fetches it from its source with the citizen's consent and checks that it is still valid.

## Functionalities

| Functionality | Requirements | REQUIRED | RECOMMENDED |
|---|---|---|---|
| [Records Capture](../requirements/records-capture.md) | 11 | 7 | 4 |
| [Records Processes](../requirements/records-processes.md) | 20 | 10 | 10 |
| [Classification and Retention](../requirements/classification-and-retention.md) | 11 | 7 | 4 |
| [Archival Preservation](../requirements/archival-preservation.md) | 6 | 1 | 5 |
| [Records Audit Trail](../requirements/records-audit-trail.md) | 10 | 1 | 9 |
| [Inter-agency Document Exchange](../requirements/document-exchange.md) | 2 | 0 | 2 |
| [Issued Document Access](../requirements/issued-documents.md) | 9 | 0 | 9 |
| **Total** | **69** | **26** | **43** |

## Actors relevant for testing

Testing this extension assumes the software solution meets the File Management core; the actors of the core are described in `file-management.md`.

| Actor | Kind | Role in tests | Functionalities |
|---|---|---|---|
| Step assignee | Person | Edits, reviews, approves or signs a record in process when the step is assigned to them; receives step notifications | Records Processes |
| Records manager | Person or system | Declares records, configures document types, classification schemes and retention schedules, places legal holds, approves disposition | Records Capture, Classification and Retention, Archival Preservation |
| Process engine or automated agent | System | Drives process steps through the Service API on a person's behalf | Records Processes, Records Audit Trail |
| Other administration's document management system | System | Sends and receives records in the exchange envelope through the Information Mediator | Inter-agency Document Exchange |
| Issuing service and requester gateway | System | Reads issued records and their checksums, creates grants, fetches issued documents | Issued Document Access |

## Interfaces

The interfaces of the File Management core are described in `file-management.md`.

| Interface | Counterpart | Direction | Functionalities | Type | Contract defined in |
|---|---|---|---|---|---|
| Document Management API | Service application, records manager, process engine, automated agent, issuing service | Inbound | All Records Management functionalities | Service API | This specification, `resources/api` (to be written) |
| Web interface | Step assignee | Both | Records Processes (PRC-7, PRC-12, PRC-17) | User interface | This specification |
| Records events | Event subscriber | Outbound | Records Processes (PRC-15), Issued Document Access (DOC-7) | Event | This specification |
| Exports | Administrator, security monitoring | Outbound | Records Audit Trail (ACT-4, ACT-8), Issued Document Access (DOC-8) | File | This specification; IETF RFC 5424 |
| Records renditions and signature containers | Archive, e-Signature BB | Both | Records Capture (REC-10, REC-11) | File | ISO 19005 (PDF/A); ETSI EN 319 162-1 (ASiC) |
| Archival transfer packages | Central government archive | Outbound | Archival Preservation (RET-8, RET-13, RET-14) | File | E-ARK SIP specification |
| Document exchange envelope | Other administration's document management system, through the Information Mediator | Outbound send, inbound receipt | Inter-agency Document Exchange | Consumed API | `govstack:spec:bb:information-mediator`; envelope specification to be agreed |
