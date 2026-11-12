---
title: Working Document Collaboration extension
---

# Working Document Collaboration extension

## Why choose this conformance module?

Choose Working Document Collaboration when officials and their partners draft and revise documents together. Several people edit the same document at the same time in the browser or on synchronised devices, invite guests and partner organisations without exchanging copies by email, and can always see who changed what.

The extension covers collaboration only. A software solution that claims it also meets the File Management core, which stores, versions, finds and protects the documents worked on together.

## Example use cases

- **A briefing note for the minister.** Three officials write the note at the same time in their browsers; every saved result becomes a new version, and each sees the others' changes.
- **Work on the move.** An inspector synchronises the inspection folder to a laptop, works offline on site and has the changes synchronised back.
- **A consultant contributes.** An external expert edits a draft concept paper through a guest link without getting an account.
- **Inter-ministerial coordination.** A ministry shares the agenda folder of a coordination meeting with a partner ministry through federated sharing; each keeps its own accounts.
- **Who changed what.** Before the meeting, the coordinator checks the activity history to see which sections were changed since the last version.

## Functionalities

| Functionality | Requirements | REQUIRED | RECOMMENDED |
|---|---|---|---|
| [Collaborative Editing](../requirements/collaborative-editing.md) | 12 | 5 | 7 |
| [Collaboration History](../requirements/collaboration-history.md) | 3 | 2 | 1 |
| **Total** | **15** | **7** | **8** |

## Actors relevant for testing

Testing this extension assumes the software solution meets the File Management core; the actors of the core are described in `file-management.md`.

| Actor | Kind | Role in tests | Functionalities |
|---|---|---|---|
| Collaborating official | Person | Edits Working Documents in the browser and through synchronisation clients, receives change notifications, views the activity history | Collaborative Editing, Collaboration History |
| Guest editor | Person | Edits a shared Working Document through a link or guest access without an account | Collaborative Editing |
| Partner organisation's system | System | Exchanges a federated share through Open Cloud Mesh | Collaborative Editing |

## Interfaces

The interfaces of the File Management core are described in `file-management.md`.

| Interface | Counterpart | Direction | Functionalities | Type | Contract defined in |
|---|---|---|---|---|---|
| Web interface and synchronisation clients | Collaborating official, guest editor | Both | Collaborative Editing, Collaboration History | User interface | This specification |
| Federated sharing | Partner organisation's system | Both | Collaborative Editing (WRK-12) | Protocol | Open Cloud Mesh (OCM) |
| Document Management API | Service application | Inbound | Collaborative Editing, Collaboration History | Service API | This specification, `resources/api` (to be written) |
