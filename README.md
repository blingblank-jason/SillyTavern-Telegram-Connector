# SillyTavern Telegram Connector Enhanced

通过 Telegram 与 SillyTavern AI 角色聊天，并在 Telegram 内完成角色、聊天、模型、预设、Provider/Profile 与导入流程控制的 SillyTavern 扩展。

> 维护说明：本仓库是 `justhil/SillyTavern-Telegram-Connector` 的增强维护版，保留原项目 GPL-3.0 许可证与 Git 历史。上游 PR 仍会继续提交；在上游合并前，本 fork 作为生产可用版本维护。

[![License](https://img.shields.io/github/license/blingblank-jason/SillyTavern-Telegram-Connector)](LICENSE)

## 新增能力概览

在原有 Telegram 聊天桥接基础上，本增强版重点加入：

- Telegram 内联按钮菜单与分页控制。
- 角色列表 `/listchars` 与聊天列表 `/listchats` 分页展示。
- `/switchchar`、`/switchchat` 无参数时直接弹出切换菜单。
- 切换角色后自动弹出该角色的聊天记录选择窗口，并提供 `🆕 新建聊天`。
- 模型、预设、Profile、Provider 与当前源模型切换命令。
- OpenAI/Chat Completion 预设导入与导入后前端列表刷新。
- Telegram 文件上传导入角色卡 / 预设的 MVP 流程。
- Bridge 运行状态、配置重载与连接心跳检测。
- Docker 部署与环境变量配置增强。

## 快速开始

### 1. 安装扩展

在 SillyTavern 中：

```text
Extensions → Install Extension
```

输入本维护版仓库地址：

```text
https://github.com/blingblank-jason/SillyTavern-Telegram-Connector
```

如果你希望使用固定版本，可 checkout release tag，例如：

```text
v0.2.0-enhanced
```

### 2. 部署 Bridge Server

推荐使用 Docker Compose：

```bash
cd server
cp config.example.js config.js
# 或使用 .env / 环境变量配置 TELEGRAM_BOT_TOKEN

docker compose up -d --build
```

也可以手动运行：

```bash
cd server
npm install
cp config.example.js config.js
# 编辑 config.js，填入 Bot Token
node server.js
```

### 3. 连接 SillyTavern 扩展

1. 打开 SillyTavern → Extensions → Telegram Connector。
2. 填入 Bridge URL，例如：
   - 本机：`ws://127.0.0.1:2333`
   - 内网容器：`ws://st-telegram-bridge:2333`
   - 公网反代：`wss://your-domain.example/tg-bridge`
3. 点击连接。

## 常用命令

| 命令 | 说明 |
|------|------|
| `/help` | 显示内联菜单 |
| `/helptext` | 显示详细命令帮助 |
| `/new` | 新建聊天 |
| `/listchars [页码]` | 角色列表（分页 + 按钮） |
| `/switchchar` | 打开角色切换按钮列表 |
| `/switchchar_数字` | 按序号切换角色 |
| `/switchchar <角色名>` | 按名称切换角色 |
| `/listchats [页码]` | 当前角色聊天记录列表（分页 + 按钮） |
| `/switchchat` | 打开聊天记录切换按钮列表 |
| `/switchchat_数字` | 按序号切换聊天记录 |
| `/switchchat <聊天名>` | 按名称加载聊天记录 |
| `/models` | 当前可用模型列表 |
| `/model <序号/名称/别名>` | 切换模型 |
| `/presets` | 预设列表 |
| `/preset <序号/名称>` | 切换预设 |
| `/profiles` | Bridge Profile 列表 |
| `/profile <序号/ID>` | 切换 Bridge Profile |
| `/providers` | Provider/Profile 列表 |
| `/provider <序号/ID>` | 切换 Provider/Profile |
| `/provider-models [查询/页码]` | 当前源模型列表 |
| `/provider-model <序号/名称>` | 切换当前源模型 |
| `/upload` | 上传导入角色卡 / 预设 |
| `/bridge_status` | Bridge 状态 |
| `/bridge-reload` | 重载 Bridge 配置 |
| `/ping` | 连接状态 |

## 配置

### Bridge Server 环境变量

| 变量 | 说明 | 默认值 |
|------|------|--------|
| `TELEGRAM_BOT_TOKEN` | Telegram Bot Token | 必填 |
| `WSS_PORT` | WebSocket 端口 | `2333` |
| `ALLOWED_USER_IDS` | Telegram 用户白名单，逗号分隔 | 空，允许所有 |
| `MESSAGE_PARSE_MODE` | 消息格式：`HTML` / `MarkdownV2` / `plain` | `HTML` |
| `BRIDGE_TELEGRAM_DISABLED` | 禁用 Telegram Bot，仅测试 Bridge 逻辑 | `0` |

### Bridge Profiles

Bridge Server 支持通过 JSON 配置模型别名、预设、Provider/Profile 与私有 custom endpoint。建议将公共配置与私有密钥分开：

- 公共配置：`server/bridge-profiles.json`
- 私有配置：`server/bridge-custom-profiles.private.json`

私有配置不要提交到 Git 仓库。

## 上传导入

`/upload` 支持从 Telegram 发送文件并导入：

- 角色卡：PNG / JSON。
- OpenAI / Chat Completion 预设：JSON。

建议以 Telegram “文件 / Document”形式发送，避免图片被压缩。

## 安全建议

- 不要公开 Bot Token、API Key、私有 Provider URL 或私有 Profile 配置。
- 生产环境建议配置 `ALLOWED_USER_IDS`。
- 如果 Bridge 暴露到公网，请使用 WSS/HTTPS 反代并限制访问。
- 私有配置文件应设置较严格权限，例如 `600`。

## 版本

当前维护版主要版本：`v0.2.0-enhanced`。

详细变更见 [CHANGELOG.md](CHANGELOG.md)。

## 许可证

GPL-3.0。此维护版继承原项目许可证，修改版本同样以 GPL-3.0 发布。
