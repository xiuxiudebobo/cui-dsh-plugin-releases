# 随附组件

Cui 面板底部的“随附组件”显示本包提供的插件、技能及可选 MCP 的来源、固定版本和本机状态。技能的启停、编辑、删除、调用统一在“记忆系统 → 技能管理”。

- 配套插件：插件市场 `dshmarket`、记忆系统 `dsh-mnemon`、搜索兜底 `dsh-free-search`。缺失项通过 DSH 官方插件管理服务补装；已有版本和启用设置保留。
- 上游技能：使用 `skills/references.json` 的原始 ID，版本和完整文件哈希固定在 `skills/upstream-pins.json`。验证后复制原始文件到 `~/.dsh/skills/<原名>`，不加 Cui 前缀，不改正文。原有同名技能保留，不纳入 Cui 所有权。
- 自编工作流：原有四个 `cui-*` 工作流保持名称；它们本来就是本项目编写的内容。
- MCP：Illustrator / Zotero 仍按需安装，软件依赖不随技能自动安装。

默认自动接收随包发布的组件；用户可关闭，或点击“同步组件”。DSH 有任务时暂停补装。用户修改过的技能保留；在记忆系统删除的技能不自动装回。备份与安装收据位于 `~/.dsh/cui-group/`。

## 管理员发布

1. 配套插件的审核版本维护在 `scripts/desktop-platform.cjs` 的 `RECOMMENDED_PLUGINS`；搜索兜底维护在 `search-plugins.json`。
2. 上游技能维护原 ID、仓库、commit、许可及文件 SHA-256。新增自编技能添加到 `skills/catalog.json`，设置 `autoInstall: true` 才会作为新增默认组件分发。
3. 通过现有 `npm test`、`npm run release` 签名发布流程推送 Cui 新版本。成员客户端接收该版本后，在空闲时同步新增组件；没有独立的远程任意命令通道。已经存在的第三方插件版本交由 DSH/插件市场更新。

首次安装或更新是否实际完成，以本机“随附组件”状态为准。缺少宿主安装接口、DSH 版本不兼容或网络失败时显示未完成，不视为已安装。
