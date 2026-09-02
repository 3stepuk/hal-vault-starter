---
title: Voice Capture — Dictate freely, consolidate at load-in
type: how-to
tags:
  - workflow
  - voice
  - obsidian
  - copilot
date: 2026-09-02
---

# Voice Capture — Dictate freely, consolidate at load-in

**The lesson (learned 2 Sep 2026):** don't fight a capture tool's quirks. Let it do its simple job, and put the *tidying* where the assistant is actually reliable.

## The pattern

Dictate on the move (phone → iOS Shortcut → Apple Notes). Each dictation lands as a dated note in a dedicated **"Hal"** folder in Apple Notes.

**The quirk:** the Shortcut doesn't reliably append to a single note — some days it creates **several notes sharing the same date-name** (the tool can't tell identical names apart). That's fine. We don't try to make the capture perfect.

## The model

1. **Capture freely.** Dictate whenever the mood takes you. Each capture is a dated note in the Hal folder.
2. **Consolidate at load-in / wrap.** The assistant reads all of that day's dictation notes → merges them into **one** "DD Mon YYYY" note → deletes the duplicates → imports the merged content into the vault **daily log**.
3. **The vault is the single clean memory.** Apple Notes is just the capture tray — never the archive.

**Date-name format:** always "2 Sep 2026" (day + three-letter month + year). Never "1st September" or "1 September 2026" — consistent naming keeps the merge simple.

## Why this is the right shape

- **Lean is resilient.** Don't engineer around a brittle tool; work *with* what it does.
- **The vault is the memory.** Consolidation happens where content is plain-text, searchable, and backed up.
- **Gentle pace.** You dictate when inspiration strikes; the tidying happens at a fixed daily rhythm, not in the moment.

## What the assistant needs

- Read Apple Notes (AppleScript) — the "Hal" folder.
- The import ritual (`import_voice_notes.py`) pulls dictation into the daily log.
- Fold the consolidation step into the **daily load-in** and **end-of-day wrap** rituals.

---

*Added 2 Sep 2026. Companion note: [[Hal Workflows]].*
