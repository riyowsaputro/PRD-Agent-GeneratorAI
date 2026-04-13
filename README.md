# PRD Generator AI

A single-file web app that interviews you about your product idea, generates a PRD (Product Requirements Document), then creates AI Agent files — all through conversation with Gemini AI.

Built by Rio Saputro.

---

## What It Does

1. **You describe your product idea** in chat. Attach Excel (.xlsx) or Word (.docx) files as reference.
2. **AI interviews you** — 3-5 questions per round, each with a concrete recommendation.
3. **One click generates the PRD** with 10 sections: Overview, Goals, Personas, User Stories, Functional Requirements, Non-Functional, Design Direction, Technical Architecture, Out of Scope, Open Questions.
4. **One more click generates 3 Agent files**: `system-prompt.md`, `workflow.md`, `skill.md` — plus a "How to Use" guide.
5. **Export** each file as `.md` or copy to clipboard.

Everything runs in your browser. No backend. Your API key never leaves the page.

---

## Quick Start

1. Open `PRD Maker.html` in any modern browser.
2. Get a free Gemini API key at [aistudio.google.com/apikey](https://aistudio.google.com/apikey) (takes 30 seconds).
3. Paste the key in the welcome screen or Settings.
4. Start describing what you want to build.

That's it. No install, no dependencies, no build step.

---

## Features

**Chat + Document Generation**
- Conversational interview with AI recommendations
- Single-click PRD generation from conversation context
- Single-click Agent file generation from PRD
- Section-level feedback — click any PRD heading to request changes

**File Attachments**
- Drag-drop or click to attach `.xlsx`, `.xls`, `.docx` files
- AI reads spreadsheet data and document text as context
- Up to 5 files per message, 5MB each
- Token estimate shown per attachment

**Model Routing with Fallbacks**
- Chat uses `gemini-3.1-flash-lite-preview` → fallback: `gemma-4-31b-it`
- Generation uses `gemini-flash-latest` → fallback chain: `gemini-2.5-pro` → `gemini-2.5-flash` → `gemini-2.0-flash`
- Automatic failover — if one model errors, the next tries without user action

**Session Management**
- Multiple sessions with auto-generated titles
- Save/load projects as `.prd.json` files
- Sessions persist in IndexedDB within a browser session
- `Ctrl+S` saves, `Ctrl+N` creates new session

**Accessibility (WCAG 2.1 AA)**
- Skip navigation link
- All interactive elements have accessible names (`aria-label`)
- Proper dialog focus trapping and focus restoration
- `inert` background when modals/dialogs are open
- Roving tabindex on tab groups with arrow key navigation
- Keyboard-operable panel resize (`Arrow Left`/`Right`)
- 44px minimum touch targets on mobile
- Color contrast ≥4.5:1 on all text in both themes
- `prefers-reduced-motion` support
- `forced-colors` (Windows High Contrast) support
- Screen reader live regions for chat messages, typing indicator, and notifications

**UI**
- Light/dark theme toggle
- English/Indonesian language toggle
- Resizable chat/document split panel
- Mobile-responsive with swipe gestures between chat and docs
- Print stylesheet (prints document panel only)
- Guided tutorial on first visit

---

## Tech Stack

Single HTML file. No build tools.

| What | How |
|------|-----|
| UI framework | None — vanilla JS, CSS custom properties |
| Markdown rendering | [marked](https://github.com/markedjs/marked) + [DOMPurify](https://github.com/cure53/DOMPurify) |
| Excel parsing | [SheetJS](https://sheetjs.com/) |
| Word parsing | [Mammoth](https://github.com/mwilliamson/mammoth.js) |
| AI | Google Gemini API (streaming SSE) |
| Storage | IndexedDB (sessions), localStorage (settings) |

All libraries loaded from CDN. Total page weight ~250KB (mostly the parsing libraries).

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+Enter` | Send message |
| `Ctrl+S` | Save project to file |
| `Ctrl+N` | New session |
| `Escape` | Close current overlay (tutorial → settings → feedback → sidebar) |
| `Arrow Left/Right` | Navigate tabs (when focused on tab bar) |
| `Arrow Left/Right` | Resize panels (when focused on resize handle) |

---

## File Outputs

**PRD.md** — The product requirements document. 10 sections, functional requirements as bullet lists (not tables), design direction with hex codes and font specs.

**system-prompt.md** — Agent persona, rules, and constraints specific to your product.

**workflow.md** — Step-by-step decision trees, user flows, error handling procedures.

**skill.md** — Domain knowledge, tool integrations, API specifications the agent needs.

**How to Use guide** — Deployment steps for each file, quick start instructions, maintenance tips.

---

## Project File Format

Saved projects use `.prd.json` with this structure:

```json
{
"v": 5,
"s": {
  "name": "Session title",
  "ts": 1713000000000,
  "ut": 1713000000000,
  "msgs": [],
  "prd": "# PRD content...",
  "agent": {
    "system": "...",
    "workflow": "...",
    "skill": "...",
    "guide": "..."
  },
  "fb": {},
  "tokens": { "in": 0, "out": 0 }
}
}

Attachment content is included in the saved file (so references persist across loads).

Configuration
Open Settings (⚙ button or sidebar → Settings):

Setting	Default	Notes
API Key	—	Gemini API key. Stored in localStorage only.
Max Tokens (Generate)	65,536	Range: 1,024–131,072. Applies to PRD/Agent generation, not chat.
Temperature	0.6	0 = deterministic, 1 = creative.
System Prompt Override	empty	Replaces both chat and generation prompts. Leave empty for built-in prompts.
Browser Support
Tested on Chrome, Firefox, Safari, Edge — all 2023+ versions. Requires:

fetch with streaming (ReadableStream)
IndexedDB
inert attribute
CSS custom properties
backdrop-filter (graceful degradation if missing)
Privacy
API key stored in localStorage — never sent anywhere except Google's Gemini API endpoint.
Sessions stored in IndexedDB — cleared automatically when you close the browser tab and reopen.
No analytics, no telemetry, no cookies, no external tracking.
File attachments parsed entirely in-browser. Content is sent to Gemini API as part of the conversation only when you send a message.

Known Limitations
API key in URL: Gemini's streaming endpoint requires the key as a query parameter. This is Google's API design. Use a restricted key if this concerns you.
No offline mode: Requires internet for AI calls. The UI works offline but can't generate.
.doc files unsupported: Only .docx (Office 2007+). Mammoth doesn't parse the legacy binary format.
Session persistence: Sessions clear when you close the browser and reopen (by design — ephemeral). Use Save/Load for permanent storage.
Token estimates: Based on chars/4 heuristic. Actual token counts from the API are not available via streaming.
Development
It's one HTML file. Open it in a browser. Edit it in any text editor. No build step.

To modify AI behavior, edit SYS_CHAT and SYS_GEN constants near the top of the <script> block.

To add a language, add an entry to the LL object with all translation keys.

To change model routing, edit CHAT_MODELS and GEN_MODELS arrays.

License
MIT

Author
Rio Saputro
