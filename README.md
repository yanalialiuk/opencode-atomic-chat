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

```bash
git clone https://github.com/<you>/opencode-atomic-chat.git
cd opencode-atomic-chat
npm install
npm run build
```

## Publish this repo to GitHub

1. On GitHub: **New repository** → name `opencode-atomic-chat` → create **without** README (this tree already has one).
2. In the project directory:

```bash
git remote add origin https://github.com/<you>/opencode-atomic-chat.git
git push -u origin main
```

3. Replace `YOUR_GITHUB_USERNAME` in `package.json` (`repository`, `bugs`, `homepage`) with your GitHub username or org.

If you use [GitHub CLI](https://cli.github.com/): `gh repo create opencode-atomic-chat --public --source=. --remote=origin --push`.

## License

MIT
