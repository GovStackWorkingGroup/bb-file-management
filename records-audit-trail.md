---
title: Records Audit Trail
description: |
  Every action on a record, including views, approvals and signatures, can be traced to a person,
  or to an automated agent acting for one, and a time, in a trail that cannot be altered
  unnoticed.
realises: [accountability]
conformance: EXTENSION
extension: records
requirements:
  # ACT-1 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: AUDITABLE
    interaction: INTERNAL
    statement: "The DMS records each create, view, download, update, move, permission change, process step, approval, signature and deletion of a Records Document with the actor and a UTC timestamp."
    documentation: |
      Extends govstack-cfr-data#req-9. Evidence a vendor produces: a sample activity log covering
      each listed action, and the configuration that enables it.
    api_operation_id:
    test:
  # ACT-2 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS returns the activity history of a Records Document through its API to a caller entitled to see it."
    api_operation_id:
    test:
  # ACT-3 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS records the reason for a permission change or a deletion when the caller supplies one."
    api_operation_id:
    test:
  # ACT-4 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: FILE
    statement: "The DMS exports activity records for a period in a machine-readable format."
    api_operation_id:
    test:
  # ACT-5 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: AUDITABLE
    interaction: INTERNAL
    statement: "The DMS protects the activity trail of Records Documents against alteration, so that any change or deletion of an entry is detectable."
    documentation: |
      Evidence a vendor produces: a description of the integrity mechanism, such as hash chaining
      or write-once storage, and a verification run.
    api_operation_id:
    test:
  # ACT-6 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS records whether a person performed an action directly or an automated agent performed it on the person's behalf, and which agent."
    documentation: |
      Source: FMS Working Group meeting of 2026-06-01.
    api_operation_id:
    test:
  # ACT-7 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: AUDITABLE
    interaction: INTERNAL
    statement: "The DMS refuses an operation on a Records Document when it cannot write the activity record for that operation."
    documentation: |
      Source: first write-up in bb-file-management (no operation without a log entry). Evidence a
      vendor produces: a description of how the operation and its activity record are written
      together, and a test that shows an operation is refused when logging fails.
    api_operation_id:
    test:
  # ACT-8 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: FILE
    contract: "IETF RFC 5424, The Syslog Protocol"
    statement: "The DMS exports activity records in the syslog format."
    documentation: |
      Source: first write-up in bb-file-management (export for security monitoring systems).
    api_operation_id:
    test:
  # ACT-9 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: AUDITABLE
    interaction: INTERNAL
    statement: "The DMS keeps activity records for a configured period of at least twelve months."
    documentation: |
      Evidence a vendor produces: the retention configuration of the activity trail. Source: first
      write-up in bb-file-management.
    api_operation_id:
    test:
  # ACT-10 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: AUDITABLE
    interaction: INTERNAL
    statement: "The DMS identifies persons and documents in activity records by identifier, without names or document content."
    documentation: |
      Source: first write-up in bb-file-management (logs free of personal data).
    api_operation_id:
    test:
---

# Description

The Records Audit Trail is the strict counterpart of *Collaboration History*. It records reads and downloads as well as changes (ACT-1), so that the DMS can show who saw a record, not only who changed it. It distinguishes actions of a person from actions of an automated agent acting for that person (ACT-6).

The RECOMMENDED requirements make the trail harder to dispute: protection against alteration (ACT-5), no operation without its record (ACT-7), a minimum retention (ACT-9) and identifiers instead of personal data (ACT-10). Security event logging stays with govstack-cfr-security#req-7.
