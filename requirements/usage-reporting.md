---
title: Usage Reporting
description: |
  Administrators and auditors see how the document stock develops and where access was refused, so
  that capacity, housekeeping and security issues are noticed early.
realises: [accountability]
requirements:
  # RPT-1 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS reports the storage used per Container and in total."
    documentation: |
      The figures count current Versions, earlier Versions and deleted Files that are still restorable.
    api_operation_id:
    test:
  # RPT-2 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS reports the number of items created, changed and deleted per day for a requested period."
    api_operation_id:
    test:
  # RPT-4 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS summarises refused access attempts per period, by user and by item, for a caller holding an audit permission."
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

Usage Reporting gives administrators figures on how the document stock develops and where access was refused. Two related lists are covered elsewhere: all Files about one person (MET-19) and the records due for review (RET-6).

Technical monitoring of the running service, such as response times and availability, is inherited from the cross-functional requirements and is not restated.
