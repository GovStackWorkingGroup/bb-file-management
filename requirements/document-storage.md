---
title: Document Storage
description: |
  Officials, citizens and services hand documents and files to the administration and get them
  back, under an identifier that never changes, with every earlier version kept and nothing lost
  when a person leaves or the product is replaced.
realises: [capture]
conformance: CORE
extension:
requirements:
  # STO-1 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS stores a File submitted through its API and returns a unique identifier."
    api_operation_id:
    test:
  # STO-2 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS returns the content of a File when given its identifier."
    api_operation_id:
    test:
  # STO-3 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS keeps the identifier of a Document or File unchanged when it is renamed or moved to another Container."
    api_operation_id:
    test:
  # STO-4 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS creates, lists, renames, moves and deletes Containers through its API."
    api_operation_id:
    test:
  # STO-5 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS stores replaced content as a new Version under the same identifier."
    api_operation_id:
    test:
  # STO-6 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS lists the Versions of a File and returns the content of any retained Version."
    api_operation_id:
    test:
  # STO-7 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS rejects an upload that exceeds a configured maximum file size and states the limit in its error response."
    api_operation_id:
    test:
  # STO-8 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS keeps a deleted File recoverable for a configured period before purging it."
    documentation: |
      Extends govstack-cfr-data#req-7 from RECOMMENDED to REQUIRED for this Building Block, because a citizen's lost submission is costly to recover.
    api_operation_id:
    test:
  # STO-9 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS assigns a Container to an organisational unit with one or more managers, so that its contents remain available when a user account is removed."
    api_operation_id:
    test:
  # STO-10 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: FILE
    statement: "The DMS exports all Files of a Container, with their folder structure, in open and documented formats."
    documentation: |
      Purpose: documents stay usable if the product is switched off or replaced (exit-first strategy)
    api_operation_id:
    test:
  # STO-11 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS restores a previous Version as the current Version."
    api_operation_id:
    test:
  # STO-12 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS rejects an upload whose media type is not on a configured allow-list."
    api_operation_id:
    test:
  # STO-13 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS accepts resumable uploads, so that an interrupted upload continues from the last byte received."
    api_operation_id:
    test:
  # STO-14 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS enforces a configured storage quota per user, group or Container."
    api_operation_id:
    test:
  # STO-15 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS returns several Files, or a whole Container, as one archive download."
    api_operation_id:
    test:
  # STO-16 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: INTERNAL
    statement: "The DMS deletes Static Files automatically when the retention period configured for their Container has passed."
    api_operation_id:
    test:
  # STO-17 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS labels each Version as a major or a minor Version."
    api_operation_id:
    test:
  # STO-18 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS rejects the deletion of an item that an authorised user has marked as protected, until the mark is removed."
    api_operation_id:
    test:
  # STO-19 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS purges a deleted item before the end of its recovery period only after a second authorised user approves the purge."
    api_operation_id:
    test:
---

# Description

Document Storage is the part of the DMS every other functionality relies on. A service application or an official submits a File, and the DMS returns an identifier that stays valid when the File is renamed or moved. Replacing the content never overwrites it.

Files live in Containers, such as folders, team spaces or case files. A Container belongs to an organisational unit rather than to one person (STO-9), so that documents survive staff changes. The whole content of a Container can be exported with its structure in open formats (STO-10), so that documents stay usable whatever happens to the software solution.

Deletion is reversible for a configured period (STO-8). Optional safeguards add protection marks (STO-18) and a second approval before an early purge (STO-19). Records Documents follow the stricter deletion rules of *Classification and Retention*.

# Workflows

## A citizen's evidence is stored for a case

```mermaid
sequenceDiagram
  participant S as Service application
  participant D as DMS
  S->>D: Create Container for case 2026-0412 (STO-4)
  D-->>S: Container identifier
  S->>D: Upload site photo into the Container (STO-1)
  D-->>S: File identifier, Version 1
  S->>D: Upload a better scan of the same photo (STO-5)
  D-->>S: Same identifier, Version 2
```

# Data structures

| Item | Fields the DMS returns at minimum |
|---|---|
| File | identifier, name, media type, size in bytes, creation time, last modification time (UTC), owner, current Version number (see *Metadata and Search*, MET-1) |
| Version | Version number, major or minor label (STO-17), creation time (UTC), author, size in bytes |
| Container | identifier, name, parent Container, owning organisational unit, managers (STO-9) |
