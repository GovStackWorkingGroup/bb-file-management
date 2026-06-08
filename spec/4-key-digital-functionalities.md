# 4 Key Functionalities

Definition of Key Functionalities: [https://specs.govstack.global/architecture/5-specification-framework/5.4-specification-template#id-5.4.4-key-functionalities](https://specs.govstack.global/architecture/5-specification-framework/5.4-specification-template#id-5.4.4-key-functionalities)



## Document Life Cycle

### Document Creation

* API or via UI accepting content and creating document
  * Access to predefined templates, and ability to customise templates (e.g. template of information to be submitted to create document, pre-defined set of information)
    * Support for standard metadata schemas like Dublin Core, DCAT-AP, and EIRA — and allow you to create your own custom metadata fields
  * Automapping data from the document into metadata, to reduce manual data duplication, as often metadata content is already inside the file

### Document Storage

#### Information Organisational Architecture

* The DMS should support nested folder structure that follows local legal requirements. For example in Estonia it is: Function → Activity → Record Series → File → Record (or similar, as these might not be well translated..)

#### Versioning

* No change without Versioning
* Automated versioning of all documents on multiple levels
* Option to jump to previous version of a file

#### To be discussed

* Also support "delta storage" — this means storing only the changes between document versions, not the whole file each time. Also label versions as "major" or "minor" (e.g., version 2.0 vs 2.1).
  * Has downsides: a corrupted increment let's the whole file be unsuable

Future – “Files as code” / “Documents as code” (not to confuse with “doc as code”):

* The system shall store documents as declarative source (YAML, JSON, Markdown with frontmatter) + separate rendering to PDF/A.
* The system shall allow retrieval of the “source (code)” form independently from publication formats.
* Provide a schema registry for document-as-code templates (JSON Schema / XML Schema validation).
* Support versioning at the clause/field level (not just whole file).

### Document Collaboration

#### Search

* Robust document search functionality through the metadata captured within the system.
* Allow full-text search inside documents that have been processed by OCR (optical character recognition), and allow searching on any metadata field, including custom fields you create.
* For search I would also add searching from document content, not only metadata, as there is often key data in the content.

#### Sharing

* The system shall allow for document sharing and collaboration among authorised stakeholders.

### Records Management

#### Archiving

The system shall have an inbuilt archival system that:

* Enables efficient search and retrieval of files
* Preserves digital files in compliance with the country’s legal and regulatory requirements.
* Capture all relevant metadata for the archived documents

The archival system shall be designed to handle a large volume of files, ensuring scalability and optimal performance even as the file repository grows over time.

Based on MoReq2010 and OAIS standards

* Retention and disposal schedules: The system must automatically delete or freeze documents after their legal retention period ends, according to rules you define.
* Format migration policy: The system must warn an administrator when a file format is becoming obsolete (e.g., PDF/A-1 is old; the system should suggest migrating to PDF/A-4).
* Support for archival packages: The system must work with SIP (Submission Information Package), AIP (Archival Information Package), and DIP (Dissemination Information Package) these are standard ways of packaging documents for long-term archives.
* Checksum management: Every file must have a SHA-256 checksum (a unique digital fingerprint). The system must periodically verify that files still match their checksum (to detect corruption).
* Legal hold: The system must allow administrators to "freeze" a document so that it cannot be deleted or altered, even if the retention schedule says it should be deleted. This is used when a document is needed for a legal investigation.

#### Delete/Destruction

* Soft Delete
* Hard Delete
  * Restrictions for hard delete for example: Require two admin approvals to delete a file or add a flag to prevent deletion of files by any, even admin, user

## Workflow Engine

1. Predefined workflows that support role based and person based assignments (sometimes you need a workflow where document goes to direct manager, sometimes you need document that goes to role X and sometimes you need a flow where it always goes to specific person)
2. Parallel and ordered steps, can be combined (so you have initially ordered from manager -> manager -> CEO and then parallel for all employees for acknowledgement as most common use case)
3. Good to have - "picking feature". So that document is assigned to whole accountants team and first person in accountants team who will pick it, will handle it and then it is dismissed for others. Or assigments to unit level is maybe better wording..
4. Timings / notifications - for example need to get a doc reviewed periodically, so it sends a notification once per quarter..
5. For the public website: Allow documents to be marked as "not yet published" so only staff can see them. Allow scheduling of publication and automatic removal on a specific date.

## Logging and monitoring

The system shall support the features below without affecting performance of the system.

* Monitoring data and statistics, for example
  * How much storage is being used
  * How many files are uploaded per hour
  * How long it takes to retrieve a document on average
  * Show daily or weekly trends of how many documents are created, changed, or deleted
* Data Analysis and Reporting
* For logging it is important that data is clean from any data that falls under GDPR or otherwise private, but same time we need to have logs, so it should be ID / UUID / obfuscated data
* Both logging and monitoring should cover product itself and also integrations (this integrations part is often overseen)

## User Authentication and Access Control

The system shall provide secure user authentication to ensure only authorised individuals can access.

The solution shall have the provision to integrate with information mediator, identity management, consent, and digital signing solutions.

* Authentication standards to support: SAML and OpenID Connect (OIDC) these allow the system to work with national eID schemes (eIDAS) and European Blockchain Services Infrastructure (EBSI).
* Specify the integration: The FMS must expose REST APIs so that external systems (identity management, consent management, digital signing) can connect to it.

## Permission Management

* Different user roles (e.g., administrators, cabinet and administration staff, citizen) shall be defined with appropriate access levels and permissions.
* Access control shall be granular, allowing administrators to manage user roles and permissions effectively.
* Add a second type of access control called ABAC (Attribute-Based Access Control). Example: "Only people from the Tax Department who have a clearance level of 'confidential' can see tax documents."
* Permission Inheritance
* Optional, dependent on national regulations: Add a "break-glass" procedure this allows a trusted administrator to override access rules in an emergency (e.g., a police investigation). Every such override must be logged.

## Security and Privacy

The system shall prioritise robust security measures to protect sensitive information and prevent unauthorised access.

It shall employ encryption protocols and secure data transmission methods particularly for data storage.

The system shall have secure storage mechanisms and backup procedures to ensure data integrity and availability.

Authorisation layer (who can access what) must be same across UI, API, search. So that same rules are applied always, no matter what mechanism is used to fetch the data

It shall comply with relevant data protection and privacy regulations, safeguarding the confidentiality of information.

* Encryption at rest: Use AES-256 (the strongest standard).
* Encryption in transit: Use TLS 1.3 (the latest secure protocol).
* Data minimization: The system must be able to automatically redact (black out) personal information like national ID numbers or bank account details.
* Right to erasure (GDPR Article 17): When a citizen asks for their data to be deleted, the system must either:
  * Delete the document completely, OR
  * Pseudonymise it (remove all identifying information) and block access
* Privacy Impact Assessment (PIA): The system documentation must include a template for conducting a PIA.

## Audit and System Logs

The system shall maintain an audit trail of user activities and document revisions. Upon the initiation of a service or operation, the system must generate a log entry in the form of a basic audit log. The execution of the operation shall not be possible unless the log entry is created.\
The information to be maintained includes (not limited to),

* User / user role
* Date and Time logged
* Module / Feature Accessed
* Data Capture and Maintenance Actions (Creation, Modification, Deletion, Printing, Search, Retrieval and Monitoring)
* Other actions performed including and not limited to changing access control, process execution, data synchronisation.
* Logs must be immutable once written; they cannot be changed or deleted. This can be done using write-once storage or blockchain anchoring.
* Add a unique operation ID to every log entry. This ID links the log entry to the specific document and the user's session.
* Logs must be exportable in standard formats like CEE (Common Event Expression) or Syslog RFC 5424 so that they can be fed into security monitoring systems (SIEM).
* Log retention period: Keep logs for at least 12 months, or longer if required by your national archives.

## Compliance and Reporting

The solution shall provide reporting capabilities, generating comprehensive statistics on user activities, document statuses and reports.

The system shall allow for data export in standard formats for further analysis and archiving purposes.

The archival system shall provide necessary features for compliance monitoring, ensuring transparency, accountability, and adherence to regulatory requirements.

Predefined reports to include:

* GDPR access request report (shows all documents belonging to a specific citizen)
* Retention schedule compliance report (shows which documents are due for deletion or archiving)
* Inactive documents report (documents not accessed for more than 5 years)
* Unauthorised access attempts summary

Export formats allowed: CSV, JSON, XML, and PDF/A (for human-readable reports)



## Integration and Accessibility

The system shall integrate with existing government systems, such as messaging, communication tools, registries.

It shall support multiple devices and platforms, including desktops, laptops, tablets, and mobile devices, for accessibility and convenience.

The system shall have a user-friendly interface and intuitive navigation to ensure ease of use for all users, including those with varying technical expertise.

**Technical integration standards:**

* Provide a REST API with OpenAPI 3.0 documentation (so other systems know how to connect)
* Optionally support CMIS (Content Management Interoperability Services) a standard for document systems
* Support event-driven integration using Webhooks or Kafka (so other systems are notified when something changes)

**Accessibility standard:** Must meet WCAG 2.1 Level AA (this is required for EU public sector bodies under Directive 2016/2102)

**Design requirement:** The web interface must be responsive (works on phones, tablets, laptops, and desktops)

## Artificial Intelligence Integration

AI can be useful, but it should be optional and have strict boundaries especially in government systems

Where AI can be used safely (low-risk areas)

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top">NO.</td><td valign="top">USED CASE</td><td valign="top">WHAT IT DOES</td><td valign="top">CONSTRAINT</td></tr><tr><td valign="top">1.</td><td valign="top">Auto-classification</td><td valign="top">When a document is uploaded, AI guesses whether it's an invoice, a permit application, a letter, etc.</td><td valign="top">Must run on your own servers (no external AI like ChatGPT). No data sent to third parties.</td></tr><tr><td valign="top">2.</td><td valign="top">Semantic search</td><td valign="top">Instead of matching exact words, the AI understands meaning ("documents about roadworks near Main Street")</td><td valign="top">The mathematical representations (vector embeddings) must be stored locally.</td></tr><tr><td valign="top">3.</td><td valign="top">Anomaly detection</td><td valign="top">AI learns normal user behaviour and alerts if someone suddenly downloads thousands of documents</td><td valign="top">Alert only – no automated blocking.</td></tr><tr><td valign="top">4.</td><td valign="top">Auto-metadata extraction</td><td valign="top">AI pulls out dates, person names, reference numbers from documents</td><td valign="top">A human must review and approve before the metadata is saved.</td></tr></tbody></table>

Note: If you choose to use AI, no document content may ever be sent to an external provider (like OpenAI, Google, or Microsoft). Every action taken by AI must be recorded in the audit log.

## Integration with other Building Blocks

### Digital Signatures

Digital signatures is important part, so maybe in general AIDES support in this spec level? But basically, system should be able to retreive information from signed containers, show files, file contents, sign documents, etc.

### Content Management System

Public website that supports automatic publishing of documents from the system

### Cloud Infrastructure

Any details about infrastructure requirements in terms of hosting requirements, minimum connectivity bandwidth, storage, etc

**1**.Hosting location- On-premise (in country data centre) GDPR compliance.

2\. Network bandwidth- there is a high system uptake (more than 100 users can use the system at the same time)

3\. Business continuity strategy-The system must run on two separate data centres (active-active mode) so if one fails, the other takes over for business continuity or cyber-attacks.

4\. Disaster recovery-Recovery Point Objective (RPO): no more than 15 minutes of data loss. Recovery Time Objective (RTO): system must be back up within 4 hours.

5.Sizing Tool a simple calculator where you can enter:

* Number of users
* Number of documents created per year
* Average file size
* How long to keep documents

The tool then tells you how much storage, bandwidth, and server power you will need.

