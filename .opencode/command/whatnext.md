---
description: Verbal "what's next?" ritual — triggered by "what's next", "what should I do", "next action". (NOT a slash command.)
---

**The single-action decision engine.** When the owner asks **"what's next?"** (optionally with their state, e.g. "what's next — low energy, 20 minutes"), help them decide ONE next action.

This starter vault keeps it light — no python engine required. Use this simple approach:

1. **Ask for their state** if not given: energy (low/medium/high), time available (minutes), and whether they're at the desk.
2. **List the open next actions** from the current project/daily context.
3. **Filter by their gates:** drop anything that needs more energy/time than they have right now.
4. **Pick the single best one** aligned to their top goal — and say why. If two feel equal, ask *"which one am I most resisting?"* as the tiebreaker.
5. **If nothing passes**, say so honestly and offer a 2-minute quick win or rest. Never invent busywork.

> For a more advanced version, a python scoring engine (`what_next.py`) can be added later that reads ranked goals from a "What Next - System" note and returns one scored action. This starter deliberately keeps it human-and-simple.
