# Development

## Prerequisites

| Tool | Version |
|------|---------|
| Node.js | 24+ |
| Go | 1.22+ |

## Install Dependencies

```bash
# Web + Relay (npm workspaces)
npm install

# Agent
cd agent && go mod download
```

## Run Locally

Local development requires three processes running simultaneously. Use three terminal windows:

=== "Terminal 1: Relay"

    ```bash
    cd packages/relay && npm run dev
    ```

=== "Terminal 2: Web UI"

    ```bash
    cd packages/web && npm run dev
    ```

    The Vite dev server automatically proxies API requests to the Relay.

=== "Terminal 3: Agent"

    ```bash
    cd agent && go run . -relay ws://localhost:8080/ws/agent
    ```

Open `http://localhost:5173` and create your admin account on the Setup page to start debugging.

!!! tip "Port Reference"

    - `:8080` — Relay backend (WebSocket + REST API)
    - `:5173` — Vite frontend dev server (proxies to Relay)

    For everyday development, just visit `:5173` to enjoy HMR hot reload.

## Build

```bash
make all        # Build all components (Agent + Relay + Web)
make agent      # Go binary → bin/rttys-agent
make relay      # TypeScript compile → packages/relay/dist/
make web        # Vite build → packages/relay/public/
```

### Cross-compile Agent

```bash
cd agent

# Linux x86_64
GOOS=linux  GOARCH=amd64 go build -o rttys-agent-linux-amd64 .

# macOS Apple Silicon
GOOS=darwin GOARCH=arm64 go build -o rttys-agent-darwin-arm64 .
```

!!! note "Web Build Outputs to Relay"

    `make web` outputs artifacts to `packages/relay/public/`, so in production the Relay serves the frontend static files directly — no additional web server needed.

## Type Checking

```bash
# Relay (TypeScript)
cd packages/relay && npx tsc --noEmit

# Web (TypeScript)
cd packages/web && npx tsc --noEmit

# Agent (Go)
cd agent && go vet ./...
```

## Project Structure

```
remotettys/
├── agent/              # Go — local agent binary
├── packages/
│   ├── relay/          # TypeScript — WebSocket relay + REST API
│   └── web/            # React + Vite — browser terminal UI
├── Dockerfile          # Multi-stage build for server
├── docker-compose.yml  # Production deployment
├── Makefile            # Build all components
└── package.json        # npm workspaces
```
