# Changelog

## Draft v3

### Structure

- Rewritten in the layout of `bb-template` (beta/2.0) and the model of the Specification Framework pull request #1: capabilities in `metadata.yml`, one file per functionality in `requirements/`, a core and two extensions.
- Ten capabilities declared along the document lifecycle. Each functionality names the capabilities it realises.
- The three key functionalities of draft v2 became fifteen functionalities:

| Draft v2 | Draft v3 functionality | Conformance |
|---|---|---|
| KF1 File Management, storage and versions | Document Storage | Core |
| KF1, metadata and search | Metadata and Search | Core |
| KF1, access control and sharing | Access Control; Document Sharing | Core |
| KF1, integration | Integration and Events | Core |
| (new) | Usage Reporting | Core |
| KF2 Working Document Collaboration, editing and sharing | Collaborative Editing | Working Document Collaboration extension |
| KF2, activity history | Collaboration History | Working Document Collaboration extension |
| KF3 Records Management, records and their states | Records Capture | Records Management extension |
| KF3, records processes | Records Processes | Records Management extension |
| KF3, classification, retention and disposition | Classification and Retention; Archival Preservation | Records Management extension |
| KF3, activity trail | Records Audit Trail | Records Management extension |
| KF3, document exchange between organisations | Inter-agency Document Exchange | Records Management extension |
| KF3, issued documents for document wallets | Issued Document Access | Records Management extension |

### Requirement labels

All working labels of draft v2 are kept. They moved as follows:

| Labels | Now in |
|---|---|
| STO-1 to STO-16 | Document Storage |
| MET-1 to MET-12 | Metadata and Search |
| ACC-1 to ACC-7 | Access Control |
| ACC-8 to ACC-13 | Document Sharing |
| INT-1 to INT-4 | Integration and Events |
| WRK-1 to WRK-13 | Collaborative Editing |
| WRK-14 to WRK-16 | Collaboration History |
| REC-1 to REC-10 | Records Capture |
| PRC-1 to PRC-17 | Records Processes |
| RET-1 to RET-7, RET-9 to RET-11 | Classification and Retention |
| RET-8, RET-12 to RET-14 | Archival Preservation |
| ACT-1 to ACT-6 | Records Audit Trail |
| XCH-1, XCH-2 | Inter-agency Document Exchange |
| DOC-1 to DOC-9 | Issued Document Access |

### New requirements, all RECOMMENDED

Taken from the first write-up in `bb-file-management/spec/4-key-digital-functionalities.md`:

| Label | Subject |
|---|---|
| STO-17 | Major and minor Version labels |
| STO-18 | Protection mark against deletion |
| STO-19 | Second approval before an early purge |
| MET-13 | Metadata as Dublin Core elements |
| MET-14, MET-15 | Proposed metadata and document type, confirmed by a person |
| MET-16 | No content sent outside the deployment for analysis |
| MET-17 | Erasure or pseudonymisation on a data subject's request |
| ACC-14 | Attribute-based access |
| ACC-15 | Recorded emergency override (break-glass) |
| ACC-16 | Redacted copies |
| INT-6 | CMIS access |
| RPT-1 to RPT-5 | Usage Reporting: storage, activity, inactive documents, refused access, exports |
| REC-11 | Reading ASiC signature containers |
| PRC-18 | Assignment to the initiator's manager |
| PRC-19 | Claiming a group step |
| PRC-20 | Periodic review of a finalized record |
| RET-15 | Destruction approved by two users |
| RET-16 | Periodic checksum verification |
| RET-17 | Report of formats at risk of obsolescence |
| ACT-7 | No operation without its activity record |
| ACT-8 | Syslog export |
| ACT-9 | Activity records kept at least twelve months |
| ACT-10 | Identifiers instead of personal data in activity records |

Added by this draft: INT-5 (WebDAV access), because most candidate products offer it and the Service API strategy is open.

### Changed wording

- ACC-4 now covers search results as well as the web interface, API, WebDAV and synchronisation clients (first write-up: the same authorisation for UI, API and search).
- REC-9 names SHA-256 as the checksum algorithm (first write-up).
- Every requirement has an `interaction` classifier and an `observability` classifier.

### Considered and not taken

| Consideration | Reason |
|---|---|
| Delta storage of Versions | An implementation choice; the working group discussed the risk of a corrupted increment |
| Documents as code (declarative source with rendering to PDF/A) | Marked as future; listed in the open questions |
| Semantic search and anomaly detection by AI | Not yet stated as verifiable behaviour; MET-16 already keeps content inside the deployment |
| Scheduled publication and removal on public websites | Belongs to a Content Management System Building Block |
| SAML and OIDC, AES-256 and TLS 1.3, WCAG 2.1 AA | Inherited from the cross-functional requirements |
| Two data centres, RPO and RTO, sizing tool | Deployment and hosting concerns, outside the system under test |
