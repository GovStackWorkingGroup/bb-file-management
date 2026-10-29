---
title: Usage Reporting
description: |
  Administrators and auditors see how the document stock develops and where access was refused, so
  that capacity, housekeeping and security issues are noticed early.
realises: [accountability]
conformance: CORE
extension:
requirements:
  # RPT-1 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS reports the storage used per Container and in total."
    documentation: |
      Source: first write-up in bb-file-management (monitoring and statistics).
    api_operation_id:
    test:
  # RPT-2 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS reports the number of items created, changed and deleted per day and per week."
    api_operation_id:
    test:
  # RPT-3 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS lists the items that nobody has accessed for a configured period."
    api_operation_id:
    test:
  # RPT-4 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS summarises refused access attempts per period, by user and by item."
    api_operation_id:
    test:
  # RPT-5 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: FILE
    statement: "The DMS exports its reports in CSV and JSON."
    api_operation_id:
    test:
---

# Description

Usage Reporting gives administrators the figures the first write-up asked for: storage used, creation and deletion trends, inactive documents and refused access attempts. Two further reports from that write-up are covered elsewhere: the list of all documents about one person (MET-11) and the list of records due for review (RET-6).

Technical monitoring of the running service, such as response times and availability, is inherited from the cross-functional requirements and is not restated.
