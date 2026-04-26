# cc-router

<figure align="center" markdown="span">
  ![cc-router](../assets/images/cc-router/icon.png){ width="160" }
</figure>

<p align="center">
  <a href="https://github.com/finch-xu/cc-router/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="License: MIT"></a>
  <img src="https://img.shields.io/badge/Tauri-2-FFC131?logo=tauri&logoColor=white" alt="Tauri 2">
  <img src="https://img.shields.io/badge/Rust-1.77+-DEA584?logo=rust&logoColor=white" alt="Rust">
  <img src="https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=black" alt="React">
  <img src="https://img.shields.io/badge/Platform-macOS%20%7C%20Windows%20%7C%20Linux-lightgrey" alt="Platform">
</p>

Bought too many Claude Code subscriptions but stuck using only one? cc-router merges Token Plans, Coding Plans, and pay-as-you-go API quotas from DeepSeek, Qwen, Kimi, MiMo, MiniMax, Zhipu GLM, Anthropic, and more into a single virtual plan. Mix and match providers across the opus / sonnet / haiku slots, schedule them sequentially or round-robin, and let cc-router auto-failover on rate limits and errors — squeezing every quota down to the last token.

[:fontawesome-brands-github: GitHub Repo](https://github.com/finch-xu/cc-router){ .md-button }
[:material-download: Download Releases](https://github.com/finch-xu/cc-router/releases){ .md-button }

## Features

- **Multi-provider aggregation** — One config covers major LLM subscriptions and pay-as-you-go APIs (Zhipu, DeepSeek, Kimi, MiniMax, Alibaba Bailian, Volcengine, Tencent Cloud, Xiaomi MiMo, OpenRouter, Fireworks, ModelScope, Ollama, and more)
- **Three-slot virtual model** — Map any real model to Claude Code's opus / sonnet / haiku slots
- **Smart scheduling** — Call multiple subscriptions sequentially or round-robin, with automatic failover on rate limits and errors
- **Local proxy** — Listens on `127.0.0.1:23456` after launch; zero cloud dependency, API keys never leave your machine
- **Onboarding wizard** — On first launch, automatically fetches model lists and generates Claude Code env config in one click

## Screenshots

<figure align="center" markdown="span">
  ![Virtual model configuration](../assets/images/cc-router/screenshot-models.png){ width="900" }
  <figcaption>Virtual model configuration: bind multiple real models to the opus / sonnet / haiku slots</figcaption>
</figure>

<figure align="center" markdown="span">
  ![Request log](../assets/images/cc-router/screenshot-logs.png){ width="900" }
  <figcaption>Request log: watch Claude Code request routing in real time</figcaption>
</figure>

## Quick Links

- [Getting Started](getting-started.md) — Download, install, and connect to Claude Code
- [GitHub](https://github.com/finch-xu/cc-router) — Source code and releases
