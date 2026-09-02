---
title: Set Up Your API Key (DeepSeek) — the 10-minute start
type: how-to
tags:
  - start-here
  - setup
  - api
  - deepseek
date: 2026-09-02
---

# Set Up Your API Key (DeepSeek) — the 10-minute start

*This is the one thing you need to do to make the vault talk. It takes about 10 minutes and costs pennies. The rest of the system waits on this.*

---

## Step 1 — Get a DeepSeek API key (free to create, pay-per-use)

1. Go to **https://platform.deepseek.com** and sign up / log in.
2. On the left menu, click **API Keys**.
3. Click **Create API Key**.
4. Give it a name (e.g. "Obsidian vault"), then **copy the key** it shows you. *(It looks like `sk-` followed by a long string.)*
5. **Optional but recommended:** top up a small amount of credit (e.g. £5) — DeepSeek is pay-per-use and very cheap, but a little credit means it always works. You can also use the free-tier Gemini option below instead.

> ⚠️ **Store the key safely — never in the vault notes.** Put it in a private file your assistant can read, e.g. `~/.config/deepseek-api.key` on a Mac, with restricted permissions. The vault itself must never hold a secret.

## Step 2 — Plug the key into the Obsidian Copilot plugin

1. Open **Obsidian Settings** (gear icon, bottom-left).
2. Go to **Community plugins → Copilot → Settings** (or click the Copilot chat panel's gear).
3. Find the **DeepSeek** provider (or "Add provider → DeepSeek").
4. Paste your API key.
5. **Reload Obsidian** (or restart) so it picks up the key.
6. In the Copilot chat, pick a DeepSeek model in the model dropdown and send a test message like *"Hello"*.

If it replies, you're live.

## Alternative — Free Gemini option

If you'd rather not add credit at all, DeepSeek also offers a **free tier** in some regions, or you can use **Google Gemini (AI Studio)** which has a free allowance:
1. Go to **https://aistudio.google.com** → **Get API key**.
2. Create a key, then plug it into the Copilot plugin's **Google/Gemini** provider instead.
3. Same steps as above.

Either works. DeepSeek is the cheap general workhorse; Gemini's free tier is handy for search and image/vision.

## Step 3 — Say hello and load in

1. Open the Copilot chat panel.
2. Say **"full load-in"** (or "load me in") — the assistant reads the Start Here notes and today's daily log and gets oriented.
3. Then ask **"what's next?"** whenever you want a single suggested action.

---

## Troubleshooting

- **"No model available" / auth error:** the key didn't paste cleanly, or the plugin needs a reload. Re-paste and reload Obsidian.
- **Empty key field but you set one:** the plugin may store keys in an encrypted internal store — re-enter through the Settings UI (not by editing files).
- **Costs too high:** you're unlikely to. DeepSeek is fractions of a penny per query. Keep threads short and you'll use almost nothing.

---

*Companion: [[Welcome to Hal]] · [[Keeping the System Healthy - Resilience and the Incident Playbook]] (has the credential-safety lesson).*
