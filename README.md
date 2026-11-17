# Document Management Building Block — specification draft v0.6 (test branch)

This branch holds a test variant of the draft of the GovStack Document Management Building Block (working name `govstack:spec:bb:dms`, formerly File Management System). It follows the repository layout of `bb-template` (branch `beta/2.0`) and the model of the Specification Framework as proposed in pull request #1 (*Functionalities and Extensions*, ARCH-ADR-7 and ARCH-TDR-1). Its Service API follows the specification maturity and conformance chapters of the Specification Framework (branch `feat/conformance_specification_maturity`) and the GovStack Cross-BB API Design Guide 0.3.0-draft.

## Deliberate deviations from the Specification Framework

This branch deviates from the Specification Framework on purpose, to test an alternative structure:

- **Conformance modules.** The specification is divided into three conformance modules: the File Management core and two extensions, Working Document Collaboration and Records Management. Every conformant software solution meets the core; the extensions add to it without repeating it. The modules are declared in `metadata.yml` under `conformance_modules` and described in the folder `conformance-modules`.
- **No `conformance` and `extension` fields** in the functionality files. Which functionalities belong to a conformance module is stated in `metadata.yml` and on each module page.
- **`technical-overview.md` instead of `overview.md`**, read after the scope. It starts with a market assessment; actors and interfaces are on the module pages.
- **API contract under `api/`.** The Specification Framework places the contract at `resources/api.yml`; the GovStack Cross-BB API Design Guide requires it at `api/openapi.yaml`, with `api/coverage.yaml`. This branch follows the guide, as the Digital Registries specification does, and keeps `resources/api.yml` as a link to the same file.
- **"Building Block Software"** replaces the framework's term for the software being assessed, and the words product and solution always appear as "software product" and "software solution".

## What is where

```sh
.
├── README.md
├── CHANGELOG.md
├── metadata.yml                  # name, URN, capabilities, conformance modules
├── authors.yml
├── toc.yml
├── api                           # Service API (API Design Guide layout)
│   ├── openapi.yaml                  # the contract: File Management core operations (draft)
│   ├── index.yaml                    # API surface inventory
│   ├── coverage.yaml                 # requirement traceability (empty while requirements are DRAFT)
│   ├── README.md
│   └── common
│       └── govstack-openapi-common.yaml  # vendored shared schemas
├── introduction
│   ├── purpose.md                # Value, capabilities, place in larger systems
│   ├── scope.md                  # Subject, conformance, relationships, covered, not covered
│   ├── technical-overview.md     # Market assessment, functionalities, conformance modules
│   ├── references.yml
│   └── terminology.yml
├── conformance-modules           # why choose it, use cases, functionalities, actors, interfaces
│   ├── file-management.md
│   ├── working-document-collaboration.md
│   └── records-management.md
├── requirements                  # one file per functionality; requirements in the YAML front matter
│   ├── file-storage.md               # File Management core
│   ├── metadata-and-search.md            # File Management core
│   ├── access-control.md                 # File Management core
│   ├── file-sharing.md               # File Management core
│   ├── integration-and-events.md         # File Management core
│   ├── usage-reporting.md                # File Management core
│   ├── collaborative-editing.md          # Working Document Collaboration extension
│   ├── collaboration-history.md          # Working Document Collaboration extension
│   ├── records-capture.md                # Records Management extension
│   ├── records-processes.md              # Records Management extension
│   ├── classification-and-retention.md   # Records Management extension
│   ├── archival-preservation.md          # Records Management extension
│   ├── records-audit-trail.md            # Records Management extension
│   ├── document-exchange.md              # Records Management extension
│   └── issued-documents.md               # Records Management extension
└── resources
    ├── api.yml                   # link to api/openapi.yaml (Specification Framework location)
    ├── api-reference.md          # operations, requirement mapping, design decisions, validation
    ├── reference-software.md
    └── open-questions.md
```

## In numbers

| Conformance module | Type | Functionalities | REQUIRED | RECOMMENDED |
|---|---|---|---|---|
| File Management | Core | 6 | 20 | 44 |
| Working Document Collaboration | Extension | 2 | 7 | 8 |
| Records Management | Extension | 7 | 26 | 45 |

## Conventions

- **Requirement numbers.** All requirements are `DRAFT` with an empty `id`. The working label (STO-1, MET-1, …) is kept as a YAML comment above each requirement.
- **Front matter fields.** Functionality files use `description`, `realises` and `interaction` from the Specification Framework pull request #1; `conformance` and `extension` are removed on this branch.
- **No software product names in the introduction.** Reference software is listed in `resources/reference-software.md`.
- **Specification maturity.** `metadata.yml` declares maturity 1. The draft contract names operations for the important requirements of the File Management core only; see `resources/api-reference.md`.
- **Operation links.** A requirement names its operations in `api_operation_id`, as one value or, where it needs several operations, as a list.
- **Not yet written.** API operations for the rest of the core and for the extensions, the `test` fields, and the `mutability` classifier.
