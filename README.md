# Document Management Building Block — specification draft v3

This folder holds the third draft of the GovStack Document Management Building Block (working name `govstack:spec:bb:dms`, formerly File Management System). It follows the repository layout of `bb-template` (branch `beta/2.0`) and the model of the Specification Framework as proposed in pull request #1 (*Functionalities and Extensions*, ARCH-ADR-7 and ARCH-TDR-1).

## What is where

```sh
.
├── README.md                     # this file
├── CHANGELOG.md                  # changes from draft v2, with the mapping of requirement labels
├── metadata.yml                  # name, URN, capabilities along the document lifecycle, extensions
├── authors.yml
├── toc.yml
├── introduction
│   ├── purpose.md                # Value, capabilities, place in larger systems
│   ├── overview.md               # System under test, functionalities, core and extensions, actors, interfaces
│   ├── scope.md                  # Subject, conformance, relationships, covered, not covered
│   ├── terminology.yml
│   └── references.yml
├── requirements                  # one file per functionality; requirements in the YAML front matter
│   ├── document-storage.md           # core
│   ├── metadata-and-search.md        # core
│   ├── access-control.md             # core
│   ├── document-sharing.md           # core
│   ├── integration-and-events.md     # core
│   ├── usage-reporting.md            # core
│   ├── collaborative-editing.md      # extension: collaboration
│   ├── collaboration-history.md      # extension: collaboration
│   ├── records-capture.md            # extension: records
│   ├── records-processes.md          # extension: records
│   ├── classification-and-retention.md   # extension: records
│   ├── archival-preservation.md      # extension: records
│   ├── records-audit-trail.md        # extension: records
│   ├── document-exchange.md          # extension: records
│   └── issued-documents.md           # extension: records
└── resources
    ├── reference-products.md     # which products the REQUIRED levels were set against
    └── open-questions.md
```

## In numbers

| Part | Functionalities | REQUIRED | RECOMMENDED |
|---|---|---|---|
| Core | 6 | 17 | 46 |
| Working Document Collaboration extension | 2 | 8 | 8 |
| Records Management extension | 7 | 26 | 43 |
| Total | 15 | 51 | 97 |

Ten capabilities are declared in `metadata.yml`, six along the document lifecycle (capture, collaborative authoring, controlled processing, exchange, retention and disposition, long-term preservation) and four that apply at every stage (findability, access protection, accountability, service integration).

## Conventions in this draft

- **Requirement numbers.** Under the Specification Framework a requirement receives its number when it is accepted. All requirements here are `DRAFT` with an empty `id`. The working label from the earlier drafts (STO-1, MET-1, …) is kept as a YAML comment above each requirement, so that comments on drafts v1 and v2 can still be traced.
- **Front matter fields.** Requirement files use the fields of the Specification Framework pull request #1: `description`, `realises`, `conformance`, `extension` and `interaction`. The `bb-template` file `requirements/functionality-name.md` still uses the older fields `capability`, `cardinality` and `type`. See the open questions.
- **Purpose and overview.** `bb-template` keeps the Purpose in its own file, `introduction/purpose.md`, while the framework chapter puts Purpose and Description together in `overview.md`. This draft follows the template: `purpose.md` holds the Purpose and `overview.md` the Description.
- **"Extension", not "optional".** In GovStack usage "optional" means `RECOMMENDED`, so the framework calls the claimable parts *extensions*. Draft v2's "optional extensions" are now simply extensions.
- **No product names in the introduction.** The framework forbids product and vendor names in `purpose.md`, `overview.md` and `scope.md`. The reference products against which the REQUIRED levels were set are therefore listed in `resources/reference-products.md`.
- **Not yet written.** `resources/api` (the Service API in OpenAPI), `api_operation_id` and `test` fields, and the `mutability` classifier, which takes its default (`REPLACEABLE`) until the Working Group decides otherwise.
