---
title: Collaboration History
description: |
  Collaborators see who created, changed, moved, shared or deleted a Working Document, and when.
realises: [accountability, co-authoring]
conformance: EXTENSION
extension: collaboration
requirements:
  # WRK-14 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS records the creation, each new Version, and each rename, move, share and delete of a Working Document with actor and UTC timestamp."
    documentation: |
      A new Version is a saved change of content, such as a save, an upload of new content or the
      end of a co-editing session (WRK-3). Individual keystrokes are not recorded.
    api_operation_id:
    test:
  # WRK-15 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: REQUIRED
    observability: OBSERVABLE
    interaction: USER_INTERFACE
    statement: "The DMS shows the activity history of a Working Document to its collaborators."
    api_operation_id:
    test:
  # WRK-16 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS returns the activity history of a Working Document through its API."
    api_operation_id:
    test:
---

# Description

Collaboration History is a lighter form of the activity trail that Records Management requires. It records no read events and needs no protection against alteration, but it lets collaborators answer the everyday question of who changed what.

What a software solution records is the creation of a Working Document, each new Version, and each rename, move, share and delete. Comparing two Versions, or the change tracking of the editor, shows what changed in the content.
