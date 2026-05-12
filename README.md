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

### Run OpenCode with this plugin (local smoke test)

1. Install the OpenCode CLI if needed: [Install](https://opencode.ai/docs) (`curl -fsSL https://opencode.ai/install | bash` or `brew install anomalyco/tap/opencode`).
2. Start [Atomic Chat](https://atomic.chat/) so the API is up at `http://127.0.0.1:1337/v1` and load a model.
3. From the **root of this repository** (where `package.json` and `opencode.json` live):

```bash
cd /path/to/opencode-atomic-chat
opencode
```

This repo includes an `opencode.json` that loads the plugin via **`"plugin": ["./"]`** (path plugin: the current directory is the npm package). On startup you should see a log line like `[opencode-atomic-chat] Atomic Chat plugin initialized`.

**Another project:** in that project’s `opencode.json` use an absolute path, for example:

```json
"plugin": ["file:///Users/you/dev/opencode-atomic-chat"]
```

(Relative paths like `./../opencode-atomic-chat` also work if your shell’s current directory when launching OpenCode matches how the path resolves.)

## Publish to npm (public)

Unscoped package `opencode-atomic-chat` is **public by default** on first `npm publish`. No `publishConfig` is required unless you later rename the package to a scoped name (`@your-scope/...`); then add `"publishConfig": { "access": "public" }`.

1. [Create an npm account](https://www.npmjs.com/signup) and enable 2FA (recommended).
2. Log in locally: `npm login` (or `npm login --auth-type=web`).
3. From the repo root, with a clean tree and tests passing:

```bash
npm install
npm publish
```

`prepublishOnly` runs `npm run build` (typecheck + tests) automatically before publish.

4. After the first release, bump version for updates: `npm version patch` (or `minor` / `major`), then `git push --follow-tags` and `npm publish`.

Package contents are controlled by the `"files"` field (`src`, `README.md`, `LICENSE`).

## License

MIT
