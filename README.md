<div align="center">

<img src="./Branding/Logo%20horizontal%20curved.png" alt="Quantivelle — Kyro WORKSAPCE" width="620">

# Kyro WORKSAPCE

**Your local-first AI study partner that turns any PDF into summaries, notes, quizzes, and flashcards.**

[![Open Kyro WORKSAPCE](https://img.shields.io/badge/Try%20it%20Live-Open%20Kyro%20WORKSAPCE-4f46e5?style=for-the-badge&logo=githubpages&logoColor=white)](https://quantivelle.github.io/Kyro-WORKSAPCE/)

**👉 Click above and start using it right now — no install, no signup, no waiting.**
**➡️ [https://vaguevault76-ctrl.github.io/StudyMind-AI/]([https://quantivelle.github.io/Kyro-WORKSAPCE/])**

---

Hey there! I'm glad you found your way here. Let me walk you through what you're looking at.

**Kyro WORKSAPCE** is a document learning platform that lives entirely inside your browser. You hand it a PDF, and it hands you back summaries, study notes, quizzes, flashcards, and plain-English explanations — all powered by AI.

Here's the part you'll appreciate: everything runs locally. We extract your PDF's text with [pdf.js](https://mozilla.github.io/pdf.js/) right on your machine, then send it straight from *your* browser to [OpenRouter](https://openrouter.ai/) models. There are no accounts, no backend servers, and no tracking. Your API key and your saved notes never leave your device.

You don't need to install anything. You don't need to configure anything. Just open the link above — the landing page explains the product and one click takes you straight into the tool.

The site is split in two: **`index.html`** is the public landing page (what the tool does, how it works, FAQ, and the **Launch Tool** button), and **`app.html`** is the application itself. Both are plain static files with no build step.

</div>

---

## Table of contents

- [Pages](#pages)
- [What you can do](#what-you-can-do)
- [How it works for you](#how-it-works-for-you)
- [Tech stack](#tech-stack)
- [Run it locally](#run-it-locally)
- [Project structure](#project-structure)
- [Security](#security)
- [Privacy](#privacy)
- [Browser support](#browser-support)
- [License](#license)
- [Trademark](#trademark)

---

## Pages

The site is a set of static pages with no build step:

| Page | Purpose |
| --- | --- |
| `index.html` | SEO landing page — what the tool does, how it works, FAQ, and a prominent **Launch Tool** button into `app.html`. |
| `app.html` | The application itself — upload, extract, generate, save. |
| `privacy.html` | Privacy policy. |
| `trademarks.html` | Trademark guidelines. |
| `license.html` | Apache 2.0 license (rendered). |

---

## What you can do

### Handle your documents your way

- You get a multi-file PDF library with drag-and-drop upload — drop in as many documents as you like.
- Text extraction happens locally, with layout, powers, and element detection preserved.
- Hindi content is detected automatically (English documents only for now).
- You can read the original PDF inline, with full page navigation.

### Let the AI do the heavy lifting

- **Summary** — you get a structured breakdown of the whole document.
- **Q&A** — you ask a question, it answers from the actual extracted content.
- **Study notes** — you get full notes you can style, file into folders, tag, and search.
- **Simplification** — you get complex passages rewritten in plain English.
- **Quizzes** — you can test yourself with MCQ, true/false, fill-in, case study, and HOTS questions.
- **Flashcards** — you revise with active recall, revision, and exam-brainstorm modes.
- **Study pack** — you get everything at once with one click.
- **Knowledge gap analysis** — you receive a learning path based on what the content actually covers.
- **Exam optimizer** — you get an exam-focused analysis of your material.
- **Comparison tables** — you can view topics side by side.
- **AI chat assistant** — you get a floating helper with text-selection actions, per-note chat history, and regeneration.
- **Self-review** — you can optionally ask the AI to verify its own output against the source.

### Keep control of your work

- Your notes are saved locally in IndexedDB, with folders, tags, pin, rename, and bulk actions.
- Your API key stays in `localStorage` only.
- Your chat history is persisted per note.
- You get an optional onboarding tour and a settings panel whenever you want them.

---

## How it works for you

1. You drop one or more PDFs into the browser.
2. pdf.js extracts the text locally — nothing is uploaded to any server.
3. The extracted text is truncated, optionally combined with your own prompt, and sent directly from your browser to OpenRouter.
4. The response comes back as markdown, gets sanitized, and picks up KaTeX math where needed.
5. You save it as a note, quiz yourself, turn it into flashcards, or keep discussing it in the chat assistant.

There is no application backend. The only outbound network call you make is to `https://openrouter.ai`.

---

## Tech stack

All third-party libraries are vendored locally under `vendor/` — you get no CDN dependencies at runtime.

| Library | Purpose |
| --- | --- |
| [pdf.js](https://mozilla.github.io/pdf.js/) | PDF text extraction and rendering |
| [marked](https://github.com/markedjs/marked) | Markdown to HTML |
| [KaTeX](https://katex.org/) | Math rendering |
| [DOMPurify](https://github.com/cure53/DOMPurify) | HTML sanitization of all AI/external output |

The landing page and the application are both single static pages (`index.html` and `app.html`) with no build step and no framework. The landing page loads no third-party JavaScript at all — every effect on it is hand-written, transform/opacity-only and gated behind `prefers-reduced-motion` and an automatic low-end-device "lite" mode.

---

## Run it locally

You don't have to. **Just use the live version:** [https://vaguevault76-ctrl.github.io/StudyMind-AI/](https://vaguevault76-ctrl.github.io/StudyMind-AI/)

If you'd rather run it yourself, there's no build step. Open `index.html` (landing page) or `app.html` (the tool) in a modern browser, or serve the folder:

```bash
# Python
python -m http.server 8080

# Node
npx serve .
```

Then visit `http://localhost:8080`.

> Opening via `file://` works for basic use, but a local HTTP server is recommended so the PDF worker and fonts load correctly.

---

## Project structure

```
.
├── index.html              # SEO landing page (single file: markup + CSS + JS)
├── app.html                # Main application (single-file app)
├── privacy.html            # Privacy policy
├── trademarks.html         # Trademark guidelines
├── license.html            # Apache 2.0 license (rendered)
├── legal.css               # Styles for the legal pages
├── LICENSE                 # Apache License 2.0
├── README.md               # This file
├── llms.txt                # Machine-readable project summary
├── robots.txt              # Crawler rules
├── sitemap.xml             # XML sitemap for search engines
├── .nojekyll               # Disable Jekyll on GitHub Pages
├── Branding/
│   ├── LOGO.png                    # Full logo (social / OG image)
│   ├── Logo horizontal.png         # Horizontal logo (original)
│   ├── Logo horizontal curved.png  # Horizontal logo used in this README (curved edges + vignette)
│   ├── logo-mark.png               # App mark (UI + splash)
│   ├── favicon.png                 # Browser tab icon
│   └── fonts/                      # Self-hosted webfonts
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

You should know that the app treats PDF text and AI output as untrusted input — because it does.

- All AI-generated and PDF-derived HTML is sanitized with DOMPurify before it ever reaches your page.
- A strict Content-Security-Policy restricts scripts, frames, objects, and network calls to the minimum required.
- External links use `rel="noopener noreferrer"`.
- Your OpenRouter API key is stored only in your browser's `localStorage` and is never sent to any server other than OpenRouter itself.

---

## Privacy

- You get no analytics, no cookies, and no tracking.
- Your API keys and notes stay in your browser only.
- You can read the full policy in [privacy.html](./privacy.html).

---

## Browser support

You'll need a modern browser with JavaScript enabled. Tested targets are current and recent versions of Chrome, Edge, Firefox, and Safari.

---

## License

You're free to use the code under the [Apache License 2.0](./LICENSE).

---

## Trademark

**Quantivelle™**, **Kyro WORKSAPCE™** and the Quantivelle logo are trademarks of Quantivelle. The open-source license covers the code only; use of the brand assets requires permission. See [trademarks.html](./trademarks.html).
