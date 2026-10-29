---
title: Integration and Events
description: |
  Services, process engines and other Building Blocks act on documents through agreed interfaces
  and learn when documents change, without polling.
realises: [integration]
conformance: CORE
extension:
requirements:
  # INT-1 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: EVENT
    statement: "The DMS notifies registered subscribers by webhook when a Document or File is created, updated, moved or deleted."
    documentation: |
      Extends govstack-cfr-architecture#req-14.
    api_operation_id:
    test:
  # INT-2 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS filters event subscriptions by Container, document type and event kind."
    api_operation_id:
    test:
  # INT-3 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: EVENT
    statement: "The DMS includes the identifier, event kind, actor, UTC timestamp and correlation identifier in each event, and leaves out the File content."
    api_operation_id:
    test:
  # INT-4 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: INTERNAL
    statement: "The DMS applies configured rules when an item enters a Container, such as setting metadata, adding a tag or moving the item."
    api_operation_id:
    test:
  # INT-5 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    contract: "IETF RFC 4918, HTTP Extensions for WebDAV"
    statement: "The DMS offers access to Containers and Files over WebDAV."
    documentation: |
      Most candidate products already offer WebDAV. Whether the Service API of this specification
      adopts a WebDAV profile is an open question.
    api_operation_id:
    test:
  # INT-6 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    contract: "OASIS Content Management Interoperability Services (CMIS) Version 1.1"
    statement: "The DMS offers the document and folder services of CMIS."
    documentation: |
      Source: first write-up in bb-file-management.
    api_operation_id:
    test:
---

# Description

The DMS is one component of a larger service system. Two kinds of process logic surround it: intra-system records processes, which run inside the DMS (*Records Processes*), and cross-system orchestration by the Workflow Building Block or another process engine. Events (INT-1 to INT-3) are the bridge to the second kind: a new upload can start a process elsewhere, which then calls the DMS back through its API.

Events carry identifiers, never content (INT-3), so that a subscriber must still pass Access Control to read a document.

INT-5 and INT-6 name standard interfaces that many products already implement, which lowers the cost of integrating an existing product.

# Data structures

| Event field | Type | Notes |
|---|---|---|
| event_id | string | Unique per event |
| kind | string | For example `document.created`, `document.updated`, `document.moved`, `document.deleted`; records events are added in *Records Processes* (PRC-15) |
| item_id | string | Identifier of the Document or File |
| container_id | string | |
| actor | string | User, service or automated agent |
| occurred_at | date-time | UTC |
| correlation_id | string | Carried over from the request that caused the event |
