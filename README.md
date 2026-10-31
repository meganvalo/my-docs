MyDocs — GitHub Pages deployment

Upload the contents of this folder directly to the root of your GitHub Pages repository (the same level as index.html). All app and icon files are kept at the root; no enclosing project folder or nested ZIP is needed.

If the app was previously installed, refresh the site (twice) to pick up the updated service-worker cache. Documents are stored in the browser, so do not clear website data unless you have a backup.


Latest update: data-safety release.
- Storage moved from localStorage to IndexedDB (one record per document). Existing documents are imported automatically on first launch; the old localStorage copy is left untouched. If IndexedDB is unavailable, the app falls back to localStorage.
- Several tabs/windows can be open at once. Changes sync between them, and if two tabs edit the same document, neither version is lost (one is kept as a "conflicted copy").
- All stored, restored and pasted HTML goes through an allowlist sanitiser. Links are limited to http(s), mailto and tel.
- Restoring a backup validates each entry and never overwrites: a document that differs from the one already here is added as a "(restored copy)".
- Deleting a document moves it to Trash (30 days) with an Undo toast; restore or delete forever from the Trash button in the sidebar.
- Images are downscaled (max 1600 px) on insert; the browser is asked to keep storage persistent.

Follow-up update:
- Pasting from Google Docs or Word keeps bold, italic, underline and strikethrough (inline styles become real formatting, and Docs' "normal weight" wrapper no longer turns everything bold).
- Table tools in the formatting panel: add or delete a row or column, or the whole table. They are enabled when the cursor is inside a table, and Undo/Redo work with them.
- Accessibility: named buttons, toggle states, labelled editor and toolbar; closed drawers are removed from the tab order, focus moves into a drawer when it opens and returns to its button when it closes.
- "+ New" now closes the document drawer. The leftover nested mydocs-app.zip was removed: delete it from your repository too.

Highlight and phone update:
- New highlight tool (12 colours) with a "No highlight" button. It removes highlighting from just the selected words, or from the whole highlighted run if you tap inside it, even for highlights that came from pasted text.
- "Clear formatting" is now a full-width button in the options panel. It removes bold, italic, underline, colour, highlight and fonts, and tidies stray line breaks and non-breaking spaces from pasted text, for the selection or (with nothing selected) the current paragraph. Links, lists and headings are kept. An Undo button appears after each clear.
- Pasting no longer brings in highlights or text colours from other sites, and pasted whitespace is normalised.
- Phone layout: proper padding inside the page, tighter list indents, safe-area spacing at the bottom, and an organised options panel (labelled groups, aligned rows, touch-sized buttons).

Tools update:
- Find & replace (Options > Tools, or Ctrl/Cmd+Shift+F): highlights every match, next/previous, match case, replace one or all. Matches are found within a single run of formatting, so a word that is half bold is not matched.
- Outline: lists Heading 1-3 and jumps to the one you tap.
- Version history: older versions are saved automatically (about every 10 minutes while editing, up to 12 per document) plus "Save a version now". Preview and Restore; restoring first saves your current text as a version. History is stored in this browser only and is not included in backups. It needs IndexedDB.
- Import .md, .txt and .html files (several at once, max 5 MB each). Each becomes a new document; imports never overwrite anything and go through the same sanitiser as paste.
- Text size menu, and checklists (tap the box to tick; exported to Markdown as - [ ] / - [x]).
- Tags: add comma-separated tags per document and filter by them above the document list. Tags are included in backups.
- Encrypted backup: a passphrase-protected backup file (AES-GCM, key from PBKDF2). The passphrase is never stored: if it is lost the file cannot be opened. Restore detects encrypted files and asks for the passphrase. Needs https (GitHub Pages is).
- Not included on purpose: encrypting the live documents in the browser, and automatic file sync.
