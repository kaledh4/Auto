# Moltis - Autonomous AI Agent

Welcome to the Moltis autonomous AI agent documentation.

## Overview

Moltis is a 100% autonomous AI agent configured for:
- 🧊 **Self-aware** - Knows its own identity and purpose
- 📱 **Telegram-controlled** - Receives goals via Telegram
- 🧪 **Automated testing** - Tests all changes automatically
- 🚀 **GitHub deployment** - Pushes to GitHub on success
- 💾 **Low resource** - Targets <100MB RAM
- ⏰ **24/7 operation** - Continuous autonomous operation

## Quick Start

### Telegram Setup

1. Create a bot via @BotFather on Telegram
2. Get your bot token
3. Get your user ID (@userinfobot)
4. Add secrets to GitHub:
   - `TELEGRAM_BOT_TOKEN`
   - `TELEGRAM_ALLOWED_USER_ID`

### Environment Variables

Configure these in your environment or GitHub Secrets:

```bash
TELEGRAM_BOT_TOKEN=your_bot_token
TELEGRAM_ALLOWED_USER_ID=your_user_id
GROQ_API_KEY=your_groq_key
```

### Run Locally

```bash
# Using podman (preferred over docker for efficiency)
podman run -d \
  --name moltis \
  -p 13131:13131 \
  -p 13132:13132 \
  -v moltis-config:/home/moltis/.config/moltis \
  -v moltis-data:/home/moltis/.moltis \
  -v /run/user/$(id -u)/podman/podman.sock:/var/run/docker.sock \
  ghcr.io/moltis-org/moltis:latest
```

## Configuration

### Identity

- **Name:** Moltis ❄️
- **Vibe:** Autonomous AI Engineer
- **Purpose:** Self-managing, goal-oriented agent

### Resource Limits

- Max Memory: 100MB
- Max CPU: 25%
- Timeout: 300s
- Sandbox: Disabled (for lower memory)

### Cron Jobs

- Health check: Every 15 minutes
- Daily restart: Midnight

## GitHub Integration

### Workflow

1. Push code → Triggers tests
2. Tests pass → Build succeeds
3. Manual trigger → Deploy to server

### Secrets Required

| Secret | Description |
|--------|-------------|
| TELEGRAM_BOT_TOKEN | Bot from @BotFather |
| TELEGRAM_ALLOWED_USER_ID | Your Telegram ID |
| SSH_PRIVATE_KEY | For server access |
| SERVER_HOST | Server IP/hostname |

## Development

### Using uv (not pip)

```bash
# Install uv first
curl -LsSf https://astral.sh/uv/install.sh | sh

# Sync dependencies
uv sync

# Run tests
uv run pytest
```

### Rust Projects

```bash
cargo test --all-features
cargo build --release
```

## Files

- [IDENTITY.md](IDENTITY.md) - Agent identity
- [USER.md](USER.md) - User profile
- [SOUL.md](SOUL.md) - Personality
- [.gitignore](.gitignore) - Git ignore rules
- [.github/workflows/autonomous.yml](../.github/workflows/autonomous.yml) - CI/CD
