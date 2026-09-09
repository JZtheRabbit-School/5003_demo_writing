# Margin editorial workspace

An interactive, self-contained review surface for editors and writers. On entry, users choose a role:

- Writers land in a dedicated **Writer space**, where they can add and see their own `.pdf` or `.docx` drafts.
- Editors land in a separate **Editor space**, where they can browse every submitted draft, select one draft at a time, and open it for editing.
- A **Change role** control always returns users to the initial role chooser.
- Editors can select text to attach inline comments, reply within the comment rail, and leave general feedback at the end of the draft.

For privacy, draft files are retained only in the browser's local IndexedDB store; they are never uploaded or sent to an external service. DOCX and text-based PDF files are read into the editorial canvas for inline highlighted comments. Image-only/scanned PDFs are rendered and recognized through a bundled, on-device Tesseract OCR runtime; the result is also placed in the editorial canvas for comments. Writers can delete their own drafts from the Writer space.

The OCR runtime is bundled in the local `tesseract*`, `eng.traineddata.gz`, and `pdf*` files. Keep these next to `index.html`; no network is used while the app runs.

Draft entries added by the older prototype stored names only. Upload those files once more to make their document contents available to editors.

## Run locally

From this directory, start a static server. This is required for local scanned-PDF OCR because browser workers cannot run from a `file://` page.

```powershell
python -m http.server 8000
```

Then open `http://localhost:8000` in a browser. No packages, build step, or external services are required.

Do not open `index.html` by double-clicking it when using OCR: `file://` pages have a `null` origin and browsers block the OCR worker for security.
