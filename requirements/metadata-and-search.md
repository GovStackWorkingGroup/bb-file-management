---
title: Metadata and Search
description: |
  Documents carry the context a service needs, such as the case they belong to or the person they
  concern, and officials and services find them again by that context, by their content or by the
  person concerned.
realises: [capture, findability, protection]
requirements:
  # MET-1 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS returns for each File its identifier, name, parent Container, media type, size in bytes, creator, creation time, last modification time and current Version number."
    api_operation_id: retrieveFile
    test:
  # MET-2 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS stores, changes and removes custom metadata as key-value pairs with string values on a File, and returns them with it."
    documentation: |
      Typed values come with a metadata schema (MET-6).
    api_operation_id: [uploadFile, retrieveFile, updateFile]
    test:
  # MET-3 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS returns the Files and Containers whose name or system metadata match a query."
    documentation: |
      Constraint: a query supports at least an exact match per field, a substring match on the name, ranges on times and size, and paged results.
    api_operation_id: searchItems
    test:
  # MET-4 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS returns the Files that match a query on custom metadata values."
    api_operation_id: searchItems
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
      Extends govstack-cfr-data#req-5. Becomes REQUIRED through document types for software solutions that
      claim the Records Management extension (REC-3).
    api_operation_id:
    test:
  # MET-7 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS searches the text content of Files."
    documentation: |
      The software provider declares the languages and scripts the search supports.
      A software solution MAY also search the Files inside compressed archives, such as ZIP files (formerly MET-9).
    api_operation_id:
    test:
  # MET-8 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS returns Files whose name or text content holds a term within one character edit of a query term."
    api_operation_id:
    test:
  # MET-10 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS records the authenticated calling service and the correlation identifier of each upload as system metadata that callers cannot change."
    documentation: |
      Extends govstack-cfr-data#req-9.
    api_operation_id: [uploadFile, retrieveFile]
    test:
  # MET-11 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS records one or more data subject identifiers, each with its scheme, on a File."
    documentation: |
      The scheme names the kind of identifier, such as a national identity number or a reference of the service application.
    api_operation_id:
    test:
  # MET-13 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: AUDITABLE
    interaction: SERVICE_API
    statement: "The DMS returns the metadata of an item mapped to the Dublin Core elements."
    documentation: |
      Conformance evidence a software provider produces: the table that maps the metadata fields of the DMS to the Dublin Core elements.
      Possible contract classifiers: ISO 15836-1:2017, Dublin Core metadata element set
    api_operation_id:
    test:
  # MET-14 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS returns metadata values extracted from the content of an uploaded File as proposals marked with their origin, and stores a proposal as metadata only when a caller accepts it."
    documentation: |
      The origin names the analysis that produced the proposal, such as an extraction rule or a model.
      Safeguard: MET-16 keeps the content inside the deployment during the analysis.
    api_operation_id:
    test:
  # MET-16 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: AUDITABLE
    interaction: INTERNAL
    statement: "The DMS processes document content without sending it to a service outside the deployment unless an administrator enables that service."
    documentation: |
      Condition: applies when the software solution analyses document content.
      Conformance evidence a software provider produces: the architecture description of the components that analyse content, with their network destinations, and the configuration through which an administrator enables or disables external services.
    api_operation_id:
    test:
  # MET-17 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "On an erasure request for a data subject from a caller holding the data subject permission, the DMS purges the Files linked only to that data subject, with their Versions, extracted text and redacted copies, and returns the Files it did not purge with the reason."
    documentation: |
      Right to erasure. The data subject permission is the one of MET-19.
      Files linked to further data subjects, and Records Documents under a retention schedule or a legal hold, are not purged and are returned with the reason. Which rule wins when erasure and retention conflict is an open question.
    api_operation_id:
    test:
  # MET-18 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS searches text that it extracts by optical character recognition from scanned images and PDF files."
    documentation: |
      The software provider declares the languages and scripts the recognition supports.
    api_operation_id:
    test:
  # MET-19 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS lists all Files linked to a data subject for a caller holding the data subject permission."
    documentation: |
      Supports data subject access requests: one query returns every File that concerns a person, across Containers and cases.
      Constraint: the data subject permission is separate from read permission.
      The query is logged as an access decision under govstack-cfr-security#req-3.
    api_operation_id:
    test:
  # MET-20 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS returns a SHA-256 digest of the content of each Version."
    documentation: |
      A service application can verify an upload and later show that the content is unchanged. REC-9 adds verification on request for finalized Versions.
    api_operation_id: [retrieveFile, listFileVersions]
    test:
---

# Description

Metadata gives a document its context. The DMS keeps a fixed set of system metadata for every File (MET-1) and lets services attach their own key-value pairs (MET-2), such as an application number.

Data subject identifiers (MET-11) tie documents to the people they concern, who are not necessarily their uploaders or owners. One query then answers a data subject access request (MET-19), and the same link supports erasure requests (MET-17).

Proposals for metadata (MET-14) may come from automated analysis, including AI models. A proposal is stored only when a caller accepts it. MET-16, which is RECOMMENDED, keeps content inside the deployment unless an administrator enables an outside service. Proposals for document types are in *Records Capture* (MET-15).

# Data structures

A field is of one of three kinds. The DMS sets a system field. A reserved field has a key defined in this specification and a value set by a caller. A custom field has a key chosen by the service application.

| Field | Type | Kind | Notes |
|---|---|---|---|
| identifier | string | system | Stable across renames and moves (STO-3) |
| name | string | system | |
| parent | string | system | Identifier of the parent Container |
| media_type | string | system | IANA media type |
| size | integer | system | Bytes |
| created_at, modified_at | date-time | system | UTC |
| creator | string | system | User or service identity that submitted the File |
| version | string | system | Current Version number |
| digest | string | system | SHA-256 of the current Version (MET-20) |
| source_service, correlation_id | string | system | Set on upload; callers cannot change them (MET-10) |
| sensitivity | string | reserved | Sensitivity classification (ACC-18) |
| data_subjects | list of identifier and scheme | reserved | The persons concerned (MET-11) |
| document_type | string | reserved | Required for Records Documents (REC-3) |
| custom | map of string to string | custom | Key-value pairs of the service application (MET-2); typed values with a schema (MET-6) |
