# ⚓ Anchor

A spaced-repetition flashcard app for learning **Governance, Risk & Compliance (GRC)**. Short daily study sessions that actually make frameworks, controls, and vocabulary stick — not passive reading.

Built as a self-contained sibling to Kyther: one `index.html`, vanilla JS, no build step, no backend, works offline.

## Features

- **Spaced repetition (SM-2)** — cards reschedule based on how you did, with a daily new-card allowance so "due today" is a real, finite target.
- **Study — quiz + flip hybrid** — each card shows the question with multiple-choice options *and* a "flip to the answer" option. Answer it (auto-graded) or flip if you don't know, then **Repeat** (see it again today) or **Next** (schedule it forward).
- **Focused decks** — click any deck on the dashboard to drill just that deck.
- **Mixed Quiz** — cross-deck, multiple-choice, auto-graded self-test. Does **not** affect your spaced-repetition schedule, so it's safe for exam-prep cramming.
- **Dashboard** — cards due today, streak, mastered count, and per-deck progress rings.
- **Stats** — current & longest streak, days studied, total reviews, a 14-day reviews chart, retention %, and a cards-by-state breakdown, plus an in-app explainer of how streak/mastered/storage work.
- **Recap** — review the cards you've already seen (most recent first), without affecting your spaced-repetition schedule.
- **Deck manager** — enable/disable decks, add your own cards, JSON import/export, reset progress.
- **Keyboard-first** — `1–4` to answer, `Space` to flip; after reveal, `1`/`R` = Repeat, `2`/`Space`/`N` = Next; `Esc` ends a session. Undo (`← Back`) fully reverses the last card.

## Decks (320 cards seeded, all on by default)

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

## Install on your phone / computer (offline PWA)

Anchor is an installable, offline-first PWA. Once it's hosted (see below), open the URL and:

- **iPhone (Safari):** Share → **Add to Home Screen**. It opens full-screen like an app and works with no internet.
- **Android (Chrome):** menu → **Install app** / Add to Home Screen.
- **Desktop (Chrome/Edge):** install icon in the address bar.

A service worker caches the app, so after the first load it runs fully offline — perfect for studying while travelling. Your progress saves locally on each device as you go.

### Hosting it (GitHub Pages, free)

The repo is a static site, so GitHub Pages serves it directly:

1. Repo **Settings → Pages**.
2. **Source: Deploy from a branch**, **Branch: `main`**, **Folder: `/ (root)`**, Save.
3. After a minute it's live at `https://<user>.github.io/Anchor/`.

## Sync setup (cross-device, free — optional)

Studying works offline with no account. To sync **progress + streak across devices**, add a free Firebase backend (the merge is conflict-free: card progress takes the most recent review, study-days are unioned so the streak is always right, reviews dedupe by id):

1. Create a free project at [console.firebase.google.com](https://console.firebase.google.com) (no card needed).
2. Add a **Web app** (`</>`), copy the `firebaseConfig` object it shows you.
3. **Build → Firestore Database → Create database**.
4. **Build → Authentication → Sign-in method → enable Anonymous.**
5. Set Firestore **Rules** to (this scopes access to the app's collection for signed-in clients):
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /anchor/{code} { allow read, write: if request.auth != null; }
     }
   }
   ```
6. In `index.html`, replace `const FIREBASE_CONFIG = null;` with your config object, e.g.
   `const FIREBASE_CONFIG = { apiKey: "…", authDomain: "…", projectId: "…", … };`
7. Redeploy. Then on each device: **Stats → Sync across devices** → **Generate** a code on one device, enter the **same code** on the other, hit **Sync now**.

**Note:** this is a shared-secret model — anyone who knows your sync code (and the app URL) could read/write that code's data. Use the generated 8-character code and don't share it. It's meant for your own devices.

## Tech & design

- Vanilla JS + HTML + CSS in one file. No framework, no build, no network calls (fonts degrade to system fallbacks offline).
- Design language: JetBrains Mono + Quicksand; dark palette with a pink accent.
- See [`PROJECT.md`](PROJECT.md) for the full spec and the SM-2 scheduling rules.

## Roadmap

- ~~Milestone 5 — flesh every deck out to full depth.~~ ✓ (284 cards)
- ~~Stats view~~ ✓ · ~~Offline PWA + optional cross-device sync~~ ✓
- **Later** — cloze cards, concept map, shareable deck codes.

## Notes

Core app has no server and works fully offline. The optional Firebase sync is the one external dependency, and only runs when you've configured it and set a sync code. Educational content only, paraphrased — no copyrighted standard text.
