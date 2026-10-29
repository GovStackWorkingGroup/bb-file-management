---
title: Issued Document Access
description: |
  A record issued to a person, such as a permit or a certificate, becomes the authoritative source
  behind that person's document wallet: requesters fetch it from its source with the person's
  consent, and can check that it is still valid.
realises: [exchange]
conformance: EXTENSION
extension: records
requirements:
  # DOC-1 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS gives each Records Document issued to a person a persistent identifier that resolves for the whole retention period of the document."
    api_operation_id:
    test:
  # DOC-2 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS records the data subjects to whom a Records Document is issued."
    api_operation_id:
    test:
  # DOC-3 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS returns the checksum and the checksum algorithm of an issued document through its API."
    documentation: |
      Purpose: an issuer binds a credential to that exact content. Builds on REC-9.
    api_operation_id:
    test:
  # DOC-4 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS records an issuance status for a Records Document, valid, superseded or revoked, and returns that status without returning the content."
    api_operation_id:
    test:
  # DOC-5 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS releases an issued document to a requester only against a time-limited grant scoped to that document and that requester."
    documentation: |
      The grant is created by a requester gateway after it has checked the holder's presentation. The gateway is described in the Trust Framework Reference Architecture, not in this specification.
    api_operation_id:
    test:
  # DOC-6 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS records each release of an issued document with requester, grant reference and UTC timestamp, and lists the releases for the data subject."
    api_operation_id:
    test:
  # DOC-7 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: EVENT
    statement: "The DMS publishes an event when a document is issued, superseded or revoked."
    documentation: |
      Extends PRC-15.
    api_operation_id:
    test:
  # DOC-8 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: FILE
    statement: "The DMS produces a downloadable copy of an issued document that carries its persistent identifier as a machine-readable code, such as a QR code."
    documentation: |
      Purpose: a printed copy can be checked against its source.
    api_operation_id:
    test:
  # DOC-9 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS provides each data subject with a private Container for self-uploaded documents that only that data subject can read and share."
    api_operation_id:
    test:
---

# Description

In a document wallet, the person's wallet usually holds a reference to a document, not a copy. The document stays with the administration that issued it, which is the authoritative source; a requester, such as a bank or a university, fetches it from there with the person's consent and checks it against a checksum the issuer put into a credential.

The DMS of the issuing administration is that source. It never talks to the Wallet Building Block directly: an issuing service sits between them, and a requester gateway creates the grant under which the DMS releases a document (DOC-5).

All requirements are RECOMMENDED for now. Once the Working Group agrees on the REQUIRED ones, this functionality may become an extension of its own that requires Records Management.

# Workflows

```mermaid
sequenceDiagram
  participant I as Issuing service
  participant D as DMS of the issuing administration
  participant W as Citizen's wallet
  participant R as Requester
  participant G as Requester gateway
  I->>D: Read issued record, identifier and checksum (DOC-1, DOC-3)
  I->>W: Credential with identifier and checksum
  W->>R: Presentation, with the holder's consent
  R->>G: Request access
  G->>D: Create grant for this document and requester
  R->>D: Fetch document with the grant (DOC-5)
  D-->>R: Document, release recorded (DOC-6)
  R-->>R: Check content against the checksum
```
