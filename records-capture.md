---
title: Records Capture
description: |
  Documents that serve as evidence enter the records regime with a document type, a state and a
  fixed content once finalized, whether they start as an upload, a draft or a set of metadata
  fields.
realises: [capture, controlled-processing, preservation]
conformance: EXTENSION
extension: records
requirements:
  # REC-1 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS declares a Static File or a Working Document a Records Document, either in process or finalized."
    api_operation_id:
    test:
  # REC-2 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS creates a Records Document of a document type from metadata fields alone, with Files as optional attachments."
    documentation: |
      Source: FMS Working Group meeting of 2026-06-01 (a document is a structured set of
      information; files are optional).
    api_operation_id:
    test:
  # REC-3 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS defines document types with typed metadata fields, mandatory fields and a default records process."
    api_operation_id:
    test:
  # REC-4 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS returns the document type and the state, in process or finalized, of each Records Document."
    api_operation_id:
    test:
  # REC-5 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS rejects any change to the content of a finalized Version."
    api_operation_id:
    test:
  # REC-6 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS adds a new Version to a finalized Records Document only through a predefined amendment process, and keeps earlier Versions unchanged and retrievable."
    documentation: |
      Implements integrity in the sense of ISO 15489-1:2016: an authorised addition after creation
      is explicitly indicated and traceable.
    api_operation_id:
    test:
  # REC-7 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS stores signed Files and their detached signatures unchanged and keeps them linked."
    documentation: |
      Creating and validating signatures is the e-Signature Building Block's job. A signature
      applied during a process should be added before finalization, so that the checksum of REC-9
      covers it.
    api_operation_id:
    test:
  # REC-8 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS changes the metadata of a finalized Records Document only for a caller with records-management permission who supplies a reason, and records that reason."
    api_operation_id:
    test:
  # REC-9 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS stores a SHA-256 checksum for each finalized Version and reports on request whether the content still matches it."
    documentation: |
      Source: first write-up in bb-file-management (checksum management).
    api_operation_id:
    test:
  # REC-10 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: FILE
    contract: "ISO 19005, Document management — Electronic document file format for long-term preservation (PDF/A)"
    statement: "The DMS produces an archival rendition in PDF/A at finalization and keeps the original alongside it."
    api_operation_id:
    test:
  # REC-11 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: FILE
    contract: "ETSI EN 319 162-1, Associated Signature Containers (ASiC)"
    statement: "The DMS lists the Files and the signer information inside an ASiC signature container without altering the container."
    documentation: |
      Source: first write-up in bb-file-management (retrieving information from signed
      containers).
    api_operation_id:
    test:
---

# Description

A Records Document is a Document created, received or maintained as evidence of an activity, decision or transaction, in pursuit of legal obligations or in the transaction of business (adapted from ISO 15489-1:2016, 3.14). Purpose, not finality, makes a record: a building permit decision is a record from its first draft.

Records Capture brings items into that regime. A Static File or a Working Document is declared a record (REC-1), either in process, when it still needs editing along a records process, or directly finalized, as with citizen evidence received as submitted. A record may also consist of metadata fields alone (REC-2). Each record has a document type with typed fields and a default records process (REC-3).

Once finalized, a Version never changes (REC-5). Later changes add new Versions through an amendment process (REC-6), which is how ISO 15489's integrity principle allows controlled additions.

# Workflows

```mermaid
stateDiagram-v2
  direction LR
  [*] --> StaticFile: upload (STO-1)
  [*] --> WorkingDocument: create (WRK-1)
  StaticFile --> InProcess: declare (REC-1)
  WorkingDocument --> InProcess: declare (REC-1)
  StaticFile --> Finalized: declare as final (REC-1)
  InProcess --> Finalized: last step completed (PRC-9)
  Finalized --> InProcess: amendment adds a Version (REC-6)
  Finalized --> Disposed: approved disposition (RET-7)
  Disposed --> [*]
```

# Data structures

| Field | Type | Notes |
|---|---|---|
| document_type | string | From the configured document types (REC-3) |
| state | enum | `IN_PROCESS`, `FINALIZED` (REC-4) |
| record_class | string | Class of the classification scheme (RET-1) |
| versions | list | Each finalized Version with its SHA-256 checksum (REC-9) |
| renditions | list | Archival renditions such as PDF/A (REC-10) |
| signatures | list | Detached signatures linked to the signed File (REC-7) |
