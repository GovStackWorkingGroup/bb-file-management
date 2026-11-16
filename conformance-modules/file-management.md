---
title: File Management core
---

# File Management core

## Why choose this conformance module?

Choose File Management when government services need one reliable place for the documents they receive and produce. Citizens' supporting documents and the files officials produce are kept under identifiers that never change, with their earlier versions and the context a service needs to find them again, and are reachable only by those entitled to them. Where the software solution offers it, documents are shared through links and other systems learn when they change.

Because every service integrates with the same interface, a government can replace the software product, and can export every document with its versions and metadata in a documented package.

Every conformant software solution meets the File Management core. The Working Document Collaboration and Records Management extensions add to it without repeating it.

## Example use cases

- **Supporting documents for an application.** A construction permit portal creates a Container for each application and stores the site photos and ownership certificate the applicant uploads. The portal keeps the Container identifier with the application, and the case officer's application lists the Files of that Container.
- **Handing out a document.** The permit office gives an applicant a download link to the issued permit that expires after 30 days.
- **Collecting documents without an account.** A social services office sends a citizen an upload-only link to submit missing evidence.
- **Starting work elsewhere.** A process engine receives an event when a new document arrives and starts the review of the application.
- **Answering a data subject access request.** An official lists every document that concerns a given person, across cases.

## Functionalities

| Functionality | Requirements | REQUIRED | RECOMMENDED |
|---|---|---|---|
| [File Storage](../requirements/file-storage.md) | 22 | 13 | 9 |
| [Metadata and Search](../requirements/metadata-and-search.md) | 17 | 3 | 14 |
| [Access Control](../requirements/access-control.md) | 10 | 4 | 6 |
| [File Sharing](../requirements/file-sharing.md) | 5 | 0 | 5 |
| [Integration and Events](../requirements/integration-and-events.md) | 6 | 0 | 6 |
| [Usage Reporting](../requirements/usage-reporting.md) | 4 | 0 | 4 |
| **Total** | **64** | **20** | **44** |

## Actors relevant for testing

| Actor | Kind | Role in tests | Functionalities |
|---|---|---|---|
| Service application | System | Calls the Service API: stores, retrieves and searches documents, manages Containers, permissions and links, reads reports | File Storage, Metadata and Search, Access Control, File Sharing, Integration and Events, Usage Reporting |
| Administrator | Person or system | Configures size limits, quotas, allow-lists and expiry periods; enables outside services for content analysis | File Storage, Metadata and Search, Usage Reporting |
| Official | Person | Accepts metadata proposals, marks items as protected and approves early purges as a manager of a Container, selects the areas to redact, lists the Files of a data subject | File Storage, Metadata and Search, File Sharing |
| Event subscriber | System | Registers for File events and receives them by webhook, as a process engine would | Integration and Events |
| Link recipient | Person | Opens a download or upload link without an account, as a citizen would | File Sharing |

## Interfaces

| Interface | Counterpart | Direction | Functionalities | Type | Contract defined in |
|---|---|---|---|---|---|
| Document Management API | Service application, administrator | Inbound | All File Management functionalities | Service API | This specification, `resources/api` (to be written) |
| WebDAV access | Clients and service applications | Inbound | Integration and Events (INT-5) | Service API | IETF RFC 4918 |
| Share page | Link recipient | Inbound | File Sharing (ACC-9) | User interface | This specification |
| File events | Event subscriber | Outbound | Integration and Events | Event | This specification |
| Exports and reports | Administrator, other systems | Outbound | File Storage (STO-10), Usage Reporting (RPT-5) | File | This specification |
