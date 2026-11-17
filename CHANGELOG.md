# Changelog

## Draft v0.6, Service API of the File Management core

Adds a first draft of the Service API. It covers the most important operations of the File Management core; the extensions have no operations yet. Requirements are unchanged except where noted.

- New contract `api/openapi.yaml` (OpenAPI 3.1.2, API version `1.0.0-draft`), written to the GovStack Cross-BB API Design Guide and ruleset 0.3.0-draft: 27 operations for Containers, Files and their content, Versions, deleted items, search, permission grants, share links and event subscriptions, the File event webhook, and `/health`. Each operation has a plain-language summary and description (Purpose, When to use, You provide, You get back, Rules, Related, Technical notes).
- Conventions of the guide applied: `/v1` paths, RFC 9457 problems under `https://govstack.global/problems/document-management/`, cursor pagination, `Idempotency-Key` on creating requests, strong `ETag` and `If-Match`, W3C trace context, OAuth 2.0 for people and for services with namespaced scopes, CloudEvents 1.0 for events.
- New files: `api/index.yaml`, `api/coverage.yaml` (empty while requirements are DRAFT), `api/README.md`, the vendored shared schemas `api/common/govstack-openapi-common.yaml`, `resources/api.yml` (link to the contract, at the location the Specification Framework names) and `resources/api-reference.md` (operations, requirement mapping, design decisions, mapping to the reference software, validation).
- `api_operation_id` filled for 32 requirements of the File Management core; a requirement that needs several operations lists them.
- `metadata.yml`: version 0.6-draft and `maturity: 1`. The specification stays at maturity 1 until every `SERVICE_API` requirement names an operation and two software solutions have checked the contract.
- Documentation updated: STO-13 (the resumable upload protocol is an open question), INT-5 (WebDAV is an additional channel, not the Service API).
- Module pages: the interface *Document Management API* now refers to `api/openapi.yaml`; *File events* to the webhook `fileEvent`.
- Terminology: added permission grant and share link.
- Open questions: the Service API strategy is answered as a proposal; 13 questions on the contract added.

## Draft v0.5, second review of the File Management core

Applies the decisions of the second review, which looked for statements that can go, and renames two functionalities.

- Functionalities renamed: Document Storage is now File Storage (`requirements/file-storage.md`) and Document Sharing is now File Sharing (`requirements/file-sharing.md`), because the core manages Files and Containers. The interface *Document events* is now *File events*. Capability names and the name of the Building Block are unchanged.
- Terminology: the entry *Document* notes that only the capitalised term is the defined one.

| Change | Labels |
|---|---|
| Removed | ACC-14 (attribute-based access), RPT-3 (inactive Files) |
| Turned into a Constraint of STO-6 | STO-21 (Version removal), which thereby becomes part of a REQUIRED requirement |
| Clause removed because a cross-functional requirement already states it | STO-8 (deletion record, govstack-cfr-data#req-7), MET-6 (error naming the field, govstack-cfr-data#req-5), MET-19 and ACC-15 (logging, govstack-cfr-security#req-3), ACC-7 (identity provider, govstack-cfr-security#req-3), MET-1 and INT-3 (UTC, govstack-cfr-data#req-2) |
| Clause removed because ACC-4 already states it | MET-3, INT-2 |
| One interaction type per requirement | INT-1 keeps event delivery, with retry as a Constraint; INT-2 now registers subscriptions through the API; ACC-9 is of type USER_INTERFACE |

- Module page: the actor and the interface *Identity provider* are removed, because identity is inherited from the cross-functional requirements.
- *Data structures* of File Storage no longer repeats the fields of a File; they are listed in *Metadata and Search*.
- Descriptions of File Storage, Metadata and Search, Access Control and Usage Reporting no longer list the requirements label by label.
- The File Management core now has 64 requirements, 20 REQUIRED and 44 RECOMMENDED (after the first review: 67, 20 and 47).

## Draft v0.5, review of the File Management core

Applies the decisions of the per-requirement review of the File Management core. The extensions change only where a requirement moved into them.

- The core knows Files and Containers only. Statements say File; *item* is defined as a File or a Container; Documents enter with the Records Management extension.
- *Expiry period* replaces *retention period* in the core (STO-16). Retention stays a term of the Records Management extension.
- Terminology: added item, caller, user, recipient, manager, share permission and expiry period. "Authorised" and "designated" users are replaced by a named permission or by the manager of a Container.

| Change | Labels |
|---|---|
| Reworded | STO-2, STO-3, STO-8 to STO-12, STO-14, STO-16, STO-18, STO-19, MET-1 to MET-4, MET-6, MET-8, MET-10, MET-14, MET-16, MET-17, ACC-1 to ACC-4, ACC-7, ACC-8, ACC-10, ACC-11, ACC-14 to ACC-16, INT-1 to INT-4, RPT-2 to RPT-4 |
| Documentation only | STO-6, STO-13, MET-13 (now AUDITABLE), INT-5, RPT-1 |
| Split | STO-4 into STO-4 and STO-20 (listing the contents of a Container); MET-7 into MET-7 and MET-18 (optical character recognition); MET-11 into MET-11 and MET-19 (listing the Files of a data subject) |
| New, REQUIRED | STO-22 (deleting a File), STO-23 (listing and restoring deleted items) |
| New, RECOMMENDED | STO-21 (Version removal), STO-24 (malware scan), STO-25 (conditional replacement), MET-20 (SHA-256 digest), ACC-17 (permissions of a moved item), ACC-18 (sensitivity classification), INT-7 (signed event deliveries) |
| Merged and removed | STO-15 and MET-12 into STO-10; ACC-12 into ACC-1 |
| Removed | MET-9 (named as an option in MET-7), ACC-13, INT-6 (CMIS, now named in the reference software) |
| Moved to the Records Management extension | STO-17 to Records Processes; MET-15 to Records Capture; the document type filter of INT-2 to PRC-15 |
| Parked for the Working Group | STO-1, see the open questions |

- Module page: reworded *Why choose this conformance module?* and the first use case, added the actors Official and Identity provider and the interfaces Share page and Identity provider, removed CMIS.
- Functionality descriptions no longer state RECOMMENDED behaviour as a guarantee.
- Metadata fields are of three kinds: system, reserved and custom.
- The File Management core now has 67 requirements, 20 REQUIRED and 47 RECOMMENDED (before: 63, 17 and 46). The Records Management extension has 71, 26 REQUIRED and 45 RECOMMENDED.

## Draft v0.5 (test branch)

- Conformance profiles replaced by conformance modules: the File Management core and the Working Document Collaboration and Records Management extensions.
- The extensions no longer include the File Management core in their scope, as in v0.3: every conformant software solution meets the core and may claim one or both extensions.
- Folder `conformance-profiles` renamed `conformance-modules`. The extension pages list only their own functionalities, actors and interfaces, and refer to the core page for the rest. "Why choose this profile?" became "Why choose this conformance module?".
- `metadata.yml`: `conformance_profiles` replaced by `conformance_modules`, each with a `type` (`CORE` or `EXTENSION`) instead of `includes`. Version set to 0.5-draft.
- Technical overview: the functionalities table names one conformance module per functionality, and the section *Conformance profiles* became *Conformance modules*.
- Purpose, scope, requirement documentation, reference software and open questions use core and extension again.
- Terminology: added conformance module, core and extension.


## Draft v0.4 (test branch)

- Core and extensions replaced by three conformance profiles: File Management (formerly the core), Working Document Collaboration and Records Management. The latter two include File Management. Their scope is unchanged.
- `metadata.yml`: `extensions` replaced by `conformance_profiles`, each with `includes` and the list of its functionalities.
- New folder `conformance-profiles` with one file per profile: why choose it, example use cases, functionalities, actors relevant for testing, interfaces.
- `introduction/overview.md` renamed `introduction/technical-overview.md` and moved after the scope in `toc.yml`. The chapter *Building Block Software* became *Market assessment*, with the former boundary description as its last section. *Core and extensions* became *Conformance profiles*. The actors and interfaces tables moved to the profile files.
- Functionalities table: column *Conformance* became *Conformance profiles*.
- `conformance` and `extension` fields removed from all functionality files.
- "system under test" replaced by "Building Block Software"; product and solution now always read "software product" and "software solution".
- `toc.yml`: fixed the entry for `reference-software.md`, which still pointed to `reference-products.md`.


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

Added by this draft: INT-5 (WebDAV access), because most candidate software products offer it and the Service API strategy is open.

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
| Two data centres, RPO and RTO, sizing tool | Deployment and hosting concerns, outside the Building Block Software |
