# 开发调试

## 环境要求

| 工具 | 版本 |
|------|------|
| Node.js | 24+ |
| Go | 1.22+ |

## 安装依赖

```bash
# Web + Relay（npm workspaces）
npm install

# Agent
cd agent && go mod download
```

## 本地启动

本地开发需要同时运行三个进程，建议使用三个终端窗口：

=== "终端 1：Relay"

    ```bash
    cd packages/relay && npm run dev
    ```

=== "终端 2：Web UI"

    ```bash
    cd packages/web && npm run dev
    ```

    Vite 开发服务器会自动代理 API 请求到 Relay。

=== "终端 3：Agent"

    ```bash
    cd agent && go run . -relay ws://localhost:8080/ws/agent
    ```

启动后打开 `http://localhost:5173`，在 Setup 页面创建管理员账号即可开始调试。

!!! tip "端口说明"

    - `:8080` — Relay 后端（WebSocket + REST API）
    - `:5173` — Vite 前端开发服务器（自动代理到 Relay）

    日常开发访问 `:5173` 即可，享受 HMR 热更新。

## 构建

```bash
make all        # 构建全部组件（Agent + Relay + Web）
make agent      # Go 二进制 → bin/rttys-agent
make relay      # TypeScript 编译 → packages/relay/dist/
make web        # Vite 构建 → packages/relay/public/
```

### Agent 交叉编译

```bash
cd agent

# Linux x86_64
GOOS=linux  GOARCH=amd64 go build -o rttys-agent-linux-amd64 .

# macOS Apple Silicon
GOOS=darwin GOARCH=arm64 go build -o rttys-agent-darwin-arm64 .
```

!!! note "Web 构建输出到 Relay"

    `make web` 的产物输出到 `packages/relay/public/`，这样生产环境下 Relay 直接托管前端静态文件，不需要额外的 Web 服务器。

## 类型检查

```bash
# Relay（TypeScript）
cd packages/relay && npx tsc --noEmit

# Web（TypeScript）
cd packages/web && npx tsc --noEmit

# Agent（Go）
cd agent && go vet ./...
```

## 项目结构

```
remotettys/
├── agent/              # Go — 本地 Agent 二进制
├── packages/
│   ├── relay/          # TypeScript — WebSocket 中继 + REST API
│   └── web/            # React + Vite — 浏览器终端 UI
├── Dockerfile          # 多阶段构建（服务端）
├── docker-compose.yml  # 生产部署
├── Makefile            # 构建所有组件
└── package.json        # npm workspaces
```
