---
title: Access Control
description: |
  Each document is reachable only by the people and services entitled to it, and the same rules
  hold whichever way it is reached.
realises: [protection]
conformance: CORE
extension:
requirements:
  # ACC-1 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS grants read, write, delete and share permissions on a Document, File or Container to individual users and to groups."
    api_operation_id:
    test:
  # ACC-2 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS applies the permissions of a Container to the items and Containers inside it."
    api_operation_id:
    test:
  # ACC-3 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS lists which user or group holds which permission on an item or Container, to a caller with share permission."
    api_operation_id:
    test:
  # ACC-4 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS applies the same permissions to an item in its web interface, its API, its search results, WebDAV access and synchronisation clients."
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
    statement: "The DMS grants permissions by organisational unit and role, such as manager or employee, taken from the organisation's structure."
    api_operation_id:
    test:
  # ACC-14 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS grants access to an item based on attributes of the person and of the item, such as the person's department and the item's security classification."
    api_operation_id:
    test:
  # ACC-15 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS lets a designated user override access rules in an emergency only after that user enters a reason, and records each override with the reason."
    documentation: |
      Condition: applies where national rules allow emergency access.
    api_operation_id:
    test:
---

# Description

Access Control decides who may read, change, delete or share an item. Permissions are granted to users and groups (ACC-1), inherited from Containers (ACC-2) and visible to those who manage them (ACC-3). The same rules apply on every channel the software solution offers (ACC-4), so that a document hidden in the web interface cannot be found through search or a synchronisation client.

Authentication, token handling and transport security are inherited from govstack-cfr-security and are not restated here.

The RECOMMENDED requirements add finer models: restrictions below the inherited level (ACC-5), organisational roles (ACC-7), attribute-based rules such as clearance levels (ACC-14) and a recorded emergency override (ACC-15). ACC-6 keeps callers from learning which items exist by probing identifiers.

Sharing with named people and links is in *Document Sharing*. Records Documents add class-based access rules in *Classification and Retention*.
