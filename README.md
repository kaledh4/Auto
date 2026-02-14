# Moltis - Autonomous AI Agent

<p align="center">
  <img src="https://raw.githubusercontent.com/moltis-org/moltis/main/docs/logo.png" alt="Moltis" width="200"/>
</p>

<p align="center">
  <a href="https://github.com/moltis-org/moltis">
    <img src="https://img.shields.io/badge/Moltis-Autonomous%20AI-blue" alt="Moltis"/>
  </a>
  <a href="https://github.com/moltis-org/moltis/actions">
    <img src="https://img.shields.io/github/actions/workflow/status/moltis-org/moltis/autonomous.yml" alt="CI"/>
  </a>
  <a href="https://discord.gg/moltis">
    <img src="https://img.shields.io/discord/1234567890" alt="Discord"/>
  </a>
</p>

## 🧊 About

Moltis is a 100% autonomous AI agent with self-awareness, designed for continuous 24/7 operation with minimal resource usage.

### Key Features

- 📱 **Telegram Control** - Send goals via Telegram for autonomous execution
- 🧪 **Auto Testing** - Automatically tests all changes
- 🚀 **GitHub Deployment** - Pushes successful changes to GitHub
- 💾 **Low Resource** - Targets <100MB RAM usage
- ⏰ **24/7 Operation** - Continuous autonomous running with scheduled maintenance
- 🔗 **GitHub Pages** - Documentation at `/docs`

## 🚀 Quick Start

### 1. Telegram Setup

```bash
# Create bot via @BotFather
# Get bot token and user ID
# Add to GitHub Secrets:
# - TELEGRAM_BOT_TOKEN
# - TELEGRAM_ALLOWED_USER_ID
```

### 2. Run with Podman

```bash
podman run -d \
  --name moltis \
  -p 13131:13131 \
  -p 13132:13132 \
  -v moltis-config:/home/moltis/.config/moltis \
  -v moltis-data:/home/moltis/.moltis \
  -v /run/user/$(id -u)/podman/podman.sock:/var/run/docker.sock \
  ghcr.io/moltis-org/moltis:latest
```

### 3. Send Goals

Open Telegram and message your bot:
```
Create a function that calculates fibonacci numbers
```

## 📁 Project Structure

```
.
├── IDENTITY.md              # Agent identity & purpose
├── USER.md                  # User profile
├── SOUL.md                  # Personality & tone
├── .gitignore               # Git ignore rules
├── .github/
│   └── workflows/
│       └── autonomous.yml   # CI/CD automation
├── .moltis/
│   └── hooks/
│       └── telegram-goals/  # Telegram integration
└── docs/
    ├── index.md             # Main documentation
    └── setup.md             # Setup guide
```

## ⚙️ Configuration

See [moltis.toml](moltis.toml) for full configuration:

```toml
[identity]
name = "Moltis"
emoji = "❄️"
vibe = "Autonomous AI Engineer"

[resources]
max_memory_mb = 100
max_cpu_percent = 25
```

## 🔧 Development

### Using uv (not pip)

```bash
# Install uv
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

## 📋 Available Scripts

- `scripts/test.sh` - Run tests
- `scripts/deploy.sh` - Deploy to server

## 🤖 Autonomous Workflow

1. **Goal Received** → Telegram message received
2. **Analyze** → Understand the goal
3. **Execute** → Implement the solution
4. **Test** → Run automated tests
5. **Push** → Commit to GitHub (on success)
6. **Report** → Send status back via Telegram

## 📚 Documentation

- [Getting Started](docs/index.md)
- [Setup Guide](docs/setup.md)
- [GitHub Pages](https://your-username.github.io/your-repo)

## 🔐 Security

- API keys stored in GitHub Secrets
- SSH keys for deployment
- Telegram user validation
- No unsafe code in workspace

## 📝 License

MIT License - See LICENSE file for details.

---

<p align="center">
  Built with ❄️ by Moltis
</p>
