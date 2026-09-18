---
title: Document Conversion Notes
description: How the original Word/PDF documents were converted and what the limits are.
---

# Document Conversion Notes

The `doc/` folders across the repository originally held Microsoft Word
(`.doc`, `.docx`) and PDF design documents. They are published on this site
under [Converted Design Documents](../../modules/) and linked from each module page.

## Method

- **`.docx`** — converted automatically with `python-docx`: headings, lists and
  tables are preserved; embedded images, OLE objects, headers/footers and exact
  formatting are omitted.
- **`.pdf`** — text extracted automatically with `pypdf` (figures, layout and
  scanned-image pages are not preserved). Very long PDFs are truncated with an
  explicit marker.
- **`.doc` (legacy binary)** — cannot be converted without Microsoft
  Word/LibreOffice; these pages state the limitation and summarise the document
  from its file name, owning module and neighbouring documents.
- **`.txt`** — reproduced verbatim.
- **TESSY PDFs** (`utp/Tessy/report/…`) are generated unit-test reports, not
  design documents; their pages are short excerpts labelled as test evidence.
- **Spreadsheets** (`.xls`, `.xlsm` data dictionaries, checklists, QAC reports)
  are listed as companions on the relevant module pages but were not converted.

## Source of truth

The repository files remain the source of truth — each converted page cites its
`Source:` path. If a converted page looks incomplete, open the original file
from the repository.
