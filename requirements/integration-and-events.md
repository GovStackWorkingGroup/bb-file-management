---
title: Integration and Events
description: |
  Services, process engines and other Building Blocks act on documents through agreed interfaces
  and learn when documents change, without polling.
realises: [integration]
requirements:
  # INT-1 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: EVENT
    statement: "The DMS delivers an event to each registered subscriber by webhook when a File is created, given a new Version, renamed, moved, deleted, restored or purged."
    documentation: |
      Extends govstack-cfr-architecture#req-14.
      Constraint: a failed delivery is retried.
      Safeguards: INT-3 keeps File names and content out of events, and INT-7 signs each delivery.
    api_operation_id:
    test:
  # INT-2 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS registers event subscriptions, filtered by Container and event kind, through its API."
    documentation: |
      The filter by document type is in *Records Processes* (PRC-15).
    api_operation_id:
    test:
  # INT-3 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: EVENT
    statement: "The DMS includes the event identifier, event kind, item identifier, Container identifier, actor identifier, timestamp and correlation identifier in each event, and leaves out the File name and content."
    api_operation_id:
    test:
  # INT-4 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: INTERNAL
    statement: "The DMS applies configured rules when a File enters a Container; a rule sets a metadata value, adds a tag or moves the File."
    api_operation_id:
    test:
  # INT-5 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS offers access to Containers and Files over WebDAV."
    documentation: |
      Constraint: WebDAV class 1 of IETF RFC 4918.
      Whether the Service API of this specification adopts a WebDAV profile is an open question. Possible contract classifiers IETF RFC 4918, HTTP Extensions for WebDAV
    api_operation_id:
    test:
  # INT-7 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: EVENT
    statement: "The DMS signs each event delivery so that the subscriber can verify its origin and integrity."
    documentation: |
      Condition: applies when the software solution offers events (INT-1).
    api_operation_id:
    test:
---

# Description

The DMS is one component of a larger service system. Two kinds of process logic surround it: intra-system records processes, which run inside the DMS (*Records Processes*), and cross-system orchestration by the Workflow Building Block or another process engine. Events (INT-1 to INT-3, INT-7) are the bridge to the second kind: a new upload can start a process elsewhere, which then calls the DMS back through its API.

INT-3, which is RECOMMENDED, keeps the File name and content out of events, so that a subscriber must still pass Access Control to read a document.

INT-5 names a standard interface that many software products already implement, which lowers the cost of integrating an existing software product.

# Data structures

| Event field | Type | Notes |
|---|---|---|
| event_id | string | Unique per event |
| kind | string | `file.created`, `file.version_created`, `file.renamed`, `file.moved`, `file.deleted`, `file.restored` or `file.purged`; records events are added in *Records Processes* (PRC-15) |
| item_id | string | Identifier of the File |
| container_id | string | |
| actor | string | Identifier of the user, service or automated agent |
| occurred_at | date-time | UTC |
| correlation_id | string | Carried over from the request that caused the event |
