# Getting Started

This page covers how to download cc-router and wire it into Claude Code.

## Prerequisites

- Operating system: macOS, Windows, or Linux
- [Claude Code](https://docs.claude.com/en/docs/claude-code) installed
- At least one supported LLM provider account with an API key (e.g. Zhipu GLM, DeepSeek, Kimi, MiniMax, Alibaba Bailian — see the [README](https://github.com/finch-xu/cc-router/blob/main/README.en.md) for the full list)

## Download & Install

Grab the installer for your platform from the [Releases page](https://github.com/finch-xu/cc-router/releases):

=== "macOS"

    Download the `.dmg` file, mount it, then drag `cc-router` into your Applications folder.

=== "Windows"

    Download the `.exe` or `.msi` file and run the installer.

=== "Linux"

    Download the `.AppImage` or `.deb` file:

    - `.AppImage`: `chmod +x cc-router_*.AppImage && ./cc-router_*.AppImage`
    - `.deb`: `sudo dpkg -i cc-router_*.deb`

## Configure Virtual Models

On first launch, cc-router walks you through an onboarding flow:

1. **Add a subscription** — Pick a provider → pick an endpoint (subscription / pay-as-you-go API) → enter your API key. cc-router automatically fetches the available model list.
2. **Bind virtual models** — Assign the fetched real models to the `opus` / `sonnet` / `haiku` virtual slots.
3. **Pick a scheduling mode** — When multiple subscriptions sit on the same slot, choose **Sequential** (move to the next one only when the current one is exhausted or fails) or **Round-robin** (rotate between requests).

You can revisit and tweak providers or slot bindings any time from the **Models** page in the main UI.

## Connect to Claude Code

After launch, cc-router runs a local proxy listening on `127.0.0.1:23456`. Open cc-router's **Settings** page, copy the full env snippet, and paste it into the `env` field of `~/.claude/settings.json`:

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "http://127.0.0.1:23456",
    "ANTHROPIC_AUTH_TOKEN": "paste the real token shown in the app",
    "API_TIMEOUT_MS": "3000000",
    "CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC": "1",
    "ANTHROPIC_MODEL": "model-opus",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "model-sonnet",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "model-opus",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "model-haiku"
  }
}
```

`model-opus`, `model-sonnet`, and `model-haiku` are the virtual model names cc-router exposes to Claude Code — the app translates them to the real model names you configured behind the scenes.

If your model supports a 1M context window, you can write `model-opus[1m]` — this is the syntax Claude Code understands.

!!! note "Port already in use"
    If the default port `23456` is taken, cc-router auto-increments to the next free port. Always copy the latest snippet from the **Settings** page so the port stays in sync.

Restart Claude Code after saving, and your requests will flow through cc-router to the real models you configured.

## Next Steps

- Open the **Request Log** in cc-router's main UI to verify Claude Code's requests are routed correctly
- Need a provider that isn't built in? See the ["Adding a new provider" section in the README](https://github.com/finch-xu/cc-router/blob/main/README.en.md). If you use Claude Code, run the bundled `new-provider` skill to generate the provider config automatically.
