# Cui Group for DeepSeek Harness

公开安装包与签名更新源。源码仓库私有；模型、文献与私有资料仍需课题组成员登录。

## 安装

1. 下载并安装官方 DeepSeek Harness Desktop **0.2.0-rc.2**：
   - [Windows x64 官方安装包](https://download.deepseek.com/dsh-desk/bin/win-x64/deepseek-harness-0.2.0-rc.2-win-x64.exe)：运行 EXE 安装。
   - [macOS Apple 芯片官方安装包](https://download.deepseek.com/dsh-desk/bin/mac-arm64/deepseek-harness-0.2.0-rc.2-mac-arm64.zip)：解压，将 DeepSeek Harness.app 放入“应用程序”。

   已安装此版本的成员可以直接继续下一步。

2. **推荐安装：一行命令。** 把下面整条命令粘进终端运行——它会自动下载最新签名版、校验 SHA256、从本地文件安装（避开 pnpm 远程链接的坑），完成后自动重开 DSH。只用 DSH 自带运行时，不需要 GitHub 账号、管理员权限或另装 Node.js，也不改官方程序。

   macOS（终端；会自动退出并重装 DSH）：

   ```bash
   DSH="/Applications/DeepSeek Harness.app/Contents/MacOS/DeepSeek Harness"; T=$(mktemp -d) && cd "$T" && curl -fL -o p.tgz "https://github.com/xiuxiudebobo/cui-dsh-plugin-releases/releases/latest/download/cui-dsh-plugin.tgz" && curl -fL -o latest.json "https://github.com/xiuxiudebobo/cui-dsh-plugin-releases/releases/latest/download/latest.json" && H=$(ELECTRON_RUN_AS_NODE=1 "$DSH" -e 'console.log(JSON.parse(JSON.parse(require("fs").readFileSync("latest.json","utf8")).payload).asset.sha256)') && tar xzf p.tgz && ELECTRON_RUN_AS_NODE=1 "$DSH" package/scripts/manual-install.cjs p.tgz "$H"
   ```

   Windows（PowerShell；**先从右下角托盘图标 → 退出，完全关闭 DSH 后再运行**）：

   ```powershell
   $exe="$env:LOCALAPPDATA\Programs\DeepSeek Harness\DeepSeek Harness.exe"; $t=Join-Path $env:TEMP ('cui'+[guid]::NewGuid()); New-Item -ItemType Directory $t|Out-Null; Set-Location $t; Invoke-WebRequest -UseBasicParsing "https://github.com/xiuxiudebobo/cui-dsh-plugin-releases/releases/latest/download/cui-dsh-plugin.tgz" -OutFile p.tgz; Invoke-WebRequest -UseBasicParsing "https://github.com/xiuxiudebobo/cui-dsh-plugin-releases/releases/latest/download/latest.json" -OutFile latest.json; $env:ELECTRON_RUN_AS_NODE='1'; $h=& $exe -e "console.log(JSON.parse(JSON.parse(require('fs').readFileSync('latest.json','utf8')).payload).asset.sha256)"; tar -xzf p.tgz; & $exe package\scripts\manual-install.cjs p.tgz $h; Remove-Item Env:ELECTRON_RUN_AS_NODE
   ```

   运行前确认终端里没有设置 `DSH_HOME`，否则会装到别的目录。Windows 命令里的 `$exe` 按 DSH 默认安装位置推测（尚未在 Windows 实机验证）；装在别处请先改成实际的 `DeepSeek Harness.exe` 路径。

   **不要在“插件 → 添加插件”里直接粘贴 https 安装包链接。** DSH 当前的 pnpm 对远程链接可能写出缺少 integrity 的锁定记录（`ERR_PNPM_MISSING_TARBALL_INTEGRITY`），之后插件就无法再更新。上面的一行命令先把 tgz 下到本地、再从本地文件安装，正好避开这个坑。

3. 安装完成后会自动重开 DSH（若没重开就手动打开）。在左侧打开 **Cui Group**，连接课题组账号，选择模型并应用。

### 备选：安装器 ZIP

仍提供 [Windows 安装器 ZIP](https://github.com/xiuxiudebobo/cui-dsh-plugin-releases/releases/latest/download/Cui-Group-Windows-installer.zip) / [macOS 安装器 ZIP](https://github.com/xiuxiudebobo/cui-dsh-plugin-releases/releases/latest/download/Cui-Group-macOS-installer.zip)。**但 macOS 上未签名的 `Install-Cui-Group.command` 双击会被 Gatekeeper 拦（提示“无法验证开发者”而打不开）**，需右键 → 打开、或在“系统设置 → 隐私与安全性”里放行；这比直接粘一行命令麻烦，故命令方式为首选。Windows 双击 `Install-Cui-Group.cmd`，按提示从菜单或托盘完全退出 DSH 再继续。

Windows 若报 `ERR_PNPM_UNEXPECTED_STORE`（原 Desktop 依赖链接自 pnpm v10），运行上面“推荐安装”的一行命令即可（1.0.3 起已内置该修复），并先从菜单或托盘完全退出 DSH；它会备份并用官方 pnpm v11 重建原依赖再安装，失败恢复旧依赖和配置，不改全局 pnpm 设置。

## 更新失败 / 卡在旧版本

若自动更新一直失败，或报 `ERR_PNPM_MISSING_TARBALL_INTEGRITY`（多见于从 0.14 升级、或曾粘贴过 https 安装链接的机器），运行上面“推荐安装”里同一条命令即可：它会下载最新签名版、从本地文件安装，并自动清理旧的远程链接锁定记录（先备份到 `~/.dsh/cui-group/backups`）。装好后，后续版本可正常自动更新。

## 使用与更新

- 默认用量为 7 天＋额度。科研资源按家族直接分层展示，选择“多选下载”后才显示选择圈；支持自定义保存目录。
- 四个科研工作流首次默认安装；技能勾选即保存，可复制 `/技能名` 在会话中补充数据和任务。热分析和动力学已接入确定性解析/拟合工具，只需要 Python 3。
- Materials Project 自动获取成员授权的课题组 Key；PubChem、OPTIMADE、AFLOW 无需手填 Key。Catalysis-Hub 需要其个人 Key。
- 自动检查、验签并下载发行包。macOS 在后台且没有活动会话/任务时自动冷更新；Windows 下载完成后按钮显示“立即重启并更新”，点它并确认即自动关闭 DSH、装好再重开（也可从菜单或托盘完全退出手动完成）。直接关闭 Windows 窗口只会进入后台、不触发安装。
- 飞牛资源在面板可见时每 30 秒同步、回到窗口立即同步，无需更新插件；在线数据库查询直接读取上游。新增查询适配器仍需插件更新。代码和技能随插件发行更新，个人 Key、已有资源和修改过的技能保留。

验证范围：macOS arm64 原生界面及工具；Windows x64 独立配置安装、环境检测、技能同步、校验下载、签名更新下载。Windows“立即重启并更新”的强制退出与一行安装命令尚未在 Windows 实机验收。MACE 重环境安装目前只验证 macOS arm64；Origin、Illustrator 执行桥和远端作业提交仍待接入。下载权重不代表已经可以计算。

模型与数据只展示飞牛实际可用文件，没有下载项的公开数据源入口不再列出。OC25 相关模型权重及配套资料位于 eSEN 分组。技能按插件固定版本更新，上游变更经验证后发布；六个目录项中 Illustrator preflight 尚缺 MCP，EditAPlot 尚待运行桥验收。

已有权重分散存放时，使用“添加已有目录”登记多个位置。匹配大小和 SHA256 的文件更新为已校验，保持原位置，不重复下载；清单外的实际权重文件另列本机模型，发现文件不等于已验证来源或运行环境。MACE-MP-0 small 支持固定校验识别，示例 64 atoms 是插件执行限制。计算节点授权、临时许可与队列尚未部署。

插件自动更新会验证签名和固定版本的安装包，并从本地已校验文件安装，不会跳过校验。

## 可选伴随扩展（独立安装）

- [dsh-batch-tool-calls](https://github.com/liancha22/dsh-batch-tool-calls)，本次核查版本 **1.1.2**：推荐用于引导模型合理合并工具调用；不改变宿主并发引擎，不保证每次减少 token。
- [dsh-ops](https://github.com/T-Auto/dsh-ops)，本次核查的 npm 发布版本 **0.3.0**：仅 **Windows x64** 选装，Mac 暂不安装此版本。提供文件与终端工具；本次未作 Windows 实机工具验收。

两者由各自上游维护，按上游说明在 DSH 中单独安装、启用或卸载。Cui Group 1.1.3 不自动安装它们，也不改动成员已有工具设置。GitHub 源码进度不等于 npm 已发布平台支持；升级时重新核对兼容性。
