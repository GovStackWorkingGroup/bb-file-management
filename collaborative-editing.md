---
title: Collaborative Editing
description: |
  Officials and invited partners draft and revise Working Documents together, at the same time and
  from any device, without exchanging copies by email.
realises: [co-authoring, exchange]
conformance: EXTENSION
extension: collaboration
requirements:
  # WRK-1 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS creates a new, empty Working Document in common office formats."
    api_operation_id:
    test:
  # WRK-2 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: USER_INTERFACE
    statement: "The DMS lets several users edit the same Working Document at the same time in a web browser, through a built-in or connected editor."
    documentation: |
      Constraint: a connected editor MAY be attached through the Web Application Open Platform
      Interface (WOPI).
    api_operation_id:
    test:
  # WRK-3 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS saves the result of a co-editing session as a new Version."
    api_operation_id:
    test:
  # WRK-4 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: USER_INTERFACE
    statement: "The DMS displays a preview of PDF, image and common office formats without downloading the File."
    api_operation_id:
    test:
  # WRK-5 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: USER_INTERFACE
    statement: "The DMS synchronises Containers with desktop and mobile clients and applies the same permissions there as on the web (see ACC-4)."
    documentation: |
      Source: FMS Working Group meeting of 2026-06-01.
    api_operation_id:
    test:
  # WRK-6 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: USER_INTERFACE
    statement: "The DMS lets a person without an account in the organisation edit a shared Working Document through a link or guest access."
    api_operation_id:
    test:
  # WRK-7 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS creates a Working Document from a stored template."
    api_operation_id:
    test:
  # WRK-8 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS locks a File for exclusive editing by one user and releases the lock on request or after a configured time-out."
    api_operation_id:
    test:
  # WRK-9 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS attaches comments to a Working Document and returns them with author and UTC timestamp."
    api_operation_id:
    test:
  # WRK-10 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: USER_INTERFACE
    statement: "The DMS notifies the collaborators on a Working Document when it is changed or commented on."
    api_operation_id:
    test:
  # WRK-11 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS stores a label or comment with a Version."
    api_operation_id:
    test:
  # WRK-12 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: PROTOCOL
    contract: "Open Cloud Mesh (OCM) protocol, IETF draft"
    statement: "The DMS shares a Container with a user at another organisation through Open Cloud Mesh, without a shared user account."
    documentation: |
      Source: FMS Working Group meeting of 2026-06-01. Can become REQUIRED once support in all
      reference products is confirmed.
    api_operation_id:
    test:
  # WRK-13 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS derives a new Working Document from a Records Document as a copy that references its source record."
    documentation: |
      Condition: applies when the solution also claims the Records Management extension. The
      record itself is not changed.
    api_operation_id:
    test:
---

# Description

A Working Document is a Document still being created or revised, editable by several people at once without a mandatory process. Collaborative Editing provides what that needs: creation in common office formats (WRK-1), simultaneous editing in a browser (WRK-2), a new Version for every saved result (WRK-3), previews (WRK-4), synchronisation with desktop and mobile clients (WRK-5) and editing by guests (WRK-6).

Co-editing may be built in or provided by a connected office editor. The DMS remains responsible for storage, Versions and permissions.

Federated sharing through Open Cloud Mesh (WRK-12) lets an organisation share with partners at other institutions while keeping the master copy. A Working Document can also start as a copy of a record (WRK-13), which gives officials an editable draft outside the record's process.

# Workflows

## A briefing note is drafted by three officials

```mermaid
sequenceDiagram
  participant A as Official A
  participant D as DMS
  participant B as Official B
  A->>D: Create Working Document from template (WRK-7)
  A->>D: Share with B as editor (ACC-12)
  A->>D: Edit in browser
  B->>D: Edit in browser at the same time (WRK-2)
  D-->>D: Save result as new Version (WRK-3)
  D-->>A: Notify of B's changes (WRK-10)
```
