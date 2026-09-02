---
title: Keeping the System Healthy — Resilience & the Incident Playbook
type: how-to
tags:
  - workflow
  - resilience
  - obsidian
  - copilot
date: 2026-09-02
---

# Keeping the System Healthy — Resilience & the Incident Playbook

*The hard-won lessons from a real incident (1 Sep 2026): when a system "looks destroyed" but the data is intact. Written so a new vault operator can build the same calm into their setup from day one.*

## The core truth: data is almost never actually lost

The scariest moments in a local-first system are almost always **observability failures**, not data failures — the files are safe, but an *index* has drifted or a *stored credential* has gone missing. Before panicking or rebuilding, **diagnose.**

## Lesson 1 — Vault path names are infrastructure. Don't rename the vault folder.

The vault's chat/session database records sessions by **absolute directory path**. If you rename or move the vault folder, every existing session appears "lost" from the history view — **even though the data is intact**. The visible history filters by the current path, so old sessions vanish from view.

**The fix / guard:**
- Treat the vault root path as fixed infrastructure. Rename once at the start, then don't.
- If a session-count ever looks wrong, run a health check that compares total sessions vs. how many match the current path. Re-point stale paths in the database (after backing it up first).

## Lesson 2 — Health checks are read-only, calm, and instant

Build one small diagnostic that **only looks and reports** — it never repairs. It should check, in one glance:
- The vault root is where it should be
- The chat/session database exists and aligns with the current path
- The API keys are present (in `~/.config/`, never in the vault)
- The backup drives are mounted

Something like:

```
HAL SYSTEM HEALTH
Vault root: OK
Chat DB: 189 sessions — 189 match current path
Gemini credential: present
DeepSeek credential: present
Backup destinations: 3/3 available
No anomalies detected.
```

If something is wrong, it says *what* is wrong. It does not fix it — the human decides the fix. This turns a panic into a thirty-second diagnosis.

## Lesson 3 — Backups: one copy must remember yesterday

Exact-mirror backups (`rsync --delete`) are excellent against **disk failure** but weak against **accidental deletion** — because if files are wiped locally, the next mirror run faithfully propagates the deletion to every drive.

**The guard:** keep most mirrors exact, but make **one** destination versioned/rotating — retaining a few dated snapshots. The principle: *one copy must remember yesterday.*

## Lesson 4 — Credentials: master copy + reliable recovery path

- The **master** keys live in `~/.config/` (chmod 600) — *outside* the vault, backed up to the drives.
- A tool (like Obsidian Copilot) keeps its **own working copy** of each key, sometimes in an **encrypted secret store** — not necessarily in its plaintext config file.
- If a key stops working, the reliable recovery is to **re-enter it through the tool's Settings UI** (which writes to the encrypted store), pulling the value from `~/.config/`. 
- ⚠️ Don't write a script that pokes keys into a config file's *legacy/plaintext* fields unless you've verified the tool actually reads them — it can "succeed" while changing nothing that matters (false confidence).

## Lesson 5 — Lean is resilient: retire, don't fight the tool

When a tool or integration is brittle (won't behave as you want, or its API/security fights you), the resilient move is usually to **work with what it does** rather than engineer around it — or to **retire it** and use the simpler reliable path. Every extra tool, provider, or stored credential is another thing that can silently break.

Examples of the lean call:
- A capture tool that fragments notes → let it, and consolidate at a fixed daily ritual (see [[Voice Capture - dictate freely, consolidate at load-in]]).
- An API token that keeps expiring and needs manual refreshing → drop it and use a manual clipboard handshake instead.
- A credential-restore script aimed at the wrong store → retire it and document the 60-second UI fix.

## The incident playbook (when it "all looks gone")

1. **Stop. Do not rebuild or delete anything.**
2. **Run the health check** — is it data loss, or an index/credential drift?
3. **Check the obvious first:** vault path unchanged? keys in `~/.config/`? drives mounted? sessions count sane?
4. **Back up the database before touching it.**
5. **Diagnose → fix the specific drift → verify.**
6. **Document the lesson** so the same scare doesn't repeat.

---

*Added 2 Sep 2026. Companion notes: [[Welcome to Hal]], [[Hal Workflows]], [[Voice Capture - dictate freely, consolidate at load-in]].*
