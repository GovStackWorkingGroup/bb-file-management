# API artifacts

| File | Purpose |
|---|---|
| [openapi.yaml](openapi.yaml) | The single DRAFT contract of the Document Management API: OpenAPI 3.1.2, API version `1.0.0-draft`, API Design Guide and ruleset `0.3.0-draft`. It covers the most important operations of the File Management core. |
| [index.yaml](index.yaml) | Inventory of the API surfaces (API Design Guide 4.5). |
| [coverage.yaml](coverage.yaml) | Requirement traceability (API Design Guide 4.6). Empty while all requirements are DRAFT and unnumbered; until then each requirement names its operations in `api_operation_id`. |
| [common/govstack-openapi-common.yaml](common/govstack-openapi-common.yaml) | Shared GovStack schemas `Problem`, `ValidationProblem`, `FieldError` and `PageInfo`, vendored at version `0.1.0-draft` (API Design Guide 2.8). |

`resources/api.yml`, the location the Specification Framework names, is a link to `openapi.yaml`. The API Design Guide requires the canonical file under `api/`.

The operations, the requirements that name them, the design decisions and the validation result are described in [resources/api-reference.md](../resources/api-reference.md).
