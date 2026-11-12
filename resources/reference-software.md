---
title: Reference software
---

# Reference software products

The File Management core is defined based on the commonalities of all software products listed below, the Working Document Collaboration extension by sync-and-share software products, and the Records Management extension by records management software products. No software product has been tested against these statements yet.

| Conformance module | Reference software products | Points to confirm with the vendors |
|---|---|---|
| File Management core | Nextcloud, OpenCloud, CERNBox, Alfresco, Webware | STO-9 in Nextcloud needs team folders; ACC-4 applies to Alfresco and Webware only for the access channels they offer; STO-10 export format in Alfresco and Webware |
| Working Document Collaboration extension | Nextcloud, OpenCloud, CERNBox | WRK-14 and WRK-15 (activity history) in CERNBox; WRK-6 guest editing in OpenCloud; Open Cloud Mesh support in OpenCloud before WRK-12 can become REQUIRED |
| Records Management extension | Alfresco with Governance Services, Webware | REC-1 declaration in process in Alfresco, which declares records as final; view events in ACT-1 need Alfresco audit configuration; PRC-9, RET-6 and RET-8 in Webware |

Nextcloud and OpenCloud are not expected to claim Records Management: OpenCloud described lifecycle management as outside its core scope and is adding only basic retention cleanup (2026-08-31). Alfresco and Webware are not expected to claim Working Document Collaboration, although both offer some collaboration features.
