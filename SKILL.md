---
name: call
description: "Initiate or receive voice calls with Claude about your coding projects via Vapi. Use when the user wants to phone Claude, start a voice conversation, dial in for a project brainstorm, get a verbal status update, or talk through code changes hands-free."
allowed-tools: Bash, Read, Write, AskUserQuestion
user-invocable: true
triggers:
  - "voice call"
  - "phone call"
  - "call Claude"
  - "talk to Claude"
  - "dial"
  - "phone conversation"
  - "audio chat"
  - "brainstorm by phone"
  - "verbal update"
  - "hands-free"
---

# /call

Initiate or receive voice calls with Claude about your coding projects. Claude calls you (outbound) or you call a Vapi number and Claude answers with your project context preloaded — read files, search code, check git status, and brainstorm live.

## Quick Start

```bash
# One-time setup
pip install claude-code-voice
claude-code-voice setup              # Add API key, phone, name
claude-code-voice status             # Verify configuration is correct
# If status shows errors, re-run setup to fix API key or phone number

# Register a project
cd your-project
claude-code-voice register

# Start receiving calls (does everything automatically)
claude-code-voice start
# Look for "Server running" and a tunnel URL — both confirm it's ready
```

Now you can:
- **Outbound**: Run `claude-code-voice call` to have Claude call you
- **Inbound**: Call the Vapi number shown and Claude answers with your project loaded

## Commands

| Command | Description |
|---------|-------------|
| `setup` | Configure Vapi API key, your phone number, and name |
| `register` | Register current directory as a project |
| `start` | **Easy mode** — starts server + tunnel, configures everything |
| `call [topic]` | Have Claude call you about current/recent project |
| `status` | Verify configuration and connectivity |
| `config name <name>` | Update your name for personalized greetings |

## Features

### Personalized Greetings
Claude greets you by name: *"Hey Sarah! I've got my-project loaded up."*

Set your name during setup or update it:
```bash
claude-code-voice config name YourName
```

### Live Project Context
During calls, Claude can:
- Read your files
- Search your code
- Check git status
- See recent changes

### Auto-Sync Transcripts
Transcripts automatically save to `~/.claude/skills/call/data/transcripts/` when calls end.

## How It Works

1. **Setup** stores your Vapi API key and creates voice tools
2. **Verify** with `claude-code-voice status` to confirm API key and phone are configured
3. **Register** snapshots your project context (git status, recent files, etc.)
4. **Start** runs a local server + tunnel so Vapi can reach your code — look for "Server running" and a tunnel URL in the output
5. **Calls** use Opus 4.5 with your project context preloaded

## Requirements

- Vapi account with API key (https://dashboard.vapi.ai)
- Vapi phone number (purchase in dashboard ~$2/month)
- Node.js (for localtunnel)

## Troubleshooting

### Call doesn't connect
```bash
claude-code-voice status  # Check configuration
```

### Claude can't access files during call
Make sure `claude-code-voice start` is running in a terminal.

### "I don't recognize this number"
Call from the phone number you used during setup.

## Manual Setup (Advanced)

If you prefer manual control:

```bash
# Terminal 1: Start server
claude-code-voice server

# Terminal 2: Start tunnel
npx localtunnel --port 8765

# Verify tunnel is reachable before configuring
curl -s https://xxx.loca.lt | head -1

# Configure the tunnel URL
claude-code-voice config server-url https://xxx.loca.lt
claude-code-voice configure-inbound
```
