---
title: File Sharing
description: |
  Documents reach citizens and partners in a controlled way: handed out or collected through
  links, withdrawn when no longer needed, and released as redacted copies.
realises: [exchange, protection]
requirements:
  # ACC-8 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS creates a link that gives read access to one File or Container until an expiry date, when one is set."
    documentation: |
      Safeguards: a password on the link (ACC-9) and revocation (ACC-11).
    api_operation_id:
    test:
  # ACC-9 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: USER_INTERFACE
    statement: "The DMS requires the password set on a share link before it grants access through that link."
    api_operation_id:
    test:
  # ACC-10 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS creates an upload-only link with an expiry date through which a recipient adds Files to a Container without seeing its contents."
    documentation: |
      Safeguard: revocation (ACC-11).
    api_operation_id:
    test:
  # ACC-11 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS revokes a Share so that every later request through it is refused."
    documentation: |
      Condition: applies when the software solution offers any Share.
    api_operation_id:
    test:
  # ACC-16 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS produces a copy of a PDF File in which the areas a user selects are removed from the image, the text layer and the embedded metadata, links the copy to the original, and keeps the original unchanged."
    documentation: |
      Data minimisation by redaction.
    api_operation_id:
    test:
---

# Description

File Sharing covers the ways an item leaves its Container's normal permissions without a grant to a named user: links that hand out a document (ACC-8, ACC-9) or collect documents (ACC-10), and redacted copies (ACC-16). A Share can be revoked (ACC-11); like every requirement of this functionality, revocation is RECOMMENDED.

The links serve citizen-facing cases: a permit handed out for download, or evidence collected from an applicant without a portal account. Where the service application authenticates the citizen and streams the File itself, neither is needed.

Sharing with named users and groups is a grant under *Access Control* (ACC-1). Co-editing with external partners and federated sharing between organisations are in the Working Document Collaboration extension.
