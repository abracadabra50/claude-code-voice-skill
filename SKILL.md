---
name: call
description: Voice conversations with Claude about your projects. Call a phone number to brainstorm, or have Claude call you with updates. (user)
allowed-tools: Bash, Read, Write, AskUserQuestion
user-invocable: true
---

# /call

Voice conversations with Claude about your projects.

## Quick Reference

```bash
claude-code-voice call "topic"              # Make a call
claude-code-voice status                    # Check setup status
claude-code-voice config server-url <url>   # Set context server URL
```

## Before Making a Call

Always check status first:
```bash
claude-code-voice status
```

This shows:
- `API Key: ✅ Set` - Vapi configured
- `Your Phone: +1...` - User's phone number
- `Vapi Number: +1...` - Outbound caller ID
- `Server URL: https://...` - Context server (optional, for live file access)
- `Tools: 4 configured` - Vapi tools ready

### If Not Set Up

Run interactive setup:
```bash
claude-code-voice setup
```

User needs:
1. Vapi API key from https://dashboard.vapi.ai
2. Their phone number
3. A Vapi phone number (purchased in dashboard)

### If "Server URL: ❌ Not set"

This is optional. Without it, calls work but can't read files live. To enable:

```bash
# Terminal 1
claude-code-voice server

# Terminal 2
npx localtunnel --port 8765
# Copy the https://xxx.loca.lt URL

# Then run:
claude-code-voice config server-url https://xxx.loca.lt
```

## Making Calls

```bash
# Call about current project
claude-code-voice call

# Call with specific topic
claude-code-voice call "let's debug the auth flow"

# Short form (if installed as skill)
claude-code-voice "discuss the API design"
```

## Troubleshooting

### "Cannot access files during call"
Server URL not configured. Run `claude-code-voice config server-url <tunnel-url>` after starting server + tunnel.

### "Vapi API error 400"
Usually means setup incomplete. Run `claude-code-voice setup` again.

### Call doesn't connect
Check `claude-code-voice status` - verify phone numbers are set and Vapi number exists.
