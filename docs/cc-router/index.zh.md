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

订阅买多了 Claude Code 却只能用一家？cc-router 把 DeepSeek、Qwen、Kimi、MiMo、MiniMax、智谱 GLM、Anthropic 等厂商的 Token Plan、Coding Plan、API 额度合并成一个虚拟 Plan，任意搭配 opus / sonnet / haiku 三槽位，按顺序或轮询调度，限流和失败自动切换——把每一份额度榨到最后一个 token。

[:fontawesome-brands-github: GitHub 仓库](https://github.com/finch-xu/cc-router){ .md-button }
[:material-download: 下载 Releases](https://github.com/finch-xu/cc-router/releases){ .md-button }

## 特性

- **多厂商聚合** —— 一次配置，覆盖国内主流大模型订阅与按量 API（智谱、DeepSeek、Kimi、MiniMax、阿里百炼、火山、腾讯云、小米 MiMo、OpenRouter、Fireworks、ModelScope、Ollama 等）
- **三槽位虚拟模型** —— 把任意真实模型映射到 Claude Code 的 opus / sonnet / haiku 三个槽位
- **智能调度** —— 顺序或轮询调用多个订阅，遇到限流/失败自动切到下一个
- **本地代理** —— 启动后监听 `127.0.0.1:23456`，零云端依赖，API Key 不出本机
- **Onboarding 引导** —— 首次启动自动抓取模型列表，一键生成 Claude Code 环境变量配置

## 界面预览

<figure align="center" markdown="span">
  ![虚拟模型配置页](../assets/images/cc-router/screenshot-models.png){ width="900" }
  <figcaption>虚拟模型配置页：把多个真实模型挂到 opus / sonnet / haiku 三槽位</figcaption>
</figure>

<figure align="center" markdown="span">
  ![请求日志页](../assets/images/cc-router/screenshot-logs.png){ width="900" }
  <figcaption>请求日志页：实时查看 Claude Code 的请求路由情况</figcaption>
</figure>

## 快速链接

- [快速开始](getting-started.md) —— 下载安装与 Claude Code 接入
- [GitHub](https://github.com/finch-xu/cc-router) —— 源代码与 Releases
