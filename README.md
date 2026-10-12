# Cui Group for DeepSeek Harness

公开安装包与签名更新源。源码仓库私有；模型、文献与私有资料仍需课题组成员登录。

## 安装

1. 下载并安装官方 DeepSeek Harness Desktop **0.2.0-rc.2**：
   - [Windows x64 官方安装包](https://download.deepseek.com/dsh-desk/bin/win-x64/deepseek-harness-0.2.0-rc.2-win-x64.exe)：运行 EXE 安装。
   - [macOS Apple 芯片官方安装包](https://download.deepseek.com/dsh-desk/bin/mac-arm64/deepseek-harness-0.2.0-rc.2-mac-arm64.zip)：解压，将 DeepSeek Harness.app 放入“应用程序”。

   已安装此版本的成员可以直接继续下一步。
2. 在 DSH 左侧点击 **插件 → 右上角添加插件**，粘贴下面地址并点击安装：

   ```text
   https://github.com/xiuxiudebobo/cui-dsh-plugin-releases/releases/download/v0.14.0/cui-dsh-plugin-0.14.0.tgz
   ```

3. 安装完成后点 **立即启用**；也可正常退出并重新打开 DSH。在左侧打开 **Cui Group**，连接课题组账号，选择模型并应用。

这是公开安装包链接，不是私有源码仓库或本仓库首页。不需要 GitHub 账号、下载解压或另装 Node.js。macOS 官方添加界面安装/启用已实测，Windows 官方 CLI 链接安装已实测；ZIP 安装器仍保留为备选：[Windows](https://github.com/xiuxiudebobo/cui-dsh-plugin-releases/releases/latest/download/Cui-Group-Windows-installer.zip) / [macOS](https://github.com/xiuxiudebobo/cui-dsh-plugin-releases/releases/latest/download/Cui-Group-macOS-installer.zip)。

Windows 若报 `ERR_PNPM_UNEXPECTED_STORE`，说明原 Desktop 依赖链接自 pnpm v10。请用新版 Windows 安装器，按提示从菜单或托盘完全退出 DSH 后继续；它会备份并使用官方 pnpm v11 重建原依赖，再安装插件。失败会恢复旧依赖和配置，并显示具体报错。不会修改全局 pnpm 设置。

## 使用与更新

- 默认用量为 7 天＋额度。科研资源按家族直接分层展示，选择“多选下载”后才显示选择圈；支持自定义保存目录。
- 四个科研工作流首次默认安装；技能勾选即保存，可复制 `/技能名` 在会话中补充数据和任务。热分析和动力学已接入确定性解析/拟合工具，只需要 Python 3。
- Materials Project 自动获取成员授权的课题组 Key；PubChem、OPTIMADE、AFLOW 无需手填 Key。Catalysis-Hub 需要其个人 Key。
- 自动检查、验签并下载发行包。macOS 在后台且没有活动会话/任务时冷更新；Windows 等 DSH 正常退出后安装，下次打开生效。直接关闭 Windows 窗口只会进入后台。
- 飞牛资源在面板可见时每 30 秒同步、回到窗口立即同步，无需更新插件；在线数据库查询直接读取上游。新增查询适配器仍需插件更新。代码和技能随插件发行更新，个人 Key、已有资源和修改过的技能保留。

验证范围：macOS arm64 原生界面及工具；Windows x64 独立配置安装、环境检测、技能同步、校验下载、签名更新下载。Windows 等退出安装的完整周期仍待验收。MACE 重环境安装目前只验证 macOS arm64；Origin、Illustrator 执行桥和远端作业提交仍待接入。下载权重不代表已经可以计算。

模型与数据只展示飞牛实际可用文件，没有下载项的公开数据源入口不再列出。OC25 相关模型权重及配套资料位于 eSEN 分组。技能按插件固定版本更新，上游变更经验证后发布；六个目录项中 Illustrator preflight 尚缺 MCP，EditAPlot 尚待运行桥验收。

已有权重分散存放时，使用“添加已有目录”登记多个位置。匹配大小和 SHA256 的文件更新为已校验，保持原位置，不重复下载；清单外的实际权重文件另列本机模型，发现文件不等于已验证来源或运行环境。MACE-MP-0 small 支持固定校验识别，示例 64 atoms 是插件执行限制。计算节点授权、临时许可与队列尚未部署。

原先的 latest 压缩包 URL 会随版本变动而与 pnpm 的锁定校验冲突，原生安装请使用上面的版本固定地址。插件自动更新继续验证签名及固定版本的下载地址，不会跳过校验。
