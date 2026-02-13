# 🚫 SECURITY RULES — NEVER BREAK THESE

## Rule #1: NEVER push secrets to this repo
- **No API keys** (Google, OpenRouter, OpenAI, etc.)
- **No bot tokens** (Telegram, Discord, etc.)
- **No passwords or PATs**
- **No `.toml` config files** containing keys
- **No database files** (`.db`, `.sqlite`)

## Rule #2: This repo is DOCS ONLY
The `/docs` folder contains **only `.md` files** for the Knowledge Base dashboard.
- ✅ Markdown files (`.md`)
- ✅ README
- ✅ `.gitignore`
- ❌ Everything else stays on the VPS

## Rule #3: Backend stays on the VPS
These paths are **local only** and must NEVER be committed:
- `/etc/moltis/` — Moltis config (has API keys)
- `/var/lib/moltis/` — Moltis data (has bot tokens)
- `/root/Medo/` — Private knowledge base data
- `/root/scripts/` — Backend automation scripts

## Rule #4: Use GitHub Secrets for any keys
If a GitHub Action or workflow needs a key, add it as a **Repository Secret** in:
`Settings → Secrets and variables → Actions`

Never hardcode keys in any file that gets committed.

## Rule #5: .gitignore is sacred
The `.gitignore` file blocks all dangerous patterns. Never remove entries from it.

---

*Created: 2026-02-13. These rules are permanent.*
