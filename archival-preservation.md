---
title: Archival Preservation
description: |
  Records stay authentic and readable for decades, move to an organisational archive when their
  active use ends, and are handed over to the central archive in a standard package with their
  context.
realises: [preservation]
conformance: EXTENSION
extension: records
requirements:
  # RET-8 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: FILE
    statement: "The DMS exports Records Documents with their metadata, process history and activity trail as a transfer package for an archive."
    api_operation_id:
    test:
  # RET-12 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS moves finalized Records Documents that are no longer in active use to an organisational archive with restricted access."
    documentation: |
      Source: FMS Working Group meeting of 2026-08-31 (creation and use, organisational archive,
      central government archive).
    api_operation_id:
    test:
  # RET-13 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: FILE
    contract: "E-ARK Submission Information Package (SIP) specification"
    statement: "The DMS produces transfer packages as E-ARK Submission Information Packages."
    api_operation_id:
    test:
  # RET-14 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: FILE
    statement: "The DMS leaves out the metadata fields marked as not for transfer when it produces a transfer package."
    documentation: |
      Source: FMS Working Group meeting of 2026-08-31 (data reduction at each handover).
    api_operation_id:
    test:
  # RET-16 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: INTERNAL
    statement: "The DMS verifies the checksums of finalized Versions at a configured interval and reports every mismatch."
    documentation: |
      Source: first write-up in bb-file-management (periodic integrity checks). Builds on REC-9.
    api_operation_id:
    test:
  # RET-17 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS reports Records Documents stored in a format that an administrator has marked as at risk of obsolescence, with the target format configured for it."
    documentation: |
      Source: first write-up in bb-file-management (format migration policy).
    api_operation_id:
    test:
---

# Description

The FMS Working Group described a three-phase archiving model: creation and use, an organisational archive, and the central government archive, with data reduced at each handover. Archival Preservation supports the DMS's part of it.

Records whose active use has ended move to a restricted organisational archive (RET-12). When the retention schedule says transfer, the DMS produces a transfer package with the records, their metadata, process history and activity trail (RET-8), preferably in the E-ARK SIP format (RET-13), leaving out fields not meant for the archive (RET-14).

Between capture and transfer, the DMS keeps records readable and intact: periodic checksum verification (RET-16) detects corruption, and format reports (RET-17) show which records need migration before their format becomes obsolete. Operating the central archive itself is outside this specification.
