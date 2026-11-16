---
title: File Storage
description: |
  Officials, citizens and services hand documents and files to the administration and get them
  back, under an identifier that never changes, with its earlier versions kept and nothing lost
  when a person leaves or the software product is replaced.
realises: [capture]
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
    statement: "The DMS returns the content of a File, byte for byte as submitted, when given its identifier."
    api_operation_id:
    test:
  # STO-3 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS keeps the identifier of a File or Container unchanged when it is renamed, moved, given a new Version or restored after deletion."
    api_operation_id:
    test:
  # STO-4 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS creates, renames, moves and deletes Containers through its API."
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
    documentation: |
      Constraint: a Version is removed only on request of a caller with delete permission or under a configured Version policy.
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
    statement: "The DMS keeps a deleted File or Container restorable for a configured period before purging it."
    documentation: |
      Replaces the rule of govstack-cfr-data#req-7 on hard deletion for this Building Block: the purge after the recovery period is routine, for data minimisation, where the cross-functional requirement permits hard deletion only when a regulation or a data subject request demands it.
      The deletion record of govstack-cfr-data#req-7, with actor, time and method, is inherited and covers each purge.
      Recoverable deletion is REQUIRED here, because a citizen's lost submission is costly to recover.
    api_operation_id:
    test:
  # STO-9 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS assigns each Container to an organisational unit or group with one or more managers, and keeps the Container and its contents manageable when a user account is removed."
    api_operation_id:
    test:
  # STO-10 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: FILE
    statement: "The DMS exports a Container as a package that holds every File in its stored format with its identifier, Versions, metadata and folder structure, described by a documented JSON manifest."
    documentation: |
      Purpose: documents stay usable if the software product is switched off or replaced (exit-first strategy).
      The package is also the archive download of a whole Container (formerly STO-15) and the JSON export of metadata (formerly MET-12).
      Extends govstack-cfr-data#req-8.
    api_operation_id:
    test:
  # STO-20 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS lists the Containers and Files directly inside a Container."
    api_operation_id:
    test:
  # STO-22 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS deletes a File on request of a caller with delete permission."
    api_operation_id:
    test:
  # STO-23 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS lists the deleted Files and Containers that are still restorable and restores one on request, with its identifier, Versions and metadata."
    api_operation_id:
    test:
  # STO-11 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS restores a previous Version by storing its content as a new current Version."
    api_operation_id:
    test:
  # STO-12 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS rejects an upload whose media type, as detected from its content, is not on a configured allow-list."
    api_operation_id:
    test:
  # STO-13 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS accepts resumable uploads, so that an interrupted upload continues from the last byte received."
    documentation: |
      Constraint: the resumable upload protocol is defined with the Service API (`resources/api`, to be written). Until then, two conformant software solutions need not accept the same client.
    api_operation_id:
    test:
  # STO-14 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS rejects an upload that would exceed the storage quota configured for its Container and states the quota in its error response."
    documentation: |
      Constraint: a quota never causes a purge before the recovery period of STO-8 ends.
    api_operation_id:
    test:
  # STO-16 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: INTERNAL
    statement: "The DMS deletes Files automatically when the expiry period configured for their Container has passed since their creation, unless they are marked as protected."
    documentation: |
      The deletion follows STO-8. The protection mark is the one of STO-18.
    api_operation_id:
    test:
  # STO-18 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS rejects the deletion and the automatic deletion of a File or Container that a manager of its Container has marked as protected, until the mark is removed."
    api_operation_id:
    test:
  # STO-19 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS purges a deleted item before the end of its recovery period only after a second manager of its Container approves the purge."
    documentation: |
      Condition: applies when the software solution offers purging before the end of the recovery period.
      Erasure under MET-17 is exempt.
    api_operation_id:
    test:
  # STO-24 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS passes each uploaded File to a configured malware scanner, withholds its content until the scan ends, and rejects or quarantines a File reported as infected."
    api_operation_id:
    test:
  # STO-25 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS rejects a replacement of content that names an expected current Version other than the actual one."
    documentation: |
      Prevents a lost update when two callers replace the content of one File at the same time (STO-5).
    api_operation_id:
    test:
---

# Description

File Storage is the part of the DMS every other functionality relies on. A service application or an official submits a File, and the DMS returns an identifier that stays valid when the File is renamed, moved, given a new Version or restored. Replacing the content never overwrites it.

Files live in Containers, such as folders, team spaces or case files. A Container belongs to an organisational unit or group rather than to one person (STO-9), so that documents survive staff changes. A whole Container can be exported as a package with its Files, their Versions and their metadata (STO-10), so that documents stay usable whatever happens to the software solution.

Deletion is reversible for a configured period. Records Documents follow the stricter deletion rules of *Classification and Retention*.

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

The fields of a File are listed in *Metadata and Search*.

| Item | Fields the DMS returns at minimum |
|---|---|
| Version | Version number, creation time (UTC), author, size in bytes, SHA-256 digest where offered (MET-20) |
| Container | identifier, name, parent Container, owning organisational unit or group, managers (STO-9) |
