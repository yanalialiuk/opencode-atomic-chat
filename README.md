# opencode-atomic-chat

[OpenCode](https://opencode.ai/) plugin for [Atomic Chat](https://atomic.chat/): auto-detection of the local OpenAI-compatible API (default `http://127.0.0.1:1337/v1`), dynamic model discovery via `GET /v1/models`, and optional chat-time validation with toasts — same idea as [`opencode-lmstudio`](https://www.npmjs.com/package/opencode-lmstudio).

## Install

```bash
npm install opencode-atomic-chat
```

## `opencode.json`

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": ["opencode-atomic-chat@latest"],
  "provider": {
    "atomic-chat": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Atomic Chat (local)",
      "options": {
        "baseURL": "http://127.0.0.1:1337/v1"
      }
    }
  }
}
```

If the `atomic-chat` provider is omitted but Atomic Chat responds on port **1337** (or **1338**), the plugin can create the provider block for you. Model ids must match those returned by `GET /v1/models` (see [OpenCode docs — Atomic Chat](https://opencode.ai/docs/providers/#atomic-chat)).

## Development

Repository: [github.com/yanalialiuk/opencode-atomic-chat](https://github.com/yanalialiuk/opencode-atomic-chat).

```bash
git clone https://github.com/yanalialiuk/opencode-atomic-chat.git
cd opencode-atomic-chat
npm install
npm run build
```

## License

MIT
