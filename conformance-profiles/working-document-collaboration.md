---
title: Working Document Collaboration profile
---

# Working Document Collaboration profile

## Why choose this profile?

Choose Working Document Collaboration when officials and their partners draft and revise documents together. Several people edit the same document at the same time in the browser or on synchronised devices, invite guests and partner organisations without exchanging copies by email, and can always see who changed what.

The profile includes File Management, so every document worked on together is also stored, versioned, findable and protected as in that profile.

## Example use cases

- **A briefing note for the minister.** Three officials write the note at the same time in their browsers; every saved result becomes a new version, and each sees the others' changes.
- **Work on the move.** An inspector synchronises the inspection folder to a laptop, works offline on site and has the changes synchronised back.
- **A consultant contributes.** An external expert edits a draft concept paper through a guest link without getting an account.
- **Inter-ministerial coordination.** A ministry shares the agenda folder of a coordination meeting with a partner ministry through federated sharing; each keeps its own accounts.
- **Who changed what.** Before the meeting, the coordinator checks the activity history to see which sections were changed since the last version.

## Functionalities

| Functionality | From profile | Requirements | REQUIRED | RECOMMENDED |
|---|---|---|---|---|
| [Document Storage](../requirements/document-storage.md) | File Management | 19 | 10 | 9 |
| [Metadata and Search](../requirements/metadata-and-search.md) | File Management | 17 | 3 | 14 |
| [Access Control](../requirements/access-control.md) | File Management | 9 | 4 | 5 |
| [Document Sharing](../requirements/document-sharing.md) | File Management | 7 | 0 | 7 |
| [Integration and Events](../requirements/integration-and-events.md) | File Management | 6 | 0 | 6 |
| [Usage Reporting](../requirements/usage-reporting.md) | File Management | 5 | 0 | 5 |
| [Collaborative Editing](../requirements/collaborative-editing.md) | Working Document Collaboration | 12 | 5 | 7 |
| [Collaboration History](../requirements/collaboration-history.md) | Working Document Collaboration | 3 | 2 | 1 |
| **Total** | | **78** | **24** | **54** |

## Actors relevant for testing

All actors of the File Management profile, plus:

| Actor | Kind | Role in tests | Functionalities |
|---|---|---|---|
| Collaborating official | Person | Edits Working Documents in the browser and through synchronisation clients, receives change notifications, views the activity history | Collaborative Editing, Collaboration History |
| Guest editor | Person | Edits a shared Working Document through a link or guest access without an account | Collaborative Editing |
| Partner organisation's system | System | Exchanges a federated share through Open Cloud Mesh | Collaborative Editing |

## Interfaces

All interfaces of the File Management profile, plus:

| Interface | Counterpart | Direction | Functionalities | Type | Contract defined in |
|---|---|---|---|---|---|
| Web interface and synchronisation clients | Collaborating official, guest editor | Both | Collaborative Editing, Collaboration History | User interface | This specification |
| Federated sharing | Partner organisation's system | Both | Collaborative Editing (WRK-12) | Protocol | Open Cloud Mesh (OCM) |
| Document Management API | Service application | Inbound | Collaborative Editing, Collaboration History | Service API | This specification, `resources/api` (to be written) |
