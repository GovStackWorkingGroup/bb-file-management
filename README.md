# Document Management Building Block — specification draft v0.4 (test branch)

This branch holds a test variant of the draft of the GovStack Document Management Building Block (working name `govstack:spec:bb:dms`, formerly File Management System). It follows the repository layout of `bb-template` (branch `beta/2.0`) and the model of the Specification Framework as proposed in pull request #1 (*Functionalities and Extensions*, ARCH-ADR-7 and ARCH-TDR-1).

## Deliberate deviations from the Specification Framework

This branch deviates from the Specification Framework on purpose, to test an alternative structure:

- **Conformance profiles instead of a core and extensions.** Three profiles: File Management, Working Document Collaboration and Records Management. The second and third include File Management. They are declared in `metadata.yml` under `conformance_profiles` and described in the folder `conformance-profiles`.
- **No `conformance` and `extension` fields** in the functionality files. Which functionalities belong to a profile is stated in `metadata.yml` and in each profile file.
- **`technical-overview.md` instead of `overview.md`**, read after the scope. It starts with a market assessment instead of the Building Block Software; actors and interfaces moved to the profile files.
- **"Building Block Software"** replaces "system under test", and the words product and solution always appear as "software product" and "software solution".

## What is where

```sh
.
├── README.md
├── CHANGELOG.md
├── metadata.yml                  # name, URN, capabilities, conformance profiles
├── authors.yml
├── toc.yml
├── introduction
│   ├── purpose.md                # Value, capabilities, place in larger systems
│   ├── scope.md                  # Subject, conformance, relationships, covered, not covered
│   ├── technical-overview.md     # Market assessment, functionalities, conformance profiles
│   ├── references.yml
│   └── terminology.yml
├── conformance-profiles          # why choose it, use cases, functionalities, actors, interfaces
│   ├── file-management.md
│   ├── working-document-collaboration.md
│   └── records-management.md
├── requirements                  # one file per functionality; requirements in the YAML front matter
│   ├── document-storage.md               # File Management
│   ├── metadata-and-search.md            # File Management
│   ├── access-control.md                 # File Management
│   ├── document-sharing.md               # File Management
│   ├── integration-and-events.md         # File Management
│   ├── usage-reporting.md                # File Management
│   ├── collaborative-editing.md          # Working Document Collaboration
│   ├── collaboration-history.md          # Working Document Collaboration
│   ├── records-capture.md                # Records Management
│   ├── records-processes.md              # Records Management
│   ├── classification-and-retention.md   # Records Management
│   ├── archival-preservation.md          # Records Management
│   ├── records-audit-trail.md            # Records Management
│   ├── document-exchange.md              # Records Management
│   └── issued-documents.md               # Records Management
└── resources
    ├── reference-software.md
    └── open-questions.md
```

## In numbers

| Profile | Own functionalities | REQUIRED | RECOMMENDED | Including File Management |
|---|---|---|---|---|
| File Management | 6 | 17 | 46 | – |
| Working Document Collaboration | 2 | 7 | 8 | 24 REQUIRED, 54 RECOMMENDED |
| Records Management | 7 | 26 | 43 | 43 REQUIRED, 89 RECOMMENDED |

## Conventions

- **Requirement numbers.** All requirements are `DRAFT` with an empty `id`. The working label (STO-1, MET-1, …) is kept as a YAML comment above each requirement.
- **Front matter fields.** Functionality files use `description`, `realises` and `interaction` from the Specification Framework pull request #1; `conformance` and `extension` are removed on this branch.
- **No software product names in the introduction.** Reference software is listed in `resources/reference-software.md`.
- **Not yet written.** `resources/api` (the Service API in OpenAPI), the `api_operation_id` and `test` fields, and the `mutability` classifier.
