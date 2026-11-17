---
title: Open questions
---

# Open questions

## Relating to Specification Framework

- [ ] Mutability: which requirements should be `IMMUTABLE`, for example REC-5 (no change to a finalized Version)?
- [ ] Issued Document Access: should it become an extension of its own that requires the Records Management extension, once its REQUIRED requirements are agreed? An extension without a REQUIRED requirement guarantees nothing.
- [ ] Interaction type of synchronisation clients (WRK-5): `USER_INTERFACE`, as drafted, or a client protocol?

## Content

- [ ] Identifier scope (STO-1): is the identifier unique within the deployment and never reassigned, and does every File sit in a Container, as STO-9 and STO-10 assume? Parked for the Working Group in the review of the File Management core.
- [ ] Service API strategy: v0.6 drafts a GovStack REST API that software products reach directly or through adapters, with WebDAV (INT-5) as an additional channel. Does the Working Group confirm this choice?
- [ ] Process cancellation: when a records process is cancelled, does the Document return to Working Document, stay a Records Document in process, or become a finalized record of the cancelled attempt?
- [ ] Amendment model: does amending a record add a new Version to the same record (REC-6 as drafted), or create a new record that supersedes and links to the old one?
- [ ] Process definitions: who may define records processes, and does a changed definition apply to Records Documents already in process or only to new ones?
- [ ] Static File to Working Document: may a Static File be opened for co-editing and change type, or must a copy be derived?
- [ ] Erasure versus retention: when a data subject requests erasure of a Records Document under retention (MET-17), which rule wins, and how is the decision recorded?
- [ ] Generated documents: when a service generates a certificate PDF, is storing it as a Records Document the service's choice, or should the specification recommend it?
- [ ] Document exchange: which envelope specification should XCH-1 and XCH-2 refer to, beyond document exchange over Information Mediator/X-Road?
- [ ] Documents as code: should a future version require that documents can be stored as declarative source with a separate rendering?

## Relating to the Service API (v0.6)

- [ ] Contract location: the Specification Framework names `resources/api.yml`, the API Design Guide `api/openapi.yaml` with `api/coverage.yaml`. v0.6 follows the guide and keeps `resources/api.yml` as a link. Should the framework adopt the guide's layout?
- [ ] Several operations per requirement: the framework says a `SERVICE_API` requirement "names its operation". v0.6 lists several operations where a requirement needs them, such as STO-4 (create, update and delete a Container). Keep lists, or split such requirements so that each names one operation?
- [ ] Events: INT-1 and INT-3 are of type `EVENT` and name the webhook operation `receiveFileEvent`. Is `api_operation_id` the right field for an event, or `contract`?
- [ ] Coverage: `api/coverage.yaml` traces only numbered requirements. All requirements are DRAFT and unnumbered, so it stays empty. Should DRAFT requirements get provisional identifiers for traceability?
- [ ] BB code: the contract uses `document-management` in problem types, scopes and event types, while the URN uses `dms`. Which code is registered with the API Working Group?
- [ ] Identifier scope (see STO-1): the contract assumes identifiers unique within the deployment across Files and Containers, and Version identifiers unique within the deployment. Does the Working Group agree?
- [ ] Names within a Container: the contract lets a software solution refuse a second item with the same name (`name-conflict`), as WebDAV-based products and Alfresco do. Should the specification require unique names, or allow duplicates?
- [ ] Permissions: the contract uses four permissions (`READ`, `WRITE`, `DELETE`, `SHARE`), as ACC-1 states. Products grant roles (Alfresco `Consumer` to `Coordinator`, Graph `read` and `write`) or permission sets (Nextcloud). Is the mapping by adapters acceptable?
- [ ] Binary content: the API Design Guide has no rule on binary downloads, and its linter reports `GET /v1/files/{fileId}/content` as an unpaginated collection (two errors). To be raised with the authors of the guide.
- [ ] Resumable uploads (STO-13): adopt the tus protocol, which OpenCloud and CERNBox use for uploads, or another protocol?
- [ ] Signed event deliveries (INT-7): which signing profile? The API Design Guide treats signing as optional and profile-specific.
- [ ] Deleting a Container: the contract deletes the Container with its contents and restores them together. Can a single File from a deleted Container be restored on its own?
- [ ] Maturity 2: which two software solutions check the contract, and who signs it off as domain expert?
