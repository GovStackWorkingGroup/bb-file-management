---
title: Open questions
---

# Open questions

## Relating to Specification Framework

- [ ] Mutability: which requirements should be `IMMUTABLE`, for example REC-5 (no change to a finalized Version)?
- [ ] Issued Document Access: should it become an extension of its own that requires Records Management, once its REQUIRED requirements are agreed? An extension without a REQUIRED requirement guarantees nothing.
- [ ] Interaction type of synchronisation clients (WRK-5): `USER_INTERFACE`, as drafted, or a client protocol?

## Content

- [ ] Service API strategy: define a GovStack REST API that candidates reach through adapters, or adopt a WebDAV profile for the core (INT-5)?
- [ ] Process cancellation: when a records process is cancelled, does the Document return to Working Document, stay a Records Document in process, or become a finalized record of the cancelled attempt?
- [ ] Amendment model: does amending a record add a new Version to the same record (REC-6 as drafted), or create a new record that supersedes and links to the old one?
- [ ] Process definitions: who may define records processes, and does a changed definition apply to Records Documents already in process or only to new ones?
- [ ] Static File to Working Document: may a Static File be opened for co-editing and change type, or must a copy be derived?
- [ ] Erasure versus retention: when a data subject requests erasure of a Records Document under retention (MET-17), which rule wins, and how is the decision recorded?
- [ ] Generated documents: when a service generates a certificate PDF, is storing it as a Records Document the service's choice, or should the specification recommend it?
- [ ] Document exchange: which envelope specification should XCH-1 and XCH-2 refer to, beyond document exchange over Information Mediator/X-Road?
- [ ] Documents as code: should a future version require that documents can be stored as declarative source with a separate rendering?
