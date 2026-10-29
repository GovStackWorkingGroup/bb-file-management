---
title: Records Processes
description: |
  A Records Document in process is edited, reviewed, approved and signed only by the people
  assigned to each step of a predefined process, in series or in parallel, and is finalized when
  the last step is completed.
realises: [controlled-processing]
conformance: EXTENSION
extension: records
requirements:
  # PRC-1 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS stores records process definitions as steps, each with an action (edit, review, approve or sign) and an assignee (a user, a group or a role)."
    api_operation_id:
    test:
  # PRC-2 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS runs the steps of a records process in series, in parallel or in a combination of both, as the process definition sets."
    api_operation_id:
    test:
  # PRC-3 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS starts a records process when a Records Document is declared in process, using the process the caller chooses or the default of its document type or record class."
    api_operation_id:
    test:
  # PRC-4 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS lets only the editors assigned to the current step change the content of a Records Document in process."
    api_operation_id:
    test:
  # PRC-5 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS makes the next step current only when the current step is completed, and records the step, actor, outcome, comment and UTC timestamp."
    api_operation_id:
    test:
  # PRC-6 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS returns a Records Document to the earlier step named in its process definition when an approver rejects it."
    api_operation_id:
    test:
  # PRC-7 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: USER_INTERFACE
    statement: "The DMS notifies the assignee of a step when that step becomes current."
    api_operation_id:
    test:
  # PRC-8 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS returns the process state of a Records Document in process: its process, its current steps and assignees, and its completed steps."
    api_operation_id:
    test:
  # PRC-9 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS finalizes a Records Document when the last step of its records process is completed."
    api_operation_id:
    test:
  # PRC-10 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS performs every step of a records process through its API, so that the Workflow BB, a service application or an automated agent can drive it."
    api_operation_id:
    test:
  # PRC-11 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS saves each edit made in a step as a new Version that names the step and the editor."
    api_operation_id:
    test:
  # PRC-12 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: USER_INTERFACE
    statement: "The DMS lets the members of a group assigned to an edit step edit the Records Document at the same time."
    api_operation_id:
    test:
  # PRC-13 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS completes a step assigned to a group either when one member completes it or when all members have completed it, as the process definition sets."
    api_operation_id:
    test:
  # PRC-14 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS rejects the deletion of a Records Document in process unless the caller holds records-management permission and supplies a reason, which the DMS records."
    api_operation_id:
    test:
  # PRC-15 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: EVENT
    statement: "The DMS notifies registered subscribers by webhook when a Records Document is declared, moves to another step, is finalized, is amended or is disposed of."
    documentation: |
      Extends INT-1.
    api_operation_id:
    test:
  # PRC-16 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS exposes the configuration of document types, permissions and process definitions through its API."
    api_operation_id:
    test:
  # PRC-17 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: USER_INTERFACE
    statement: "The DMS completes an approve or sign step on behalf of a person through an automated agent only after that person confirms the step."
    documentation: |
      Legal responsibility when an AI assistant acts for a user.
    api_operation_id:
    test:
  # PRC-18 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS assigns a step to the manager of the person who started the process, taken from the organisation's structure."
    api_operation_id:
    test:
  # PRC-19 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS lets one member of a group claim a step assigned to the group, and removes the step from the task lists of the other members."
    api_operation_id:
    test:
  # PRC-20 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS starts a review of a finalized Records Document at the recurring interval set in its document type."
    api_operation_id:
    test:
---

# Description

Records Processes are the intra-system workflows of the DMS: the steps a Records Document passes through between declaration and finalization. Orchestration across systems and Building Blocks stays with the Workflow Building Block or another process engine.

A process definition is a set of steps, each with an action and an assignee (PRC-1), arranged in series, in parallel or both (PRC-2). While a step is current, only its assigned editors may change the content (PRC-4). Every completed step is recorded (PRC-5), a rejection returns the record to an earlier step (PRC-6), and the record is finalized when the last step is completed (PRC-9).

# Workflows

## A building permit decision: A edits, B edits, C approves

```mermaid
sequenceDiagram
  participant A as Case officer A
  participant D as DMS
  participant B as Engineer B
  participant C as Head of unit C
  A->>D: Declare draft decision in process (REC-1, PRC-3)
  A->>D: Edit and complete step 1 (PRC-4, PRC-5)
  D-->>B: Step 2 is current (PRC-7)
  B->>D: Add safety conditions, complete step 2
  D-->>C: Step 3 is current
  alt C rejects
    C->>D: Reject with comment
    D-->>B: Back to step 2 (PRC-6)
  else C approves
    C->>D: Approve
    D-->>D: Finalize (PRC-9)
  end
```

# Data structures

| Process definition field | Type | Notes |
|---|---|---|
| process_id | string | |
| name | string | |
| steps | list of step | |
| step.id | string | |
| step.action | enum | `EDIT`, `REVIEW`, `APPROVE`, `SIGN` |
| step.assignee | object | A user, a group or a role; or the manager of the initiator (PRC-18) |
| step.after | list of step ids | Steps that must be completed first; steps with the same predecessors run in parallel (PRC-2) |
| step.on_reject | step id | Step the record returns to when rejected (PRC-6) |
| step.group_completion | enum | `ANY_MEMBER`, `ALL_MEMBERS` (PRC-13) |
