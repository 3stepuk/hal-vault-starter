---
title: Operating Workflows — the nitty-gritty mechanics
date: 2026-08-30
tags:
  - start-here
  - workflow
  - mechanics
---

# Operating Workflows — the nitty-gritty mechanics

*How Hal physically operates your Mac: clipboard, text input, screen-reading, clicking, cutting/pasting. The mechanical layer under the high-level patterns.*

> **Read together:** [[Hal Workflows]] (the master patterns) · [[Capability Map]] (everything Hal can do). This is the operating layer.

---

## 1. The clipboard is the handshake

The single most important habit. Almost every interaction runs through the clipboard.

- **Give you a prompt / text to paste → `pbcopy` it first.** The ritual: *"the prompt's on your clipboard"* = Hal has copied it, you just paste. You should never have to copy it yourself.
- **Read what you copied → `pbpaste`.** When you say "look at this," check the clipboard first.

```bash
echo "text" | pbcopy        # put text on the clipboard
pbcopy < file.txt           # copy a file's contents
pbpaste                     # read the clipboard
```

**Always confirm the copy worked** — after `pbcopy`, immediately `pbpaste` to verify. Never hand over an empty clipboard.

---

## 2. Putting text into a field (three ways, in order)

### A. Safari JavaScript (preferred for web apps — AI Studio, chat sites, forms)
When you have the page open in Safari and "Allow JavaScript from Apple Events" is on:

```bash
osascript -e 'tell application "Safari" to do JavaScript "<js>" in front document'
```

For a textarea/input, inject the value **with the setter + native input events** so the app's state updates (plain `.value =` often doesn't fire React's onChange):

```js
var el = document.querySelector('<selector>');
var setter = Object.getOwnPropertyDescriptor(window.HTMLTextAreaElement.prototype,'value').set;
setter.call(el, '<text>');
el.dispatchEvent(new Event('input', {bubbles:true}));
```

- No mouse, no coordinates — solves multi-display coordinate problems entirely.
- Works in anything open in Safari (DeepSeek, Gemini, ChatGPT, Claude, Perplexity).
- Only in pages you have open, on your say-so. It acts as *you* in your logged-in session.

### B. Clipboard + Cmd-V (when the app is in focus and JS isn't available)
`pbcopy` the text, then send Cmd-V. Works for native apps and some web apps that reject JS injection.

### C. cliclick character-by-character (last resort — slow, fragile)
Avoid for long prompts (a long type can time out mid-word and truncate). Fine for short inputs or clicks:

```bash
cliclick c:<x>,<y>          # click at coordinates
cliclick t:"text"           # type text
cliclick kp:return          # press Return
```

**⚠️ Coordinate pitfalls:** dual-display negative coordinates are unreliable; devicePixelRatio scaling (DPR ≠ 1) makes pixel clicks miss. Prefer DOM positions / JS over raw coordinates.

---

## 3. Seeing the screen

- **Screenshot any display:** `screencapture -x -D <displayNum> /tmp/out.png` (display 1 = main).
- **Then read it** via the image-description skill (some engines can't see images directly — Hal uses a vision model as the eyes).
- **Screen Recording permission must be granted** for Hal to capture the display.

---

## 4. Reading the focused app

- **Safari:** `osascript -e 'tell application "Safari" to get URL of front document'` → see every tab's URL/title.
- **Notes / Calendar / Reminders / Contacts / Messages:** AppleScript (see [[Capability Map]]).
- **Clipboard:** `pbpaste` / `pbcopy` (see §1).

---

## 5. Cut, copy, paste inside an app

1. **Select:** `cliclick` drag-select, or Cmd-A (select all).
2. **Copy:** `pbcopy` (from selected text read via AppleScript) or Cmd-C.
3. **Paste:** Cmd-V after `pbcopy`.

Prefer **reading via AppleScript/Safari-JS → pbcopy → re-inject** over raw Cmd-C/V where possible — more reliable, doesn't depend on focus or selection.

---

## 6. The "see the input, fill it, verify" loop

1. **Locate** the text input — screenshot + describe, or query the DOM via Safari JS for a `textarea`/`input`.
2. **Fill** it via the best method from §2 (JS injection preferred).
3. **Trigger** the action (JS `.click()`, or `cliclick`, or let you click).
4. **Verify** — read the output back before reporting anything done. **Never claim without checking.**

---

## 7. Standing mechanical rules

- `pbcopy` before you say "it's on the clipboard" — and verify with `pbpaste`.
- Prefer Safari JS → DOM over coordinates (multi-display + DPR make raw clicks fragile).
- Never type long prompts with cliclick — use JS injection or clipboard+Cmd-V.
- Verify the result (grep/read/curl/pbpaste) before reporting done.
- Everything runs as you, on your say-so — local, never in a corporate cloud.

---

*Companion: [[Hal Workflows]] (the master patterns) · [[Capability Map]] · [[Welcome to Hal]].*
