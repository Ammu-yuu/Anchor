# Anchor

A spaced-repetition flashcard app for learning **Governance, Risk & Compliance (GRC)** — engaging, self-contained, offline-first, and built in Kyther's visual language.

## One-liner
Help a GRC learner actually *retain* frameworks, controls, risk concepts, and vocabulary through short daily study sessions — not passive reading. Built as a sibling to Kyther.

## Why it exists
The author is actively studying GRC and sitting real certifications (ISO 27001 Lead Implementer, IAPP AIGP). Anchor is the tool to make that material stick, and the decks are tuned to reinforce what's known, feed the in-progress certs, and pre-load radar topics.

---

## Product decisions (locked)
- **Separate app, its own repo** — not part of Kyther. No OSINT, no Kyther code.
- **Full spaced repetition** (SM-2), not just flip cards.
- **Single self-contained `index.html`** — vanilla JS, no framework, no build step, no backend.
- **All state in `localStorage`** — decks, progress, streaks. Keyless. Works offline.
- **JSON import/export** so decks and progress are portable/backup-able.

---

## Design language
- **Fonts:** JetBrains Mono (data/UI) + Quicksand (titles)
- **Palette ("jellyfish" — deep navy with lavender/periwinkle glows):**
  - bg `#0a0e3a`
  - panel `#151c58`
  - border `#2d3778`
  - text `#eae7fb`
  - dim `#8f97d0`
  - accent — Verbena `#b37ad4` (gradients pair with Periwinkle `#7997e6`)
  - success — teal `#4fd6b0`
  - warn — amber `#e0b34e` (learning state)
  - source swatches: Phlox `#caa9f3`, Verbena `#b37ad4`, Periwinkle `#7997e6`, Atlantis `#206abc`, Phthalo Blue `#0e155e`
- **Spacing scale:** `--pad: 20px`, `--gap: 26px`, `--radius: 8px`

---

## Views
1. **Dashboard** — cards due today, current streak, per-deck progress (New / Learning / Mastered). One big "Start studying" button.
2. **Study session** — one card at a time: front → flip (Space) → back, then rate recall **Again / Hard / Good / Easy** (keys 1–4). Card reschedules on rating. Session progress bar.
3. **Decks** — browse/enable decks, see counts, add/edit your own cards, import/export JSON.
4. **Mixed Quiz** — pick any set of decks (or all), get a shuffled cross-deck test. **Does NOT touch SM-2 scheduling** — a no-consequences self-test for exam prep.
5. **Stats** *(v1.1)* — reviews over time, retention %, mastered count, longest streak.

---

## Spaced-repetition engine (SM-2, simplified)
Per card store `{ ease, interval, reps, due, lapses, state }`:
- **Again** → `reps=0`, `interval=0` (relearn today), `ease −0.20`, `state=Learning`, `lapses++`
- **Hard** → `interval ×1.2`, `ease −0.15`
- **Good** → first time 1 day → 6 days → then `interval ×ease`
- **Easy** → longer jump, `ease +0.15`
- Clamp `ease ≥ 1.3`; `due = today + interval`.
- Dashboard surfaces cards where `due ≤ today`.

Card format: `{ deck, front, back, hint?, tags[] }`.
Back = concise answer + a one-line **"why it matters."**
All content is **paraphrased concept knowledge — never copyrighted standard text.**

---

## Decks (11 + 1 optional)

### Foundations — default ON
1. **Governance & GRC mindset** — three lines of defense, roles (board/CISO/risk owner/control owner/DPO), control types (preventive/detective/corrective), policy→standard→procedure→guideline.
2. **Risk fundamentals** — inherent vs residual, likelihood × impact, appetite vs tolerance vs capacity, the 4 treatments (accept/mitigate/transfer/avoid), KRIs vs KPIs, risk register.
3. **Vocabulary & acronyms** — the trip-up terms: RTO/RPO, SoD, DLP, IAM, least privilege, attestation, materiality, control gap, compensating control, GRC vs IRM.

### Standards & frameworks — each its own deck
4. **ISO 27001 & 27002** ⭐ *(feeds Lead Implementer)* — ISMS clauses 4–10, PDCA, SoA, risk treatment plan, Annex A 2022 control themes. Sibling refs: ISO 31000, 27005.
5. **NIST** — CSF 2.0 (Govern/Identify/Protect/Detect/Respond/Recover), Tiers & Profiles, 800-53 vs 800-171, RMF.
6. **AI Governance** ⭐ *(feeds AIGP)* — ISO 42001 (AIMS), EU AI Act (risk tiers), NIST AI RMF (Govern/Map/Measure/Manage). Includes **contrast cards** tagged `42001-vs-aiact` that explicitly separate the voluntary certifiable standard (42001) from binding regulation (EU AI Act).
7. **GDPR** — lawful bases, data-subject rights, controller vs processor, 72-hr breach notice.
8. **Bahrain PDPL** — real cards; includes a card flagging the **Saudi PDPL / SDAIA** distinction. (Bahrain-market differentiator.)
9. **PCI DSS** — cardholder data, SAQ, segmentation.
10. **SOC 2** — the 5 Trust Services Criteria, Type I vs Type II.
11. **HIPAA** — PHI, Privacy vs Security Rule, covered entity vs business associate.

### Adjacent security — optional, default OFF, labeled "not a compliance standard"
12. **Adjacent security** — OWASP Top 10, OWASP Top 10 for LLM Applications, MITRE ATLAS, Zero Trust. Kept distinct from GRC standards on purpose.

**Currency note:** ISO 27001/27002 = 2022 revision; NIST CSF = 2.0 (2024). Decks are dated; paraphrasing kept framework-agnostic where possible.

**Depth:** newcomer *retention* level (foundations-level bar, e.g. ISC2 CC / CRISC territory) — enough to hold a conversation and pass a foundations exam, not audit-grade citation.

---

## Engagement touches
- Smooth card-flip animation; keyboard-first (Space flips, 1–4 rate, Esc ends).
- Streak counter + small celebration when a deck hits "Mastered."
- Progress rings per deck; "you're done for today" empty state.

---

## Build order (milestones)
1. Shell + design tokens + one hardcoded deck rendering as flip cards.
2. Study loop with Again/Hard/Good/Easy + localStorage progress.
3. SM-2 scheduling + "due today" dashboard + streak.
4. Deck management + JSON import/export + Mixed Quiz mode.
5. Write out the full GRC decks.
6. **v1.1:** Stats view + polish (animations, empty states).

## Out of scope
No accounts, no server, no external calls, no OSINT/Kyther code. Content is educational and paraphrased — no copyrighted standard text reproduced.

## Later stretch
Cloze (fill-in-the-blank) cards, concept map, shareable deck codes.
