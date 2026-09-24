# Margin — writer and editor workspace

Margin is a small, local-first browser app for reviewing drafts. It gives writers a place to add their work and editors a focused surface for opening one draft at a time, highlighting passages, leaving inline notes, replying to comments, and adding overall feedback.

This is a prototype built as a single-page application. It uses no accounts, database server, or third-party API while running.

## What it can do

### Writer space

- Upload `.docx` and `.pdf` drafts.
- Choose a genre for each upload, including sci-fi, fantasy, horror, mystery, romance, poetry, and more.
- See drafts added in the current browser workspace.
- Delete drafts you no longer want to keep locally.
- See when a draft has been edited and open the editor's shared general feedback and inline notes alongside the reviewed draft text, saved when the editor completes the review.

### Editor space

- Choose a genre, browse only writer submissions in that category, and open one draft.
- Highlight a passage and attach an inline editorial comment.
- Reply to an existing comment.
- Add general feedback at the end of the draft.
- Keep up to five drafts in a personal active editing library.
- Finish an edit to share its notes with the writer and move it into a completed-edits library, grouped by genre.
- Reply privately to a writer’s question on an inline note after the writer has sent their first message.

### Document handling and privacy

- Draft files are stored only in the browser’s IndexedDB storage on the current computer.
- DOCX files are parsed into editable paragraph text.
- Text-based PDFs are parsed into editable text.
- Image-only/scanned PDFs use the included local PDF and Tesseract OCR assets to attempt text recognition before opening the result for annotation.
- Files are not uploaded to a server or sent to an external OCR service.

## Requirements

- A modern Chromium-based browser.
- A local HTTP server. This is required for the OCR worker used by scanned PDFs.
- Either Python 3 or Node.js to start that server. No package installation or build step is needed.

## Run locally

Open a terminal in this project folder and use one of the following options.

### Option 1: Python

```powershell
python -m http.server 8000
```

### Option 2: Node.js

```powershell
node -e "require('http').createServer((req,res)=>require('fs').readFile(req.url==='/'?'index.html':req.url.slice(1),(err,data)=>{res.writeHead(err?404:200);res.end(err?'Not found':data)})).listen(8000)"
```

Then visit [http://localhost:8000](http://localhost:8000).

Do not open `index.html` by double-clicking it when using OCR. A `file://` page has a `null` origin, and browsers block the OCR worker for security.

## How to use it

1. Choose **I’m a writer** or **I’m an editor** on the welcome screen.
2. As a writer, choose a genre, select **Upload drafts**, then choose one or more PDF or DOCX files.
3. Use **Change role** to return to the welcome screen.
4. As an editor, choose the genre you want to edit, choose **Browse submissions**, then select and open one matching draft. Opening it adds it to **My editing library**; at most five drafts can be active at once.
5. Select text in the document, choose **Add comment**, write the note, and save it.
6. Add broader feedback in the **General feedback** area at the bottom, then select **Finish editing & share feedback**. The draft leaves the active editing library, appears in **Completed edits** grouped by genre, and the writer can select **Read feedback** beside their draft. Their draft opens in a read-only review view, with editor notes linked to the relevant passages.
7. Under an inline note, the writer may send one private message. After the editor replies from **Completed edits**, the private thread becomes an ongoing conversation for both roles.

## OCR notes

The included OCR language model is English. Recognition quality depends on the scan’s resolution, contrast, orientation, and handwriting quality. OCR can take noticeably longer than opening a DOCX or a text-based PDF, especially for multi-page files.

Keep `pdf.min.js`, `pdf.worker.min.js`, `tesseract.min.js`, `tesseract.worker.min.js`, `tesseract-core.wasm.js`, `tesseract-core.wasm`, and `eng.traineddata.gz` beside `index.html`; they are required for local scanned-PDF OCR.

## Project files

- `index.html` — app interface, styles, and client-side logic.
- `AGENT.md` — collaboration and end-of-session guidance.
- `SESSION_JOURNAL.md` — running record of what was learned, changed, and planned.

## Development notes

- The app is designed to run locally, so each browser profile has its own drafts.
- Existing drafts from the early metadata-only prototype must be uploaded again to make their file contents available.
- Before sharing changes, check `git status`, commit intended work, and push when ready.

## Reflection
I wanted to create an app that connects novice writers with editors. Many people I know, including myself, have written fiction or fanfiction at some point in their lives. From my own experience, finding a beta reader or editor who can offer critical feedback can be difficult. My initial idea was to let editors highlight passages, leave annotations, and provide overall feedback. However, the first prototype Codex created only offered an editor’s view with placeholder text. I had to clarify to the Codex that this app needed to support both writers and editors, each with their own pages for uploading/reviewing drafts and they also have the option to switch roles. Testing out these features revealed several problems: uploaded DOCX files initially displayed placeholder text instead of their actual content even though the file name had changed, writers could not delete drafts, and somehow the editor can select multiple works for editing at the same time (open two or more documents in one page), which is not what I intended. Through repeated testing and revisions, these issues were resolved......mostly. Testing PDF uploads introduced another challenge: my PDF contained images rather than selectable text, so extracting its content required an OCR engine. This eventually worked, although the extracted text sometimes confused “I” with “|,” an issue which yet to be resolved.

As the core interaction improved, I added genre categories, a separate editing library for the editor, a limit of five active works per editor, as well as a button for marking editing as complete. There are some very interesting miscommunications between me and the Codex, for example, when I asked it to make the writer able to access editor's feedback once they finished editing, it interpreted it as being able to access those feedback, but the feebacks themselves were taken out of context as the text itself is not displayed. I also experimented with annotation symbols and visual details, as well as requested a reply feature that would let writers and editors discuss feedback through alternating messages. This process showed me that generating code was only one part of building the app. Yes Codex can write codes and create prototypes for me, but it cannot test the app from a user's perspective and won't know what went wrong unless been told. Only I can do that and see the errors it had been making, feel about the design, and tell it how it could improve. Codex helped turn my ideas into working features, but I still needed to define the intended behavior, test it myself, identify mismatches, and explain what needed to change. The early prototypes were rough, and the app became more complex through that back-and-forth process. Currently this prototype simulates writer and editor workflows  only within the same browser profile, which means that it does not yet support separate user accounts or sharing drafts across devices. Next, I would like to explore making it accessible across multiple devices and adding user accounts. as well as improving the accuracy of text extracted from scanned PDFs.

