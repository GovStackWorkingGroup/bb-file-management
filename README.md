# Document Management Building Block — specification draft v0.5 (test branch)

This branch holds a test variant of the draft of the GovStack Document Management Building Block (working name `govstack:spec:bb:dms`, formerly File Management System). It follows the repository layout of `bb-template` (branch `beta/2.0`) and the model of the Specification Framework as proposed in pull request #1 (*Functionalities and Extensions*, ARCH-ADR-7 and ARCH-TDR-1).

## Deliberate deviations from the Specification Framework

This branch deviates from the Specification Framework on purpose, to test an alternative structure:

- **Conformance modules.** The specification is divided into three conformance modules: the File Management core and two extensions, Working Document Collaboration and Records Management. Every conformant software solution meets the core; the extensions add to it without repeating it. The modules are declared in `metadata.yml` under `conformance_modules` and described in the folder `conformance-modules`.
- **No `conformance` and `extension` fields** in the functionality files. Which functionalities belong to a conformance module is stated in `metadata.yml` and on each module page.
- **`technical-overview.md` instead of `overview.md`**, read after the scope. It starts with a market assessment; actors and interfaces are on the module pages.
- **"Building Block Software"** replaces the framework's term for the software being assessed, and the words product and solution always appear as "software product" and "software solution".

## What is where

```sh
.
├── README.md
├── CHANGELOG.md
├── metadata.yml                  # name, URN, capabilities, conformance modules
├── authors.yml
├── toc.yml
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
│   ├── document-storage.md               # File Management core
│   ├── metadata-and-search.md            # File Management core
│   ├── access-control.md                 # File Management core
│   ├── document-sharing.md               # File Management core
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
    ├── reference-software.md
    └── open-questions.md
```

## In numbers

| Conformance module | Type | Functionalities | REQUIRED | RECOMMENDED |
|---|---|---|---|---|
| File Management | Core | 6 | 17 | 46 |
| Working Document Collaboration | Extension | 2 | 7 | 8 |
| Records Management | Extension | 7 | 26 | 43 |

## Conventions

- **Requirement numbers.** All requirements are `DRAFT` with an empty `id`. The working label (STO-1, MET-1, …) is kept as a YAML comment above each requirement.
- **Front matter fields.** Functionality files use `description`, `realises` and `interaction` from the Specification Framework pull request #1; `conformance` and `extension` are removed on this branch.
- **No software product names in the introduction.** Reference software is listed in `resources/reference-software.md`.
- **Not yet written.** `resources/api` (the Service API in OpenAPI), the `api_operation_id` and `test` fields, and the `mutability` classifier.
