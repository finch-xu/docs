# 快速开始

本页介绍如何下载安装 cc-router，并把它接入 Claude Code。

## 前置要求

- 操作系统：macOS、Windows 或 Linux
- 已安装 [Claude Code](https://docs.claude.com/en/docs/claude-code)
- 至少一个支持的大模型厂商账号与 API Key（如智谱 GLM、DeepSeek、Kimi、MiniMax、阿里百炼等，完整列表见 [README](https://github.com/finch-xu/cc-router#支持的编程套餐和api)）

## 下载安装

前往 [Releases 页面](https://github.com/finch-xu/cc-router/releases) 下载对应平台的安装包：

=== "macOS"

    下载 `.dmg` 文件，双击挂载后将 `cc-router` 拖入"应用程序"。

=== "Windows"

    下载 `.exe` 或 `.msi` 文件，双击运行安装向导。

=== "Linux"

    下载 `.AppImage` 或 `.deb` 文件：

    - `.AppImage`：`chmod +x cc-router_*.AppImage && ./cc-router_*.AppImage`
    - `.deb`：`sudo dpkg -i cc-router_*.deb`

## 配置虚拟模型

首次启动 cc-router 会进入 Onboarding 引导：

1. **添加订阅** —— 选择厂商 → 选择接入点（订阅 / 按量 API） → 填入 API Key，cc-router 会自动抓取该订阅可用的模型列表
2. **绑定虚拟模型** —— 把抓到的真实模型分配到 `opus` / `sonnet` / `haiku` 三个虚拟槽位
3. **选择调度模式** —— 同一槽位下挂多个订阅时，可选 **顺序**（前一个用完/失败再切下一个）或 **轮询**（请求间轮转）

如需新增厂商或调整槽位，可在主界面 **模型** 页随时修改。

## 接入 Claude Code

cc-router 启动后会在本机起一个监听 `127.0.0.1:23456` 的代理服务。打开 cc-router 的 **设置** 页，复制完整的 env snippet，粘贴到 `~/.claude/settings.json` 的 `env` 字段：

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "http://127.0.0.1:23456",
    "ANTHROPIC_AUTH_TOKEN": "填写app里给你的真实token",
    "API_TIMEOUT_MS": "3000000",
    "CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC": "1",
    "ANTHROPIC_MODEL": "model-opus",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "model-sonnet",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "model-opus",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "model-haiku"
  }
}
```

`model-opus` `model-sonnet` `model-haiku` 就是你配置到cc的模型名字，这是app提供给你的接口和虚拟模型名字。app会自动把虚拟模型名转成真实模型名。    

如果你的模型支持1M上下文，你可以写`model-opus[1m]`，这是`Claude Code`支持的写法.    

!!! note "端口被占用"
    默认端口 `23456` 若被占用，cc-router 会自动 +1 递增。请始终从"设置"页复制最新的 snippet，确保端口号一致。

保存配置后重启 Claude Code，即可通过 cc-router 路由到你配置的真实模型。

## 下一步

- 在 cc-router 主界面查看 **请求日志**，验证 Claude Code 的请求是否正确路由
- 想新增不在内置列表里的厂商？参考 [README 的"添加新 provider"章节](https://github.com/finch-xu/cc-router#添加新provider)，可在 Claude Code 中执行 `new-provider` skill 自动生成
