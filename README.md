# StudyMind AI

A local-first intelligent document learning platform that turns PDF documents into summaries, notes, quizzes, flashcards, and simple explanations using AI.

Everything runs in the browser. PDF text is extracted locally with [pdf.js](https://mozilla.github.io/pdf.js/), then sent directly from your browser to [OpenRouter](https://openrouter.ai/) models. There are no accounts, no backend servers, and no tracking. Your API key and saved notes never leave your device.

---

## Table of contents

- [Features](#features)
- [How it works](#how-it-works)
- [Tech stack](#tech-stack)
- [Run locally](#run-locally)
- [Deploy on GitHub Pages](#deploy-on-github-pages)
- [Project structure](#project-structure)
- [Security](#security)
- [Privacy](#privacy)
- [Browser support](#browser-support)
- [License](#license)
- [Trademark](#trademark)

---

## Features

### Document handling

- Multi-file PDF document library with drag-and-drop upload
- Local text extraction with layout, powers, and element detection
- Hindi-content detection (English documents only for now)
- Inline PDF viewer with page navigation

### AI generation

- **Summary** — structured document summaries
- **Q&A** — ask questions grounded in the extracted content
- **Study notes** — full notes with styles, folders, tags, and search
- **Simplification** — plain-English explanations of complex text
- **Quizzes** — MCQ, true/false, fill-in, case study, and HOTS questions
- **Flashcards** — active recall, revision, and exam-brainstorm modes
- **Study pack** — one-click generation of combined study materials
- **Knowledge gap analysis** — learning-path suggestions from the content
- **Exam optimizer** — exam-focused analysis of the material
- **Comparison tables** — side-by-side topic comparisons
- **AI chat assistant** — floating assistant with text-selection actions, per-note chat history, and regeneration
- **Self-review** — optional AI verification pass that checks output against the source

### Storage and productivity

- Notes saved locally (IndexedDB) with folders, tags, pin, rename, and bulk actions
- API keys stored in `localStorage` only
- Chat history persisted per note
- Optional onboarding tour and settings panel

---

## How it works

1. The user drops one or more PDFs into the browser.
2. pdf.js extracts text locally (no upload to any server).
3. The extracted text is truncated, optionally combined with a user prompt, and sent directly from the browser to OpenRouter.
4. The model response is rendered as markdown, sanitized, and enhanced with KaTeX math where present.
5. Output can be saved as a note, quizzed, turned into flashcards, or discussed in the chat assistant.

There is no application backend. The only outbound network call is to `https://openrouter.ai`.

---

## Tech stack

All third-party libraries are vendored locally under `vendor/` — no CDN dependencies at runtime.

| Library | Purpose |
| --- | --- |
| [pdf.js](https://mozilla.github.io/pdf.js/) | PDF text extraction and rendering |
| [marked](https://github.com/markedjs/marked) | Markdown to HTML |
| [KaTeX](https://katex.org/) | Math rendering |
| [DOMPurify](https://github.com/cure53/DOMPurify) | HTML sanitization of all AI/external output |

The application itself is a single static page (`index.html`) with no build step and no framework.

---

## Run locally

No build step is required. Open `index.html` in a modern browser, or serve the folder:

```bash
# Python
python -m http.server 8080

# Node
npx serve .
```

Then visit `http://localhost:8080`.

> Opening via `file://` works for basic use, but a local HTTP server is recommended so the PDF worker and fonts load correctly.

---

## Deploy on GitHub Pages

1. Push this repository to GitHub.
2. Open **Settings** → **Pages**.
3. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
4. Choose branch `main` (or `master`) and folder `/ (root)`, then **Save**.
5. Wait a minute — the site will be live at `https://<your-username>.github.io/<your-repo>/`.

The `.nojekyll` file is included so GitHub Pages serves the files as-is without Jekyll processing.

---

## Project structure

```
.
├── index.html              # Main application (single-file app)
├── privacy.html            # Privacy policy
├── trademarks.html         # Trademark guidelines
├── license.html            # Apache 2.0 license (rendered)
├── legal.css               # Styles for the legal pages
├── LICENSE                 # Apache License 2.0
├── README.md               # This file
├── llms.txt                # Machine-readable project summary
├── robots.txt              # Crawler rules
├── .nojekyll               # Disable Jekyll on GitHub Pages
├── Branding/
│   ├── LOGO.png            # Full logo (social / OG image)
│   ├── logo-mark.png       # App mark (UI + splash)
│   ├── favicon.png         # Browser tab icon
│   └── fonts/              # Self-hosted webfonts
└── vendor/                 # Third-party libraries (vendored, offline-friendly)
    ├── pdf.min.js          # pdf.js core
    ├── pdf.worker.min.js   # pdf.js worker
    ├── cmaps/              # pdf.js character maps
    ├── standard_fonts/     # pdf.js standard fonts
    ├── marked.min.js       # Markdown renderer
    ├── katex.min.js        # KaTeX math
    ├── katex.min.css
    ├── katex-fonts/        # KaTeX fonts
    ├── auto-render.min.js  # KaTeX auto-render helper
    └── dompurify.min.js    # HTML sanitizer
```

---

## Security

The app treats PDF text and AI output as untrusted input.

- All AI-generated and PDF-derived HTML is sanitized with DOMPurify before being inserted into the page.
- A strict Content-Security-Policy restricts scripts, frames, objects, and network calls to the minimum required.
- External links use `rel="noopener noreferrer"`.
- The OpenRouter API key is stored only in the browser's `localStorage` and is never sent to any server other than OpenRouter itself.

---

## Privacy

- No analytics, no cookies, no tracking.
- API keys and notes stay in your browser only.
- See [privacy.html](./privacy.html) for the full policy.

---

## Browser support

Requires a modern browser with JavaScript enabled. Tested targets are current and recent versions of Chrome, Edge, Firefox, and Safari.

---

## License

Code is licensed under the [Apache License 2.0](./LICENSE).

---

## Trademark

**Quantivelle™** and the Quantivelle logo are trademarks of Quantivelle. The open-source license covers the code only; use of the brand assets requires permission. See [trademarks.html](./trademarks.html).
