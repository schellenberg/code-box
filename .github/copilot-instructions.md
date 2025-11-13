**Purpose**
- **What:** Short, actionable guidance for AI coding agents working in this repository.
- **Where to look:** Primary source is `README.md` (project description and UX requirements).

**Big Picture**
- **Single-page offline web tool:** The app provides a full-page textbox (CodeMirror downloaded locally) to let students write code then copy/paste into an LMS.
- **Why offline-first:** The README explicitly requires a locally downloaded CodeMirror so the page works with or without internet connectivity.

**Key Files & Locations**
- **`README.md`**: authoritative description of feature requirements (monospace, tab/shift-tab behavior, no autocomplete/highlighting, copy button).
- **`index.html` (expected)**: page shell and inclusion of local CodeMirror assets.
- **`static/` or `vendor/` (expected)**: place for local CodeMirror files and CSS; avoid CDN links.
- **`main.js` (or similar)**: plain JS to wire CodeMirror, tab handling, and the copy-to-clipboard button.

**Developer Workflows**
- **Preview locally:** Run a static server from the repository root. On Windows PowerShell use:

```
python -m http.server 8000
# or
npx http-server -p 8000
```

- **Open** `http://localhost:8000` and verify the textbox behavior and the "Copy Code" button.

**Project-specific Conventions**
- **Offline assets only:** Do not introduce CDN dependencies for CodeMirror or other runtime libraries; bundle them under `static/` or `vendor/`.
- **Minimal toolchain:** Prefer plain HTML/CSS/vanilla JS. If adding a build step, document it clearly in `README.md`.
- **Behavior driven by README:** Implementations must satisfy these exact UX bullets from `README.md`: monospace font; `Tab` inserts indentation; `Shift+Tab` unindents; no autocomplete; no syntax highlighting; copy-button selects all and copies to clipboard.

**Integration Points & APIs**
- **Clipboard:** Use the modern Clipboard API (`navigator.clipboard.writeText`) with fallback to `document.execCommand('copy')` for compatibility.
- **CodeMirror config:** Ensure the configuration disables autocomplete/addons and disables syntax mode if present (use plain text mode or no-mode option).

**Patterns to Follow (Examples)**
- **Tabs behavior:** Capture `Tab` and `Shift+Tab` inside the editor rather than default browser behavior. Example: configure CodeMirror keymap or handle `keydown` events to insert/remove indentation.
- **Copy button:** Select all content from the editor instance (e.g., `editor.getValue()`), then call `navigator.clipboard.writeText(...)` and provide user feedback (e.g., temporary tooltip or subtle notice).

**What Agents Should Do**
- **Read `README.md` first** and mirror its language precisely in issues/PR descriptions when adding or changing behavior.
- **When adding files**: place local libraries under `static/` or `vendor/`, update `index.html` to reference them relatively, and add a short note in `README.md` documenting the asset origin/version.
- **Keep changes minimal & reversible:** This is a small, offline-first educational utility — prefer small, well-documented edits over introducing heavy frameworks.

**PR & Commit Guidance**
- **Commit messages:** short verb + scope, e.g., `feat(ui): add copy button with clipboard API` or `chore(vendor): add codemirror-5.65.13 files`.
- **PR description:** Reference the relevant `README.md` requirement and demonstrate manual verification steps (server command + URL + checklist of the six UX bullets).

**If you need more context**
- Ask for expected filenames or whether a front-end framework is desired. If no guidance is given, implement in plain HTML/CSS/vanilla JS.

**Contact for Clarification**
- If any requirement in `README.md` appears ambiguous (e.g., which CodeMirror release to use), propose a default (CodeMirror 5.x bundled locally) and request confirmation.

---
If you'd like, I can now scaffold a minimal `index.html`, `static/` layout, and a small `main.js` implementing the exact behaviors from `README.md` for quick verification.
