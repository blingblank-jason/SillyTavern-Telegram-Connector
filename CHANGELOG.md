# Changelog

## v0.2.0-openclaw - 2026-06-11

此版本是 `blingblank-jason/SillyTavern-Telegram-Connector` 增强维护版的首个整理版，基于上游 `justhil/SillyTavern-Telegram-Connector`。

### Added

- 新增 Telegram 内联按钮主菜单与详细帮助入口。
- 新增 `/listchars [页码]` 角色分页列表与 inline 切换按钮。
- 新增 `/listchats [页码]` 当前角色聊天记录分页列表与 inline 切换按钮。
- 新增 `/switchchar` 无参数打开角色切换菜单。
- 新增 `/switchchat` 无参数打开当前角色聊天记录切换菜单。
- 新增切换角色后自动弹出聊天记录选择窗口，并提供 `🆕 新建聊天`。
- 新增模型、预设、Profile、Provider、当前源模型等 Bridge 控制命令。
- 新增 Bridge runtime config reload 与状态回读能力。
- 新增 Telegram 文件上传导入角色卡 / OpenAI 预设 MVP 流程。
- 新增导入 OpenAI 预设后前端内存 registry 与 DOM select 同步刷新。
- 新增 Docker 环境变量与 headless/容器部署相关适配。

### Changed

- 优化长消息分页与内联按钮组合显示。
- 优化角色/聊天切换路径，减少用户手动输入序号后的二次操作。
- README 改为增强维护版说明，明确 fork 关系、主要能力、配置与安全建议。

### Security

- 私有 Provider/Profile 配置应保存在本地私有文件，不进入 Git。
- 建议生产环境启用 `ALLOWED_USER_IDS` 白名单。
- 不要将 Telegram Bot Token、API Key、私有 endpoint 或任何 PAT 提交到仓库。

## Upstream baseline

- 上游仓库：`justhil/SillyTavern-Telegram-Connector`
- 许可证：GPL-3.0
- 本维护版保留原始 Git 历史与许可证。
