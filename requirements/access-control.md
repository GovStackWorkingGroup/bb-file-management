---
title: Access Control
description: |
  Each document is reachable only by the people and services entitled to it, and the same rules
  hold whichever way it is reached.
realises: [protection]
requirements:
  # ACC-1 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS grants and revokes read, write, delete and share permissions on a File or Container for individual users, groups and service identities."
    documentation: |
      A software solution MAY let a grant carry an expiry date. A grant to a named user or group replaces the named share in a viewer or editor role (formerly ACC-12).
    api_operation_id:
    test:
  # ACC-2 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS applies the permissions of a Container to the items inside it."
    api_operation_id:
    test:
  # ACC-3 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS lists which user, group or service identity holds which permission on an item, to a caller with share permission."
    api_operation_id:
    test:
  # ACC-4 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS applies the same permissions to an item on every access channel the software solution offers."
    documentation: |
      Access channels include the API, search results, events, exports, share pages, the web interface, WebDAV and synchronisation clients.
    api_operation_id:
    test:
  # ACC-5 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS restricts the permissions on an item below those it inherits from its Container."
    api_operation_id:
    test:
  # ACC-6 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS gives the same not-found response for an item the caller may not read as for an item that does not exist."
    api_operation_id:
    test:
  # ACC-7 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS grants permissions by organisational unit and by role."
    api_operation_id:
    test:
  # ACC-15 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS lets a user with override permission override the access rules on one item for a limited time after that user enters a reason."
    documentation: |
      Condition: applies where national rules allow emergency access.
      Constraint: the override is logged with its reason, and the managers of the Container are notified.
    api_operation_id:
    test:
  # ACC-17 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS applies the permissions of the new Container to a moved item and keeps the permissions granted on the item itself."
    api_operation_id:
    test:
  # ACC-18 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS stores a sensitivity classification on each File and Container and returns it with their metadata."
    documentation: |
      Constraint: the levels follow govstack-cfr-data#req-13, which asks for at least public, internal and confidential.
    api_operation_id:
    test:
---

# Description

Access Control decides who may read, change, delete or share an item. Permissions are granted to users, groups and service identities and can be revoked (ACC-1). They are inherited from Containers (ACC-2) and visible to those who manage them (ACC-3). The same rules apply on every channel the software solution offers (ACC-4), so that a document hidden in the web interface cannot be found through search or a synchronisation client.

Authentication, token handling and transport security are inherited from govstack-cfr-security and are not restated here.

A grant to a named user or group is how a document is shared inside the organisation. Links and redacted copies are in *File Sharing*. Records Documents add class-based access rules in *Classification and Retention*.
