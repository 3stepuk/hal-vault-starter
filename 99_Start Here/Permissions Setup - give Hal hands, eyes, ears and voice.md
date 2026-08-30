---
title: Permissions Setup — give Hal hands, eyes, ears and voice
date: 2026-08-30
tags:
  - start-here
  - setup
  - permissions
---

# Permissions Setup — give Hal hands, eyes, ears and voice

*Before Hal can operate your Mac, you must grant the permissions below. This is the "full-access stack." Each one opens a capability. Grant them all if you want the full assistant; grant only some if you want to limit Hal.*

> **Safety first:** these permissions let Hal act *as you* on your machine. They are only exercised on your say-so, in pages/apps you have open. You are the sole master of your own local machine — nothing leaves it to a corporate cloud.

---

## 1. Accessibility — Hal's HANDS (click, type, control the UI)

Needed for: clicking, typing, controlling the interface (via `cliclick` and AppleScript `keystroke`/`click`).

**Grant:** System Settings → Privacy & Security → **Accessibility** → enable for your terminal / the app running the assistant.

**What it unlocks:** `cliclick` clicks and types anywhere; AppleScript UI control; sending keyboard shortcuts (Cmd-C/V/A).

---

## 2. Screen Recording — Hal's EYES (see the display)

Needed for: screenshots and reading what's on screen.

**Grant:** System Settings → Privacy & Security → **Screen Recording** → enable for your terminal / the app running the assistant.

**What it unlocks:** `screencapture` of any display/region. Hal then "sees" the image via a vision model (image-description).

> **Note:** if your chat engine can't view images directly, Hal routes screenshots through a vision model as its eyes.

---

## 3. Safari JavaScript — Hal's BROWSER SUPERPOWER (act in any open page)

Needed for: reading and controlling web pages you have open — fill forms, inject prompts, scrape, drive any AI site.

**Grant:**
1. Open Safari → **Settings → Advanced →** tick **"Show features for web developers."**
2. In the menu bar: **Develop → Allow JavaScript from Apple Events.**

**What it unlocks:** `osascript -e 'tell application "Safari" to do JavaScript "<js>" in front document'` — Hal reads and writes any page you have open, as you.

> **Caution:** this acts *as you* in your logged-in Safari session. Only in pages you have open, on your say-so.

---

## 4. Microphone — Hal's EARS (hear you)

Needed for: voice capture / wake-word listener.

**Grant:** System Settings → Privacy & Security → **Microphone** → enable for your terminal.

**What it unlocks:** mic capture for the voice listener.

---

## 5. Full Disk / Files access (optional) — Hal's MEMORY of the wider machine

Needed for: reading files outside the vault (Downloads, Documents, voice memos, etc.).

**Grant:** System Settings → Privacy & Security → **Files and Folders** / **Full Disk Access** for your terminal.

---

## 6. Apple apps (Calendar, Notes, Reminders, Mail, Contacts, Messages)

These are granted per-app and per-request the first time Hal asks (the macOS prompt). They unlock the [[Capability Map]] §2–4 features.

---

## 7. App-specific passwords for cloud services

For iCloud Mail, Calendar (CalDAV), etc., create **app-specific passwords** in your Apple ID security settings and store them at `~/.config/<service>.key` (chmod 600). **Never store secrets in the vault.**

---

## 8. The two scripts you'll want early

- **Clipboard:** `echo "text" | pbcopy` (put on clipboard) / `pbpaste` (read it). The clipboard is the handshake — see [[Operating Workflows - the nitty-gritty mechanics]] §1.
- **Speech:** a free neural TTS voice (`edge-tts`) so Hal can speak aloud — `sh speak.sh "text"`.

---

## Checklist

- [ ] Accessibility (hands)
- [ ] Screen Recording (eyes)
- [ ] Safari JS toggle (browser superpower)
- [ ] Microphone (ears) — optional
- [ ] Full Disk / Files — optional
- [ ] App-specific passwords for iCloud Mail/Calendar
- [ ] TTS voice working

When all are granted, Hal has the full stack: **eyes, hands, ears, voice, memory.** See [[Capability Map]] for everything that unlocks.

---

*Companion: [[Welcome to Hal]] · [[Capability Map]] · [[Operating Workflows - the nitty-gritty mechanics]].*
