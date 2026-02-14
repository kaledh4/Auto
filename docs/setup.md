# Setup Guide

## GitHub Secrets Configuration

This guide explains how to set up the required secrets for autonomous operation.

### Required Secrets

Go to your repository Settings → Secrets and variables → Actions and add:

| Secret Name | Value | How to Get |
|-------------|-------|------------|
| TELEGRAM_BOT_TOKEN | `123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11` | @BotFather on Telegram |
| TELEGRAM_ALLOWED_USER_ID | `123456789` | @userinfobot on Telegram |
| GITHUB_TOKEN | (auto-generated) | GitHub creates this automatically |
| SSH_PRIVATE_KEY | `-----BEGIN OPENSSH PRIVATE KEY-----\n...` | Generate with `ssh-keygen -t ed25519` |
| SERVER_HOST | `your-server.com` | Your server IP or hostname |

### Optional Secrets

| Secret Name | Value | How to Get |
|-------------|-------|------------|
| GROQ_API_KEY | `gsk_...` | groq.com |
| OPENAI_API_KEY | `sk-...` | platform.openai.com |
| GEMINI_API_KEY | `AIza...` | aistudio.google.com |

### Setting Up SSH for Deployment

1. Generate a new SSH key (don't use an existing one):
   ```bash
   ssh-keygen -t ed25519 -C "moltis-deploy"
   ```

2. Add the public key to your server:
   ```bash
   ssh-copy-id -i ~/.ssh/moltis_deploy.pub user@server
   ```

3. Add the private key to GitHub Secrets as `SSH_PRIVATE_KEY`

4. Add your server hostname as `SERVER_HOST`

### Telegram Bot Setup

1. Open Telegram and search for @BotFather
2. Send `/newbot` to create a new bot
3. Follow the prompts to name your bot
4. Copy the bot token shown
5. Add to GitHub Secrets as `TELEGRAM_BOT_TOKEN`

### Getting Your Telegram User ID

1. Open Telegram and search for @userinfobot
2. Start the bot
3. It will show your user ID
4. Add to GitHub Secrets as `TELEGRAM_ALLOWED_USER_ID`

### Testing the Setup

After setting up secrets:

1. Push a test commit to trigger the workflow
2. Go to Actions tab to see the workflow running
3. Check that tests pass
4. Manually trigger a deploy to verify server access

### Troubleshooting

**Workflow fails on test:**
- Check that dependencies are properly configured
- Ensure `uv` is used for Python projects

**Deploy fails:**
- Verify SSH key is correctly added to server
- Check SERVER_HOST is correct
- Ensure podman/docker is running on server

**Telegram not working:**
- Verify bot token is correct
- Check user ID is properly added to allowed list
- Ensure the bot is started by the user
