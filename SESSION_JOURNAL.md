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
