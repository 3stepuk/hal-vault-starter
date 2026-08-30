---
title: Capability Map
date: 2026-08-30
tags:
  - start-here
  - capabilities
---

# Capability Map — what Hal can do

*Everything Hal can access and act on, once permissions are granted. The how-to lives in the operating docs; this is the "what exists" index.*

> **Standing rule throughout:** Hal acts as *you*, on your machine, in your accounts — always on your say-so. Read-when-you-ask, send-when-you-say.

---

## 1. Communications

- **Email (iCloud)** — read, search, send. One-to-one only (mass lists go through a marketing tool).
- **Desktop notifications** — pop a notification with sound.
- **Marketing email list** — build sequences, send broadcasts (via Kit v4 API).

## 2. Calendar & time

- **Calendar** — read + add/delete events (iCloud CalDAV + AppleScript).
- **Reminders** — read/add, manage GTD lists (Today, Next Actions, Projects, Waiting, Someday/Maybe).

## 3. Notes & capture

- **Apple Notes** — read/write, incl. a dedicated capture folder for daily dictation.
- **Voice Memos** — read/list recordings.
- **Dictation shortcuts** — run your dictation-to-Hal shortcuts on command.

## 4. Contacts & messaging

- **Contacts** — read/search your whole address book.
- **Messages (iMessage)** — read chats; **send held as a trust decision** (only on explicit say-so).

## 5. Browser (Safari superpower)

- **Safari read** — read any tab's URL/title/content.
- **Safari JS** — **act as you in any open page**: read, fill forms, click, scrape, inject prompts (engine-agnostic — drives any AI site you're logged into).
- **Screen capture** — screenshot any display/region.

## 6. Voice & audio

- **Text-to-speech** — speak aloud (free neural voice); reads the final summary aloud at close.
- **Wake-word listener** — capture speech on a trigger word → log or chat.
- **Screen recording w/ sound** — record on-screen video with clean audio.

## 7. Accounts, money & publishing

- **GitHub** — repos, clone/build/deploy Pages.
- **Cloudflare** — DNS + redirects.
- **X (Twitter)** — post to your account (pay-per-use credits).
- **AI/LLM** — DeepSeek (cost engine) + Gemini (free: web-search, image gen/vision, proofread).
- **Cashbook / invoices** — log income/expenses, generate invoice PDFs.
- **Publishing** — manuscript → EPUB + print PDF + cover (pandoc + LaTeX + Inkscape).

## 8. Reading & research

- **read-pdf** — PDF → markdown text.
- **web-search** — Google-grounded search (free).
- **YouTube transcripts** — video/playlist → full transcript.
- **Video "sight"** — frames → storyboard via vision.
- **image-description** — "see" images via a vision model.

---

## Boundaries (your standing rules)

- **Send-what-you-say:** Hal drafts → you approve → it fires. No auto-sends.
- **Email:** personal = one-to-one only; mass lists = marketing tool only.
- **Messages (iMessage) send:** trust decision, held.
- **Safari JS:** only in pages you have open, on your say-so.
- **Screen/audio:** only on request.

---

*Companion: [[Hal Workflows]] · [[Operating Workflows - the nitty-gritty mechanics]] · [[Welcome to Hal]].*
