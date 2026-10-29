---
title: Scope
---

# Scope

## Subject and applicability

This document specifies the Document Management Building Block, a software component that stores the documents and files of government services and administrations, keeps their metadata and versions, controls who may reach them and, when the solution claims the extensions, supports collaborative editing of Working Documents and the management of Records Documents.

It is applicable to any software solution claiming conformance to `govstack:spec:bb:dms`.

A conformant solution meets the core of this document. It may also claim one or both of these extensions, and meets every requirement of each extension it claims:

- Working Document Collaboration: editing Working Documents at the same time in a browser and on synchronised devices, with guests and partner organisations, and seeing who changed what.
- Records Management: managing Records Documents from declaration through predefined processes, finalization, classification and retention to disposition or archival transfer, with a complete audit trail.

## Relationships

This document extends `govstack:spec:cfr`. A conformant solution meets the requirements of both.

The Document Management Building Block performs no role in a Domain Reference Architecture yet; none exists for document and records management. In `govstack:ra:credentials` it serves as the authoritative source behind a Credential Issuer for issued documents, through *Issued Document Access* in the Records Management extension.

## Covered

**Core**

- **Document Storage**: storing Files under stable identifiers, Versions, Containers owned by organisational units, recoverable deletion and export in open formats
- **Metadata and Search**: system and custom metadata, search by metadata and content, data subject links and erasure
- **Access Control**: permissions for users, groups, organisational roles and attributes, applied the same way on every access channel
- **Document Sharing**: shares with named users, external collaborators and through upload and download links, and redacted copies
- **Integration and Events**: document events, rules on entering a Container, WebDAV and CMIS access
- **Usage Reporting**: storage, activity, inactivity and refused-access reports

**Working Document Collaboration extension**

- **Collaborative Editing**: creating, co-editing, previewing, synchronising and sharing Working Documents, including federated sharing through Open Cloud Mesh
- **Collaboration History**: the history of changes to Working Documents shown to their collaborators

**Records Management extension**

- **Records Capture**: declaring records, document types, record states, integrity of finalized Versions, signatures and archival renditions
- **Records Processes**: predefined edit, review, approve and sign steps in series and in parallel, up to finalization
- **Classification and Retention**: classification schemes, retention schedules, legal holds and authorised disposition
- **Archival Preservation**: organisational archive, integrity checks, format risk reports and transfer packages for an archive
- **Records Audit Trail**: the complete, tamper-evident activity trail of Records Documents
- **Inter-agency Document Exchange**: this Building Block's side of the exchange of records between administrations through the Information Mediator
- **Issued Document Access**: this Building Block's side of access to issued documents for document wallets, as described in `govstack:ra:credentials`

## Not covered

| Excluded | Owned by |
|---|---|
| Authentication, identity proofing and token handling | `govstack:spec:bb:identity` and `govstack:spec:cfr` |
| Orchestration of processes across systems and Building Blocks | `govstack:spec:bb:workflow`, or another process engine |
| Creating and validating electronic signatures and seals | `govstack:spec:bb:e-signature` |
| Generating documents, such as certificates, from data | The service application |
| Publishing documents on public websites | A Content Management System Building Block |
| Notifying citizens by email or SMS | `govstack:spec:bb:messaging` |
| Structured registry data about persons, businesses or assets | `govstack:spec:bb:digital-registries` |
| Records of consent to process personal data | `govstack:spec:bb:consent` |
| Holding credentials for citizens; credential schemas; the requester gateway | `govstack:spec:bb:wallet` and `govstack:ra:credentials` |
| Transport of exchanged documents between administrations | `govstack:spec:bb:information-mediator` |
| Operation of the central government archive | The adopting government's archive authority |
| Retention periods, classification schemes and the legal effect of a record | The adopting government |
| Hosting, backup, disaster recovery and capacity | `govstack:spec:cfr` and the deployment |
| Service applications that use the Building Block | The country's Digital Service System |

## Ownership

Owned by the Document Management Working Group
