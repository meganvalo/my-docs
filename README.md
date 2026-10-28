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
