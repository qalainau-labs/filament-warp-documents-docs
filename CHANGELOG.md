# Changelog

All notable changes to `qalainau/filament-warp-documents` are documented in this file.

## [1.0.0] - 2026-11-16

### Added

- First release of Warp Documents: document control for Filament v5 panels.
- Documents with a number, type, folder and owner, kept as revisions. A revision is a file (PDF, Word, Excel, images or anything else) or a page written in the panel. A new revision is a draft that only its author and approvers see; the current revision stays in use until the new one is approved.
- Check-out and check-in, so two people do not revise the same document at once.
- Built-in approval: approvers by person or group, one after another or all at once, send back and resubmit. Nobody approves their own revision. Optional password signatures (`->signatures()`).
- Approval through Warp Flow (`->flowApprovals('documents')` with `ApprovableVersion`), when Warp Flow is installed. Without Warp Flow the built-in approval is used.
- Effective dates, and a SUPERSEDED or OBSOLETE watermark on old revisions. Documents can be made obsolete.
- Readers (everyone, groups or people) confirm “I have read and understood” each new revision; minor corrections need no new confirmation. Due dates, progress and reminders. An optional comprehension check asks a few multiple-choice questions before confirming (`Lifecycle::acknowledge()` takes the answers).
- Periodic reviews from the document type, expiry dates for certificates and licences, and a daily `warp-documents:remind` command (`->reminders()`).
- Redline compare: pages show removed words struck through and added words underlined; files side by side with their details.
- Controlled copies: “Print controlled copy” stamps the PDF with its copy number, holder, printer and date and keeps a register. When a new revision takes effect, the old copies are listed for collection. `->copyCheck()` adds a QR code that opens a public page saying whether that paper is still current.
- Word, Excel and PowerPoint files shown as PDF (`->convertToPdf()` with `LibreOfficeConverter`, `GotenbergConverter` or your own closure, optionally on a queue).
- Search inside files (`->fullTextSearch()`): find a document by a word that is only in its Word, Excel, PowerPoint, OpenDocument, text, RTF or PDF file, on any of the four databases. `php artisan warp-documents:process-files` processes files that are already stored.
- Master list, exportable to Excel and printable, and a read matrix of people × documents (who has read the current revision, who has not, who is overdue) with CSV and Excel export. `Domain\ReadMatrix::build()` gives the same from code.
- Import the documents you already use from a register (Excel or CSV) and a ZIP, or by dropping many files, with a check of every row before anything is saved (`->imports()`, `Lifecycle::import()`).
- Links to your own records: `HasDocuments` on a model and `DocumentsRelationManager` show the current revision of each linked document, listing only documents the person may see.
- *My document tasks* page and `DocumentTasksWidget` for what is waiting for the signed-in person.
- Permissions: who may see each document, `canManageUsing()`, `canCreateUsing()`, `canImportUsing()`, `canViewReadMatrixUsing()`, your app's model policies, and `canAccessUsing()` / `canWriteUsing()` to decide per page from your app's roles.
- Append-only audit trail of every change, approval, confirmation and printed copy, and events for your own code.
- Filament multi-tenancy, and English, Japanese, German, French, Spanish, Italian, Brazilian Portuguese, Korean and Simplified and Traditional Chinese.
