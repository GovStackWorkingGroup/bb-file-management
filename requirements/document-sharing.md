---
title: Document Sharing
description: |
  Documents reach colleagues, citizens and partners in a controlled way: shared with named people,
  handed out or collected through time-limited links, and withdrawn when no longer needed.
realises: [exchange, protection]
conformance: CORE
extension:
requirements:
  # ACC-8 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS creates a link that gives read access to one item or Container until a set expiry date."
    api_operation_id:
    test:
  # ACC-9 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS requires the password set on a share link before it grants access through that link."
    api_operation_id:
    test:
  # ACC-10 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS creates an upload-only link through which a recipient adds Files to a Container without seeing its contents."
    api_operation_id:
    test:
  # ACC-11 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS revokes a Share so that the access it granted ends immediately."
    api_operation_id:
    test:
  # ACC-12 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS shares an item or Container with a named internal user or group in a viewer or editor role."
    api_operation_id:
    test:
  # ACC-13 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS shares an item with an external collaborator who has no account in the organisation."
    api_operation_id:
    test:
  # ACC-16 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS produces a copy of a document with selected personal data redacted, and keeps the original unchanged."
    documentation: |
      Data minimisation by redaction.
    api_operation_id:
    test:
---

# Description

Document Sharing covers the ways an item leaves its Container's normal permissions: a named share (ACC-12), a share with someone outside the organisation (ACC-13), and links that hand out a document or collect documents (ACC-8, ACC-10). Every share can be withdrawn at once (ACC-11).

The links serve citizen-facing cases: a permit handed out for download, or evidence collected from an applicant without a portal account. Where the service application authenticates the citizen and streams the File itself, neither is needed.

Co-editing with external partners and federated sharing between organisations are in the Working Document Collaboration extension.
