# 接口文档

所有接口均需通过身份认证（Session Cookie）。涉及状态变更的接口还需要携带 `X-CSRF-Token` 请求头。

!!! info "认证方式"

    登录成功后，服务端通过 `httpOnly` Cookie 下发 JWT Token。后续请求自动携带 Cookie，无需手动设置 `Authorization` 头。

---

## 初始化

首次部署时使用，创建管理员账号后自动禁用。

| 方法 | 路径 | 说明 |
|------|------|------|
| `GET` | `/api/setup/status` | 查询是否已初始化 |
| `POST` | `/api/setup/init` | 创建管理员账号 |

??? example "POST /api/setup/init"

    **请求体：**

    ```json
    {
      "username": "admin",
      "password": "your-strong-password"
    }
    ```

---

## 认证

| 方法 | 路径 | 说明 |
|------|------|------|
| `POST` | `/api/auth/login` | 登录 |
| `GET` | `/api/auth/me` | 获取当前用户信息 |
| `POST` | `/api/auth/logout` | 登出 |

??? example "POST /api/auth/login"

    **请求体：**

    ```json
    {
      "username": "admin",
      "password": "your-password"
    }
    ```

---

## 用户管理

| 方法 | 路径 | 说明 |
|------|------|------|
| `GET` | `/api/users` | 获取用户列表 |
| `POST` | `/api/users` | 创建用户 |
| `DELETE` | `/api/users/:username` | 删除用户 |
| `PUT` | `/api/users/:username/password` | 修改用户密码 |

??? example "POST /api/users"

    **请求体：**

    ```json
    {
      "username": "newuser",
      "password": "user-password"
    }
    ```

??? example "PUT /api/users/:username/password"

    **请求体：**

    ```json
    {
      "password": "new-password"
    }
    ```

---

## 用户偏好

| 方法 | 路径 | 说明 |
|------|------|------|
| `PUT` | `/api/preferences` | 更新用户偏好设置 |

??? example "PUT /api/preferences"

    **请求体：**

    ```json
    {
      "uiTheme": "dark",
      "terminalTheme": "ghostty"
    }
    ```

---

## Agent Token

用于授权本地机器的 Agent 连接到 Relay 服务器。

| 方法 | 路径 | 说明 |
|------|------|------|
| `GET` | `/api/tokens` | 获取所有 Token |
| `POST` | `/api/tokens` | 创建 Token |
| `PUT` | `/api/tokens/:id/enabled` | 启用/禁用 Token |
| `DELETE` | `/api/tokens/:token` | 删除 Token |

??? example "POST /api/tokens"

    **请求体：**

    ```json
    {
      "label": "Home Mac",
      "notes": "客厅 Mac Mini"
    }
    ```

??? example "PUT /api/tokens/:id/enabled"

    **请求体：**

    ```json
    {
      "enabled": false
    }
    ```

---

## Agent 管理

| 方法 | 路径 | 说明 |
|------|------|------|
| `GET` | `/api/agents` | 获取已连接的 Agent 列表 |
| `DELETE` | `/api/agents/:id` | 删除 Agent |
| `DELETE` | `/api/agents/:id/fingerprint` | 重置机器指纹 |

!!! tip "何时需要重置指纹"

    当 Agent 所在机器更换硬件或重装系统后，机器指纹会发生变化，导致连接被拒绝。此时需要通过此接口重置指纹，允许 Agent 重新绑定。

---

## 服务器密钥

| 方法 | 路径 | 说明 |
|------|------|------|
| `GET` | `/api/server-key` | 获取服务器 Ed25519 公钥 |

---

## 审计日志

| 方法 | 路径 | 说明 |
|------|------|------|
| `GET` | `/api/audit?limit=100` | 获取审计日志 |

**查询参数：**

| 参数 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `limit` | `number` | `100` | 返回的日志条数上限 |
