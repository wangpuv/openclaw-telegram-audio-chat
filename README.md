# openclaw-audio-chat

OpenClaw plugin that auto-sends Telegram voice bubble replies from assistant text using local TTS.

## What it does

- Adds `/audio_chat on|off|status|max <n>`
- Stores per-chat enable/disable state in the OpenClaw state directory
- Cleans markdown before TTS
- Skips long messages with a tip instead of generating voice
- Debounces sends to reduce duplicate voice bubbles

## Install

After publication, install with:

```bash
openclaw plugins install openclaw-audio-chat
```

OpenClaw checks ClawHub first and falls back to npm automatically.

## Config

Use `extensions.audioChat` (or `audioChat`) in gateway config:

```json
{
  "extensions": {
    "audioChat": {
      "enabledByDefault": false,
      "channels": ["telegram"],
      "defaultMaxChars": 150,
      "tooLongTip": "Message too long, skipped voice reply",
      "voice": "zh-CN-YunxiaNeural",
      "access": {
        "directOnly": true,
        "allowUserIds": []
      }
    }
  }
}
```

## Dependencies

This plugin requires:

- `ffmpeg`
- `edge-tts` available via Python (`python3 -m edge_tts`) or another dedicated Python environment

## Privacy and safety

- No hardcoded personal user IDs or chat IDs
- Voice synthesis is local (`edge-tts` + `ffmpeg`)
- The plugin only sends voice notes to chats where it is enabled
- Recommended default: keep `enabledByDefault: false`
- Recommended default: keep `access.directOnly: true`

## Notes

Currently focused on Telegram voice-note delivery (`asVoice=true`).
