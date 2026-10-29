---
title: Metadata and Search
description: |
  Documents carry the context a service needs, such as the case they belong to or the person they
  concern, and officials and services find them again by that context, by their content or by the
  person concerned.
realises: [capture, findability, protection]
conformance: CORE
extension:
requirements:
  # MET-1 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS returns for each File its identifier, name, media type, size in bytes, creation time, last modification time in UTC, owner and current Version number."
    api_operation_id:
    test:
  # MET-2 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS stores custom metadata as key-value pairs on a Document or File and returns them with it."
    api_operation_id:
    test:
  # MET-3 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS returns the Documents and Files that match a query on name or system metadata, limited to those the caller may read."
    api_operation_id:
    test:
  # MET-4 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS returns the Documents and Files that match a query on custom metadata values."
    api_operation_id:
    test:
  # MET-5 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS assigns tags from a managed vocabulary and filters items by tag."
    api_operation_id:
    test:
  # MET-6 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS validates custom metadata against a configured schema with typed and mandatory fields."
    documentation: |
      Extends govstack-cfr-data#req-5. Becomes REQUIRED through document types for solutions that
      claim the Records Management extension (REC-3).
    api_operation_id:
    test:
  # MET-7 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS searches the text content of Files, including text that it extracts by optical character recognition from scanned images and PDF files."
    api_operation_id:
    test:
  # MET-8 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS returns search results for a query that contains spelling errors, such as a mistyped name."
    documentation: |
      Source: FMS Working Group meeting of 2026-06-01.
    api_operation_id:
    test:
  # MET-9 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS searches the content of Files inside compressed archives, such as ZIP files."
    documentation: |
      Source: FMS Working Group meeting of 2026-06-01.
    api_operation_id:
    test:
  # MET-10 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS records the submitting service application and the correlation identifier of each upload as metadata."
    documentation: |
      Extends govstack-cfr-data#req-9.
    api_operation_id:
    test:
  # MET-11 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS records one or more data subject identifiers on a Document or File and lists all items linked to a given data subject."
    documentation: |
      Supports data subject access requests: one query returns every item that concerns a person,
      across Containers and cases.
    api_operation_id:
    test:
  # MET-12 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: FILE
    statement: "The DMS exports the metadata of a Document, File or Container in JSON."
    documentation: |
      Extends govstack-cfr-data#req-8.
    api_operation_id:
    test:
  # MET-13 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    contract: "ISO 15836-1:2017, Dublin Core metadata element set"
    statement: "The DMS returns the metadata of an item mapped to the Dublin Core elements."
    documentation: |
      Source: first write-up in bb-file-management.
    api_operation_id:
    test:
  # MET-14 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS proposes metadata values extracted from the content of an uploaded File, such as dates, names and reference numbers, and stores them only after a person confirms them."
    documentation: |
      Source: first write-up in bb-file-management (automatic metadata extraction with human
      review).
    api_operation_id:
    test:
  # MET-15 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS proposes a document type for an uploaded File and assigns it only after a person confirms the proposal."
    documentation: |
      Source: first write-up in bb-file-management (automatic classification).
    api_operation_id:
    test:
  # MET-16 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: AUDITABLE
    interaction: INTERNAL
    statement: "The DMS processes document content for proposals and search without sending it to a service outside the deployment."
    documentation: |
      Evidence a vendor produces: the architecture description of the components that analyse
      content, with their network destinations, and the configuration that disables external
      services.
    api_operation_id:
    test:
  # MET-17 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "On an authorised erasure request for a data subject, the DMS deletes or pseudonymises the items linked to that data subject, except items under a retention period or a legal hold."
    documentation: |
      Source: first write-up in bb-file-management (right to erasure). Which rule wins when
      erasure and retention conflict is an open question.
    api_operation_id:
    test:
---

# Description

Metadata gives a document its context. The DMS keeps a fixed set of system metadata for every File (MET-1) and lets services attach their own key-value pairs (MET-2), such as an application number. Search by name and system metadata is REQUIRED; search by custom metadata, by content, with spelling tolerance and inside compressed archives is RECOMMENDED.

A service application that needs every document of one case can rely on a Container per case (STO-4) even when it cannot search custom metadata.

Data subject identifiers (MET-11) tie documents to the people they concern, who are not necessarily their uploaders or owners. One query then answers a data subject access request, and the same link supports erasure requests (MET-17).

Proposals for metadata and document types (MET-14, MET-15) may come from automated analysis, including AI models. They are stored only after a person confirms them, and content is never sent outside the deployment for that purpose (MET-16).

# Data structures

| Field | Type | Kind | Notes |
|---|---|---|---|
| identifier | string | system | Stable across renames and moves (STO-3) |
| name | string | system | |
| media_type | string | system | IANA media type |
| size | integer | system | Bytes |
| created_at, modified_at | date-time | system | UTC |
| owner | string | system | User or organisational unit |
| version | string | system | Current Version number |
| document_type | string | custom | Required for Records Documents (REC-3) |
| data_subjects | list of strings | custom | Identifiers of the persons concerned (MET-11) |
| source_service, correlation_id | string | custom | Set on upload (MET-10) |
| custom | map of string to value | custom | Further key-value pairs (MET-2) |
