# ⚓ Anchor

A spaced-repetition flashcard app for learning **Governance, Risk & Compliance (GRC)**. Short daily study sessions that actually make frameworks, controls, and vocabulary stick — not passive reading.

Built as a self-contained sibling to Kyther: one `index.html`, vanilla JS, no build step, no backend, works offline.

## Features

- **Spaced repetition (SM-2)** — cards reschedule based on how you did, with a daily new-card allowance so "due today" is a real, finite target.
- **Study — quiz + flip hybrid** — each card shows the question with multiple-choice options *and* a "flip to the answer" option. Answer it (auto-graded) or flip if you don't know, then **Repeat** (see it again today) or **Next** (schedule it forward).
- **Focused decks** — click any deck on the dashboard to drill just that deck.
- **Mixed Quiz** — cross-deck, multiple-choice, auto-graded self-test. Does **not** affect your spaced-repetition schedule, so it's safe for exam-prep cramming.
- **Dashboard** — cards due today, streak, mastered count, and per-deck progress rings.
- **Deck manager** — enable/disable decks, add your own cards, JSON import/export, reset progress.
- **Keyboard-first** — `1–4` to answer, `Space` to flip; after reveal, `1`/`R` = Repeat, `2`/`Space`/`N` = Next; `Esc` ends a session. Undo (`← Back`) fully reverses the last card.

## Decks (200+ cards seeded)

**Foundations** (on by default): Governance & GRC mindset · Risk fundamentals · Vocabulary & acronyms

**Standards & frameworks**: ISO 27001 & 27002 · NIST (CSF 2.0 / RMF) · AI Governance (ISO 42001, EU AI Act, NIST AI RMF — with `42001-vs-aiact` contrast cards) · GDPR · Bahrain PDPL (+ Saudi PDPL / SDAIA distinction) · PCI DSS · SOC 2 · HIPAA

**Adjacent security** (optional, off by default, clearly *not* a compliance standard): OWASP Top 10 · OWASP Top 10 for LLMs · MITRE ATLAS · Zero Trust

All content is **paraphrased concept knowledge** — no copyrighted standard text is reproduced. Aimed at newcomer *retention* (foundations-level, e.g. ISC2 CC / CRISC territory).

## Run it

It's a single static file — no dependencies.

```bash
# just open it
open index.html

# or serve it (avoids any file:// quirks)
python3 -m http.server 8177
# then visit http://localhost:8177
```

All state (progress, streaks, custom cards) lives in your browser's `localStorage`. Use **Export JSON** in the Deck manager to back it up or move it between browsers.

## Tech & design

- Vanilla JS + HTML + CSS in one file. No framework, no build, no network calls (fonts degrade to system fallbacks offline).
- Design language: JetBrains Mono + Quicksand; dark palette with a pink accent.
- See [`PROJECT.md`](PROJECT.md) for the full spec and the SM-2 scheduling rules.

## Roadmap

- **Milestone 5** — flesh every deck out to full depth.
- **v1.1** — Stats view (reviews over time, retention %, longest streak).
- **Later** — cloze cards, concept map, shareable deck codes.

## Out of scope

No accounts, no server, no external calls. Educational content only.
