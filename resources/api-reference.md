---
title: API reference
description: Draft Service API of the File Management core - Containers, Files, Versions, deleted items, search, permission grants, share links and event subscriptions.
---

# API reference

The Document Management API lets service applications, and the people who use them, store, retrieve, find and protect documents. This first draft covers the most important operations of the **File Management core**. The Working Document Collaboration and Records Management extensions have no operations yet.

| | |
|---|---|
| Contract | [`api/openapi.yaml`](../api/openapi.yaml), OpenAPI 3.1.2, API version `1.0.0-draft`, paths under `/v1` |
| Framework location | `resources/api.yml` is a link to the same file |
| API Design Guide | GovStack Cross-BB API Design Guide and ruleset `0.3.0-draft`, declared in `info.x-govstack-api-guide` |
| Shared schemas | `api/common/govstack-openapi-common.yaml`, vendored, version `0.1.0-draft` |
| Traceability | `api_operation_id` in `requirements/*.md`; `api/coverage.yaml` stays empty until requirements are numbered |
| BB code | `document-management`, in problem types, OAuth scopes and event types (to be registered with the API Working Group) |
| Status | DRAFT, not reviewed by the Working Group |

## Specification maturity

The specification stays at **maturity 1**. The contract is not yet complete enough for maturity 2, which needs every `SERVICE_API` requirement to name an operation, a check against at least two software solutions and a domain expert's sign-off. The contract covers every REQUIRED `SERVICE_API` requirement of the core except ACC-4, which applies to all operations and channels and is not one operation. Of the RECOMMENDED requirements, those listed under *Not yet in the contract* have no operation yet.

## Operations

An operation is required for a claim of the File Management core when a REQUIRED requirement names it.

| Group | Operation | Operation id | Method and path | Requirements | Level |
|---|---|---|---|---|---|
| Health | Check that the service is available | `getHealth` | `GET /health` | — | — |
| Containers | Create a Container | `createContainer` | `POST /v1/containers` | STO-4, STO-9 | REQUIRED |
| Containers | Retrieve one Container by its identifier | `retrieveContainer` | `GET /v1/containers/{containerId}` | STO-3, STO-9 | REQUIRED |
| Containers | Update, rename or move a Container | `updateContainer` | `PATCH /v1/containers/{containerId}` | STO-4, STO-9 | REQUIRED |
| Containers | Delete a Container and its contents | `deleteContainer` | `DELETE /v1/containers/{containerId}` | STO-4, STO-8 | REQUIRED |
| Containers | List the items in a Container | `listContainerItems` | `GET /v1/containers/{containerId}/items` | STO-20 | REQUIRED |
| Files | Upload a File into a Container | `uploadFile` | `POST /v1/containers/{containerId}/files` | STO-1, STO-7, STO-12, STO-14, MET-2, MET-10 | REQUIRED |
| Files | Retrieve the details of one File | `retrieveFile` | `GET /v1/files/{fileId}` | STO-3, MET-1, MET-2, MET-10, MET-20 | REQUIRED |
| Files | Update, rename or move a File | `updateFile` | `PATCH /v1/files/{fileId}` | MET-2, ACC-17 | REQUIRED |
| Files | Delete a File | `deleteFile` | `DELETE /v1/files/{fileId}` | STO-8, STO-22 | REQUIRED |
| Files | Download the content of a File | `downloadFileContent` | `GET /v1/files/{fileId}/content` | STO-2 | REQUIRED |
| Files | Replace the content of a File | `replaceFileContent` | `PUT /v1/files/{fileId}/content` | STO-5, STO-7, STO-12, STO-14, STO-25 | REQUIRED |
| Versions | List the Versions of a File | `listFileVersions` | `GET /v1/files/{fileId}/versions` | STO-6, MET-20 | REQUIRED |
| Versions | Download the content of a Version | `downloadFileVersionContent` | `GET /v1/versions/{versionId}/content` | STO-6 | REQUIRED |
| Versions | Restore a Version | `restoreFileVersion` | `POST /v1/versions/{versionId}/restore` | STO-11 | RECOMMENDED |
| Deleted items | List deleted items that can be restored | `listDeletedItems` | `GET /v1/deleted-items` | STO-23 | REQUIRED |
| Deleted items | Restore a deleted item | `restoreDeletedItem` | `POST /v1/deleted-items/{itemId}/restore` | STO-23 | REQUIRED |
| Search | Search Files and Containers | `searchItems` | `POST /v1/items/search` | MET-3, MET-4 | REQUIRED |
| Permissions | List who holds which permissions on an item | `listPermissionGrants` | `GET /v1/items/{itemId}/permission-grants` | ACC-2, ACC-3 | REQUIRED |
| Permissions | Grant permissions on an item | `createPermissionGrant` | `POST /v1/items/{itemId}/permission-grants` | ACC-1 | REQUIRED |
| Permissions | Revoke a permission grant | `revokePermissionGrant` | `DELETE /v1/items/{itemId}/permission-grants/{grantId}` | ACC-1 | REQUIRED |
| Share links | List the share links of an item | `listShareLinks` | `GET /v1/items/{itemId}/share-links` | ACC-11 | RECOMMENDED |
| Share links | Create a share link | `createShareLink` | `POST /v1/items/{itemId}/share-links` | ACC-8, ACC-10 | RECOMMENDED |
| Share links | Revoke a share link | `revokeShareLink` | `DELETE /v1/items/{itemId}/share-links/{shareLinkId}` | ACC-11 | RECOMMENDED |
| Subscriptions | List your event subscriptions | `listSubscriptions` | `GET /v1/subscriptions` | INT-2 | RECOMMENDED |
| Subscriptions | Create an event subscription | `createSubscription` | `POST /v1/subscriptions` | INT-2 | RECOMMENDED |
| Subscriptions | Retrieve one event subscription | `retrieveSubscription` | `GET /v1/subscriptions/{subscriptionId}` | INT-2 | RECOMMENDED |
| Subscriptions | Delete an event subscription | `deleteSubscription` | `DELETE /v1/subscriptions/{subscriptionId}` | INT-2 | RECOMMENDED |
| Subscriptions | Receive a File event | `receiveFileEvent` | Webhook `fileEvent` | INT-1, INT-3 | RECOMMENDED |

A software solution keeps its own paths and operation identifiers and marks each of its operations with `x-govstack-operation` (Specification Framework, *API operations conformance*). The paths above are those of the reference contract.

## Design decisions

The operations follow what the reference software products have in common, expressed in the conventions of the API Design Guide.

| Topic | Decision | Industry practice it follows |
|---|---|---|
| Resources | Separate `containers` and `files`, with permission grants and share links under a common `items` path, because grants and links apply to both | Alfresco and Microsoft Graph (the model of OpenCloud's Libre Graph API) use one node or drive item type; the CS3 APIs of CERNBox distinguish containers and files by a type field. Separate resources keep the schemas simple and the terms of the requirements |
| Identifiers | Opaque, server-assigned, unique within the deployment across Files and Containers, never reused; Version identifiers unique too | Alfresco node ids, Graph item ids, CS3 resource ids and Nextcloud file ids are stable across rename and move, unlike WebDAV paths |
| Upload | One `multipart/form-data` request with a JSON `metadata` part and the `content` part | Alfresco `POST /nodes/{id}/children` with `filedata`; Google Drive multipart upload |
| Content | `GET` and `PUT` on a `content` sub-resource; replacing content adds a Version | Alfresco and Graph `/content`; WebDAV `GET` and `PUT` in Nextcloud, OpenCloud and CERNBox |
| Versions | List per File; download and restore per Version; restore adds a new Version | Alfresco `versions/{id}/revert`, Graph `restoreVersion`, CS3 `RestoreFileVersion`, Nextcloud versions endpoint |
| Deletion | Deleting moves the item to a recoverable state, listed under `deleted-items`, restored with the same identifier | Alfresco trashcan (`deleted-nodes`), Nextcloud and OpenCloud trash bin, CS3 recycle bin |
| Search | `POST /v1/items/search` with typed criteria combined by AND, because criteria can contain personal data | Alfresco `search` API, WebDAV `SEARCH` and `REPORT` in Nextcloud and OpenCloud |
| Permissions | A permission grant names one principal and the permissions `READ`, `WRITE`, `DELETE`, `SHARE`; inherited grants are listed with the Container they come from | Nextcloud share permissions, CS3 grants, Graph permissions with roles, Alfresco permissions with roles (`Consumer`, `Collaborator`, `Coordinator`); adapters map roles to the four permissions |
| Share links | `READ` or `UPLOAD` access, optional expiry and password; the address is returned once | Nextcloud public links and file drop, OpenCloud and Graph `createLink`, CS3 public shares, Alfresco shared links |
| Concurrency | Strong `ETag` on Files and Containers; the content has its own validator (`contentETag`); `If-Match` makes updates and replacements conditional | Graph `eTag` and `cTag`; WebDAV `ETag` with `If-Match` |
| Events | Subscriptions managed through the API; File events delivered as CloudEvents 1.0 by webhook, without File name or content | Nextcloud webhook listeners, Graph subscriptions, Alfresco event gateway; CloudEvents as set by the API Design Guide |
| Errors | RFC 9457 problems with `https://govstack.global/problems/document-management/{slug}`; the size and quota limits are stated as `maxSizeBytes` and `quotaBytes` | `413` for size and `507` for quota, as in WebDAV, Nextcloud and Graph |

## Mapping to the reference software

This is a desk mapping from public documentation, not a test result. The vendors confirm it before the contract can reach maturity 2.

| Operations | Nextcloud | OpenCloud | CERNBox | Alfresco | Webware |
|---|---|---|---|---|---|
| Containers | WebDAV `MKCOL`, `PROPFIND`, `MOVE`, `DELETE`; team folders for STO-9 | Spaces (Libre Graph `drives`) and WebDAV folders | CS3 `CreateContainer`, `Stat`, `ListContainer`, `Move`, `Delete` | `nodes` of type folder | To confirm |
| Files and content | WebDAV `PUT`, `GET`, `PROPFIND`, `PROPPATCH` | WebDAV with TUS uploads; Libre Graph drive items | CS3 `InitiateFileUpload`, `InitiateFileDownload`, arbitrary metadata | `nodes`, `nodes/{id}/content` | To confirm |
| Versions | WebDAV versions endpoint | WebDAV versions (meta) | CS3 `ListFileVersions`, `RestoreFileVersion` | `nodes/{id}/versions` | To confirm |
| Deleted items | WebDAV trash bin | Trash bin per space | CS3 `ListRecycle`, `RestoreRecycleItem` | `deleted-nodes` | To confirm |
| Search | WebDAV `SEARCH` | WebDAV `REPORT` search | To confirm | `search` | To confirm |
| Permission grants | OCS Share API (user and group shares) | Libre Graph `invite` and `permissions` | CS3 grants | Node permissions | To confirm |
| Share links | OCS Share API (public links, file drop) | Libre Graph `createLink` | CS3 public shares | `shared-links` (no upload-only link) | To confirm |
| Subscriptions and events | Webhook listeners app | To confirm | To confirm | Event gateway | To confirm |

An adapter is expected wherever a software product exposes WebDAV, OCS or CS3 interfaces rather than this contract.

## Not yet in the contract

| Requirements | What is missing |
|---|---|
| STO-10, RPT-5 | Export package and report files (`FILE` interfaces with their own format) |
| STO-13 | Resumable uploads; the open questions name the candidate protocol |
| STO-18, STO-19, STO-24 | Protection mark, second approval before an early purge, malware scan status |
| MET-5, MET-6, MET-7, MET-8, MET-13, MET-14, MET-18 | Tags, metadata schemas, full-text and fuzzy search, Dublin Core view, metadata proposals, text recognition |
| MET-11, MET-17, MET-19 | Data subjects, their Files and erasure |
| ACC-5, ACC-7, ACC-15, ACC-16, ACC-18 | Restricting inherited permissions, organisational units and roles, emergency access, redacted copies, sensitivity classification |
| INT-5, INT-7 | WebDAV is defined by IETF RFC 4918; the signing profile of event deliveries |
| RPT-1, RPT-2, RPT-4 | Usage reports |

ACC-4 and ACC-6 apply to every operation: the contract states them in its shared rules and in the `404` answer.

## Validation

Checked on 17 November 2026 with `openapi-spec-validator` 0.9.0 (passes) and the driver of the API Design Guide 0.3.0-draft (`node api-design-guide/linter/cli.mjs --repo-root .`). The driver reports 2 errors, 10 warnings and 4 information findings, all of one of these kinds:

- **Binary downloads.** The linter treats every `GET` whose path does not end in an identifier as a collection, so `downloadFileContent` and `downloadFileVersionContent` are reported as unpaginated collections (12.4 errors; 12.1 and 12.2 warnings), and their `application/octet-stream` answer as a non-JSON media type (9.1). The guide has no rule on binary content yet; this is to be raised with the authors of the guide.
- **Binary bodies.** The binary request of `replaceFileContent` and the binary answers of the two downloads have no example (4.2).
- **Request filters.** `itemType` uses a closed list of values in two request inputs (9.9, information only).

The optional strict profile (`--profile strict`) adds four 5.2 warnings, because `content` and `restore` are not plural nouns: `content` is a single sub-resource of a File or Version, and `restore` an action sub-resource under 5.8.

## Run the checks

From the repository root, with the guide checked out as `api-design-guide/`:

```bash
uv tool install openapi-spec-validator==0.9.0
npm --prefix api-design-guide/linter ci
openapi-spec-validator api/openapi.yaml
node api-design-guide/linter/cli.mjs --repo-root .
```
