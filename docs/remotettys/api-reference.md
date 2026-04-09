# API Reference

All endpoints require authentication (session cookie). State-changing endpoints also require the `X-CSRF-Token` header.

!!! info "Authentication"

    After a successful login, the server issues a JWT token via an `httpOnly` cookie. Subsequent requests carry the cookie automatically — no need to set an `Authorization` header manually.

---

## Setup

Used during first-time deployment. Automatically disabled after the admin account is created.

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/api/setup/status` | Check if setup is complete |
| `POST` | `/api/setup/init` | Create admin account |

??? example "POST /api/setup/init"

    **Request body:**

    ```json
    {
      "username": "admin",
      "password": "your-strong-password"
    }
    ```

---

## Auth

| Method | Path | Description |
|--------|------|-------------|
| `POST` | `/api/auth/login` | Login |
| `GET` | `/api/auth/me` | Get current user info |
| `POST` | `/api/auth/logout` | Logout |

??? example "POST /api/auth/login"

    **Request body:**

    ```json
    {
      "username": "admin",
      "password": "your-password"
    }
    ```

---

## Users

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/api/users` | List all users |
| `POST` | `/api/users` | Create a user |
| `DELETE` | `/api/users/:username` | Delete a user |
| `PUT` | `/api/users/:username/password` | Change user password |

??? example "POST /api/users"

    **Request body:**

    ```json
    {
      "username": "newuser",
      "password": "user-password"
    }
    ```

??? example "PUT /api/users/:username/password"

    **Request body:**

    ```json
    {
      "password": "new-password"
    }
    ```

---

## User Preferences

| Method | Path | Description |
|--------|------|-------------|
| `PUT` | `/api/preferences` | Update user preferences |

??? example "PUT /api/preferences"

    **Request body:**

    ```json
    {
      "uiTheme": "dark",
      "terminalTheme": "ghostty"
    }
    ```

---

## Agent Tokens

Used to authorize local machine agents to connect to the relay server.

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/api/tokens` | List all tokens |
| `POST` | `/api/tokens` | Create a token |
| `PUT` | `/api/tokens/:id/enabled` | Enable/disable a token |
| `DELETE` | `/api/tokens/:token` | Delete a token |

??? example "POST /api/tokens"

    **Request body:**

    ```json
    {
      "label": "Home Mac",
      "notes": "Living room Mac Mini"
    }
    ```

??? example "PUT /api/tokens/:id/enabled"

    **Request body:**

    ```json
    {
      "enabled": false
    }
    ```

---

## Agents

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/api/agents` | List connected agents |
| `DELETE` | `/api/agents/:id` | Delete an agent |
| `DELETE` | `/api/agents/:id/fingerprint` | Reset machine fingerprint |

!!! tip "When to Reset Fingerprint"

    When the agent's host machine has a hardware change or OS reinstall, the machine fingerprint changes, causing connection rejection. Use this endpoint to reset the fingerprint and allow the agent to re-bind.

---

## Server Key

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/api/server-key` | Get server Ed25519 public key |

---

## Audit Log

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/api/audit?limit=100` | Get audit log entries |

**Query parameters:**

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `limit` | `number` | `100` | Maximum number of log entries to return |
