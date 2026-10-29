---
title: Inter-agency Document Exchange
description: |
  Administrations send records to each other in an agreed envelope through the Information
  Mediator, and register what they receive, instead of exchanging them by email.
realises: [exchange]
conformance: EXTENSION
extension: records
requirements:
  # XCH-1 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: CONSUMED_API
    contract: "govstack:spec:bb:information-mediator"
    statement: "The DMS sends a Records Document with its metadata to another organisation's DMS in an agreed exchange envelope through the Information Mediator BB."
    documentation: |
      Which envelope specification to refer to is an open question.
    api_operation_id:
    test:
  # XCH-2 (working label; the number is issued on acceptance)
  - id:
    status: DRAFT
    level: RECOMMENDED
    observability: OBSERVABLE
    interaction: SERVICE_API
    statement: "The DMS receives Records Documents in the agreed exchange envelope and registers each with its sender and receiver."
    api_operation_id:
    test:
---

# Description

When one administration processes a document and returns it to another, both keep it as a record. Inter-agency Document Exchange lets the DMS of each send and receive records in an agreed envelope, carried over the Information Mediator Building Block. The envelope names at least the sending and receiving organisation or person.

Both requirements are RECOMMENDED until the Working Group agrees on an envelope specification.
