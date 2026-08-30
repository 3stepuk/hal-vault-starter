---
title: Hal Workflows — the master patterns
date: 2026-08-30
tags:
  - start-here
  - workflow
---

# Hal Workflows — how we work

*The repeatable patterns. If it worked once and could work again, it belongs here. For the mechanical "how Hal touches the machine" detail, see [[Operating Workflows - the nitty-gritty mechanics]].*

---

## The master pattern — "write, copy, paste, Hal wires it up"

The single most used workflow (proven across AI Studio builds).

1. **Hal writes the full prompt** — self-contained, exact requirements, no ambiguity.
2. **Hal copies it to your clipboard** — `pbcopy` — nothing to type or hunt for.
3. **You paste it** into the target tool (Google AI Studio, etc.).
4. **You click run/build** where the tool needs a human hand.
5. **Hal does the wiring after** — GitHub repo, Pages deploy, file placement, verification.

> **Ritual:** "the prompt's on your clipboard" = Hal has copied it, you just paste. If you ever have to copy it yourself, that's a gap — Hal should have done it.

---

## 1. Build an app / site in Google AI Studio → publish to GitHub Pages

1. **Hal writes the master-prompt** (self-contained: UI, data, behaviour, constraints — and "no backend, no API calls, no AI, must run statically" unless AI is genuinely wanted).
2. **Hal copies it to clipboard** (`pbcopy`). You paste into AI Studio, click run.
3. **AI Studio builds it.** Export via **Download-as-zip** (or direct GitHub export) — the in-app "Push to GitHub" dialog is unreliable via scripted clicks.
4. **Hal clones, builds, deploys:**
   - make repo public first
   - secret check: `git ls-files | grep -iE "\.env|secret|key"` (only `.env.example` allowed)
   - set `base: '/<RepoName>/'` in `vite.config.ts`
   - `npm install && npm run build`
   - orphan `gh-pages` branch with `index.html` + `assets/` at the root only (never `dist/`, never `git add -A`)
   - check the Pages source branch — set to `gh-pages` if it points at `main`
   - **force a rebuild** (`gh api -X POST .../pages/builds`) — switching source does NOT auto-rebuild
   - verify the real asset URLs return 200
5. **Register it** in a launch log.

*Blank-screen failure (Mentalism Practice App) was this runbook missed once: source deployed instead of build, no base path, wrong Pages source branch, no forced rebuild.*

---

## 2. The two-engine pattern

For launch/research prompts, run the **same prompt through BOTH engines and synthesize** (free, minutes).

- **DeepSeek** → targets, email mechanics, precise structure.
- **Gemini** → copy, voice, fresh angles.

**Hal's job:** draft one prompt → run it through both (via Safari JS) → capture both answers → synthesise into one filed result.

---

## 3. Send-what-you-say email

- **Hal drafts** → **you approve** → **Hal sends**. No auto-sends.
- Boundary: personal SMTP = one-to-one only; mass lists = a marketing tool (Kit) only.

---

## 4. Load-in & wrap rituals (voice-first)

- **"Full load-in"** / "load me in" / "start the day" → read the State of the Union + daily log + appointments, check inbox + `#hal-look`, balance + pricing window, import voice notes, prioritised what-needs-doing.
- **"Wrap it up"** → import voice notes, update daily log, refresh carry list, ready-check.
- Slash commands don't work in the chat box (opens Obsidian's searcher) — rituals are voice-first.

---

## 5. Standing rules (across all workflows)

- **Send-what-you-say** — Hal drafts, you approve, it fires.
- **Clipboard first** — whenever Hal hands you a prompt, it's on the clipboard already.
- **Verify before claiming** — grep/read/curl/pbpaste before telling you something is done.
- **Your eyes are the source of truth** — for images, names, labels (AI descriptions are not).
- **Learning all the time** — every failure gets a written post-mortem.

---

*Companion: [[Operating Workflows - the nitty-gritty mechanics]] · [[Capability Map]] · [[Welcome to Hal]].*
