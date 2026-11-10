---
title: File Management profile
---

# File Management profile

## Why choose this profile?

Choose File Management when government services need one reliable place for the documents they receive and produce. Citizens' supporting documents and the files officials produce are kept under identifiers that never change, with every earlier version, and with the context a service needs to find them again. Each document is reachable only by those entitled to it, can be shared in a controlled way, and other systems learn when it changes.

Because every service integrates with the same interface, a government can replace the Building Block Software without rewriting its services, and can export all documents in open formats if it does.

File Management is included in the other two profiles.

## Example use cases

- **Supporting documents for an application.** A construction permit portal creates a Container for each application and stores the site photos and ownership certificate the applicant uploads. The case officer's application finds them again by case number.
- **Handing out a document.** The permit office gives an applicant a download link to the issued permit that expires after 30 days.
- **Collecting documents without an account.** A social services office sends a citizen an upload-only link to submit missing evidence.
- **Starting work elsewhere.** A process engine receives an event when a new document arrives and starts the review of the application.
- **Answering a data subject access request.** An official lists every document that concerns a given person, across cases.
- **Changing supplier.** A ministry exports all documents of a department with their folder structure in open formats before switching to another Building Block Software.

## Functionalities

| Functionality | From profile | Requirements | REQUIRED | RECOMMENDED |
|---|---|---|---|---|
| [Document Storage](../requirements/document-storage.md) | File Management | 19 | 10 | 9 |
| [Metadata and Search](../requirements/metadata-and-search.md) | File Management | 17 | 3 | 14 |
| [Access Control](../requirements/access-control.md) | File Management | 9 | 4 | 5 |
| [Document Sharing](../requirements/document-sharing.md) | File Management | 7 | 0 | 7 |
| [Integration and Events](../requirements/integration-and-events.md) | File Management | 6 | 0 | 6 |
| [Usage Reporting](../requirements/usage-reporting.md) | File Management | 5 | 0 | 5 |
| **Total** | | **63** | **17** | **46** |

## Actors relevant for testing

| Actor | Kind | Role in tests | Functionalities |
|---|---|---|---|
| Service application | System | Calls the Service API: stores, retrieves and searches documents, manages Containers, permissions and shares, reads reports | Document Storage, Metadata and Search, Access Control, Document Sharing, Integration and Events, Usage Reporting |
| Administrator | Person or system | Configures size limits, quotas, allow-lists and retention periods; approves early purges | Document Storage, Usage Reporting |
| Event subscriber | System | Registers for document events and receives them by webhook, as a process engine would | Integration and Events |
| Link recipient | Person | Opens a download or upload link without an account, as a citizen would | Document Sharing |

## Interfaces

| Interface | Counterpart | Direction | Functionalities | Type | Contract defined in |
|---|---|---|---|---|---|
| Document Management API | Service application, administrator | Inbound | All File Management functionalities | Service API | This specification, `resources/api` (to be written) |
| WebDAV and CMIS access | Clients and service applications | Inbound | Integration and Events | Service API | IETF RFC 4918; OASIS CMIS 1.1 |
| Document events | Event subscriber | Outbound | Integration and Events | Event | This specification |
| Exports and reports | Administrator, other systems | Outbound | Document Storage (STO-10), Metadata and Search (MET-12), Usage Reporting (RPT-5) | File | This specification |
