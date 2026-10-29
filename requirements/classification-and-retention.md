---
title: Classification and Retention
description: |
  Each record belongs to a class of the organisation's classification scheme, which sets who may
  see it and how long it is kept, and records are destroyed or transferred only after an
  authorised decision.
realises: [retention, protection]
conformance: EXTENSION
extension: records
requirements:
  # RET-1 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS assigns each Records Document, in process or finalized, to one class of a hierarchical classification scheme."
    documentation: |
      The scheme follows local legal requirements and may have several levels, for example
      function, activity, record series and file.
    api_operation_id:
    test:
  # RET-2 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS applies the access rules defined on a class to every Records Document in that class."
    api_operation_id:
    test:
  # RET-3 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS applies to each Records Document the retention period, trigger event and disposition action of its class."
    api_operation_id:
    test:
  # RET-4 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS groups Records Documents into a records aggregation and rejects additions to the aggregation once it is closed."
    api_operation_id:
    test:
  # RET-5 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS rejects the deletion of a finalized Records Document other than through an approved disposition."
    api_operation_id:
    test:
  # RET-6 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS lists the Records Documents whose retention period has ended, for review."
    api_operation_id:
    test:
  # RET-7 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS performs a disposition action only after an authorised user approves it."
    api_operation_id:
    test:
  # RET-9 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS starts a retention period when it receives the trigger event through its API, such as the closure of a case."
    api_operation_id:
    test:
  # RET-10 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS places and lifts a legal hold on Records Documents and suspends their disposition while the hold applies."
    api_operation_id:
    test:
  # RET-11 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS keeps a disposition record with identifier, class, title, action, approver and date after destroying a Records Document."
    api_operation_id:
    test:
  # RET-15 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS destroys a Records Document only after two different authorised users approve the destruction."
    api_operation_id:
    test:
---

# Description

Classification ties each record to a class of the organisation's file plan (RET-1). The class carries the access rules (RET-2) and the retention schedule: the retention period, the event that starts it and the action at its end (RET-3). A records aggregation, such as a case file, groups records whose retention starts together when the aggregation closes (RET-4).

Nothing leaves the regime silently. A finalized record cannot be deleted outside an approved disposition (RET-5); records due for disposition are listed for review (RET-6); every disposition action needs an authorised approval (RET-7). A legal hold suspends disposition (RET-10), and a disposition record remains after destruction (RET-11).

Transfer to an archive, which is one possible disposition action, is described in *Archival Preservation*.

# Workflows

```mermaid
sequenceDiagram
  participant S as Service application
  participant D as DMS
  participant M as Records manager
  S->>D: Case 2026-0412 closed (RET-9)
  D-->>D: Start retention period of the case file (RET-3, RET-4)
  Note over D: Retention period passes
  D-->>M: Records due for review (RET-6)
  M->>D: Approve destruction (RET-7)
  D-->>D: Destroy, keep disposition record (RET-11)
```

# Data structures

| Retention schedule field | Type | Notes |
|---|---|---|
| class_id | string | Class of the classification scheme |
| retention_period | duration | For example ten years |
| trigger_event | string | For example `case.closed`; empty when the period starts at finalization |
| disposition_action | enum | `DESTROY`, `TRANSFER`, `REVIEW` |
| access_rules | list | Applied to every record in the class (RET-2) |
