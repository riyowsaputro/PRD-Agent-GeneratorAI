# 📄 PRD + Agent Generator AI

What Is This?
A web-based tool powered by Google Gemini AI that:

Interviews you about your product idea (3-5 questions per round + recommendations)
Generates a complete PRD with 10 industry-standard sections
Generates AI Agent files — system-prompt, workflow, and skill documents
Exports everything to Markdown, PDF, or clipboard

Quick Start
# 1. Get free API key
#    → https://aistudio.google.com/apikey

# 2. Open the tool
open index.html
# or serve locally
npx serve .

# 3. Paste API key → Pick model → Go!
# 4. Describe your product idea in chat
# 5. Answer questions or click "Process all → PRD"
# 6. Click "Generate Agent from PRD" for agent files
# 7. Export everything

How It Works
┌─────────────────────────────────────────────────────┐
│                    YOUR IDEA                         │
│            "I want to build a..."                    │
└──────────────────────┬──────────────────────────────┘
│
▼
┌─────────────────────────────────────────────────────┐
│              🎯 AI INTERVIEW                         │
│   Round 1: Problem & Users (+ recommendations)      │
│   Round 2: Scope & Constraints (+ recommendations)  │
│   Round 3: Design & Behavior (+ recommendations)    │
│                                                      │
│   ──── OR click "Process All" to skip ────           │
└──────────────────────┬──────────────────────────────┘
│
▼
┌─────────────────────────────────────────────────────┐
│              📄 PRD GENERATED                        │
│   10 sections: Overview, Goals, Personas,            │
│   Stories, Requirements, Design, Technical...        │
└──────────────────────┬──────────────────────────────┘
│
▼
┌─────────────────────────────────────────────────────┐
│          🤖 AI AGENT GENERATED                       │
│   system-prompt.md  →  Agent's brain & rules        │
│   workflow.md       →  Step-by-step procedures      │
│   skill.md          →  Domain knowledge & tools     │
│   How to Use        →  Deployment guide             │
└──────────────────────┬──────────────────────────────┘
│
▼
┌─────────────────────────────────────────────────────┐
│              🚀 EXPORT & DEPLOY                      │
│   PRD → .md / PDF / clipboard                       │
│   Agent → individual .md files or all-in-one        │
│   Project → .prd.json (save/load)                   │
└─────────────────────────────────────────────────────┘

PRD Sections
#	Section	Description
1	Overview	One-paragraph product summary
2	Goals & Success Metrics	Measurable targets
3	User Personas	2-4 grounded personas
4	User Stories & Flows	Step-by-step user journeys
5	Functional Requirements	Features with IDs and P0/P1/P2 priority
6	Non-Functional Requirements	Performance, security, scalability
7	Design Direction	Colors (hex), typography, components, reference apps
8	Technical Considerations	Architecture, APIs, data model
9	Out of Scope	What this version does NOT include
10	Open Questions	Risks and assumptions to validate
Agent Files
File	Purpose	How to Use
system-prompt.md	Agent persona, rules, constraints	Paste as system instruction in ChatGPT/Claude/Cursor
workflow.md	Operating procedures, decision trees	Reference for developers building AI features
skill.md	Domain knowledge, tools, integrations	Knowledge base / RAG document for the agent
Features
Core
✅ AI interview with recommendations at every question
✅ 10-section PRD generation
✅ 3-file Agent generation (system-prompt, workflow, skill)
✅ Auto-generated usage guide
✅ "Process all" button to skip interview
Interface
✅ Bilingual (English / Indonesian casual)
✅ Dark/Light theme
✅ Interactive 5-step tutorial
✅ Mobile responsive with swipe
✅ Resizable split panels
✅ Notification pulse when PRD/Agent ready
Data
✅ IndexedDB storage (50MB+)
✅ Auto-clear on browser close (privacy)
✅ Save/Load project files (.prd.json)
✅ Export: Markdown, PDF, clipboard
✅ Export all agent files at once
✅ PRD version tracking
Performance
✅ Streaming responses (real-time)
✅ Throttled rendering (150ms) — prevents freezing
✅ Markdown cache (LRU, 80 entries)
✅ Lazy message loading (last 30)
✅ Debounced auto-save (1.2s)
Keyboard Shortcuts
Shortcut	Action
Ctrl+Enter	Send message
Ctrl+S	Save project to file
Ctrl+N	New session
Esc	Close modal/sidebar

Storage Architecture
┌──────────────────────────────────────┐
│         IndexedDB "prdgen"           │
│            (~50-500MB)               │
│                                      │
│  Sessions: messages, PRD, Agent      │
│  Active session ID                   │
│                                      │
│  ⚡ Auto-clears when browser closes  │
│  (via sessionStorage flag trick)     │
└──────────────────────────────────────┘

┌──────────────────────────────────────┐
│     localStorage (persistent)        │
│                                      │
│  API key, model, theme, language     │
│  Tutorial/intro completion flags     │
└──────────────────────────────────────┘

Requirements
Modern browser (Chrome, Firefox, Safari, Edge)
Google Gemini API key (free tier available)
Internet connection for API calls
Models Supported
Model	Speed	Quality	Best For
gemini-2.5-flash	⚡⚡⚡	⭐⭐⭐	Recommended — fast + good quality
gemini-2.5-pro	⚡	⭐⭐⭐⭐⭐	Complex products, detailed PRDs
gemini-2.0-flash	⚡⚡⚡⚡	⭐⭐	Quick drafts, simple products

📁 Project Structure
index.html          ← Entire app (single file, no build needed)
README.md           ← This file

That's it. One HTML file. No npm, no webpack, no framework. Just open and go.

🔒 Privacy
API key stored in localStorage (your browser only)
Session data stored in IndexedDB (your browser only)
Session data auto-deleted when browser closes
Nothing is sent to any server except Google's Gemini API
No analytics, no tracking, no cookies
📄 License
MIT License — Use it, modify it, ship it.

Built with ❤️ by Rio Saputro
