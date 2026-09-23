# Session journal

This is a running record of project sessions: learning, project changes, next steps, and known limitations.

## 2026-09-09 — Project setup

### Learned

- Git can track project history through local commits, with an author name and email attached to each commit.
- Scanned PDFs need OCR before their image-based content can be highlighted and commented on as text.

### Project changes

- Built the Margin writer/editor review app with role-specific views, draft management, inline comments, general feedback, DOCX extraction, and local PDF OCR support.
- Added bundled local PDF and OCR runtime assets.
- Organized the project into `5003_demo_writing` and initialized Git with the initial commit `25cc10e`.
- Added session wrap-up guidance in `AGENT.md`.

### Next to learn or change

- Verify local OCR end-to-end with a scanned PDF served through `http://localhost:8000`.
- Consider refining OCR accuracy, loading progress, and editor review workflows.

### Known limitations

- OCR runs only from the local HTTP preview, not when `index.html` is opened through `file://`.

## 2026-09-15 — Genre libraries and completed editorial feedback

### Learned

- A local browser app can use `localStorage` to retain lightweight workflow state, such as active and completed editing lists, alongside file data held in IndexedDB.
- A review workflow benefits from separate queues for available submissions, active work, and completed work.

### Project changes

- Added genre selection for writer uploads and genre-filtered editor submission browsing.
- Added a personal editor active-editing library with a five-draft limit and removable entries.
- Added a completion action that moves an edited draft into a genre-grouped completed-edits library and shares the editor's general feedback and inline notes with the writer.
- Refined the writer feedback flow so completed reviews open as a read-only copy of the draft with linked inline notes beside the relevant passages, plus the overall feedback at the end.
- Updated the README with the current workflow and usage instructions.

### Next to learn or change

- Test the full writer-to-editor-to-writer feedback loop with several draft types and genres.
- Consider adding named editor profiles or timestamps if the prototype later supports multiple independent editors.

### Known limitations

- The prototype is local to one browser profile; it has no accounts, network syncing, or real multi-user collaboration.
- Inline comments are shared when an editor completes the review; unfinished comments are not yet saved as a draft review.

## 2026-09-22 — Role-selection icons

### Learned

- Small inline SVG icons give a consistent visual result across browsers without relying on an emoji font.

### Project changes

- Replaced the writer role’s star with a quill icon and the editor role’s abstract mark with a document icon.

### Next to learn or change

- Continue refining the prototype’s visual language and end-to-end review workflow.

### Known limitations

- The local preview server must be running for `http://localhost:8000` to open.

## 2026-09-23 — Private note conversations

### Learned

- A simple state rule can model an intentional messaging workflow: a writer sends one opening message, and an editor reply unlocks the ongoing conversation.

### Project changes

- Added per-comment private message threads stored locally with each completed edit.
- Writers can send one private message under an editor’s inline note; editors can reply from their completed-edits view; after that reply, both roles can continue the thread.
- Documented the workflow in the README.

### Next to learn or change

- Test the role-switching conversation flow with multiple notes on the same draft.

### Known limitations

- Private messages remain in this browser’s local storage and are not sent over a network or shared across devices.
