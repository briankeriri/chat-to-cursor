# Quick Setup Guide

For the [briankeriri/chat-to-cursor](https://github.com/briankeriri/chat-to-cursor) fork of [TalkToCursor](https://github.com/MindSyncTech/talk-to-cursor). Use this after cloning and building. Full install: [INSTALL.md](INSTALL.md) · [README.md](README.md).

## 1. Prerequisites

- Node.js 18+
- **ffmpeg** with **`ffplay`** on your PATH (`ffplay -version`)
  - Linux: install `ffmpeg` from your package manager
  - macOS: `brew install ffmpeg`
  - Windows: WinGet / Chocolatey / Scoop / manual `ffplay.exe`

## 2. Get your ElevenLabs API key

1. Go to https://try.elevenlabs.io/talktocursor
2. Sign up or log in (free tier available)
3. Create an API key and copy it

## 3. Configure via settings UI (recommended)

```bash
npm run settings
```

Open http://localhost:3847, paste the API key, test, and save. Optionally pick a voice and presets.

Alternatively, put `ELEVENLABS_API_KEY` in the `env` block of your `~/.cursor/mcp.json` entry (see [INSTALL.md](INSTALL.md)).

## 4. Register the MCP server

Ensure `~/.cursor/mcp.json` points at this project's `build/index.js` (absolute path). Example:

```json
{
  "mcpServers": {
    "tts": {
      "command": "node",
      "args": ["/ABSOLUTE/PATH/TO/chat-to-cursor/build/index.js"]
    }
  }
}
```

## 5. Restart Cursor / Agent

Fully quit and reopen Cursor. If you use **Cursor Agent** (CLI), restart that session so MCP reloads.

## 6. Test

1. Open a chat and confirm the `speak` tool is available
2. Ask: **"Say hello using the speak tool"**
3. You should hear audio on your default output device

## Troubleshooting (audio)

- Tool reports success but no sound → confirm `ffplay -version`, output device, and volume
- Cursor Agent stripped env → this server restores Linux `XDG_RUNTIME_DIR` (PipeWire/Pulse; Wayland and X11) and common ffmpeg PATH entries on macOS/Windows. Rebuild (`npm run build`) and restart Agent after updates
- Linux: stay in a normal graphical user session; avoid routing into a virtual sink with no output (e.g. misconfigured Easy Effects)

## Next steps

- Voice rule: `~/.cursor/rules/voice-feedback.mdc` (see INSTALL.md)
- Hands-free dictation (macOS): Auto-Submit + optional Wispr Flow (see INSTALL.md)
- Voices and usage: https://try.elevenlabs.io/talktocursor
