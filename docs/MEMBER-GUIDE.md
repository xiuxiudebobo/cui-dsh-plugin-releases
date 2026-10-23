# Cui Group 使用

官方 Desktop 0.2.0-rc.2 下载：[Windows x64](https://download.deepseek.com/dsh-desk/bin/win-x64/deepseek-harness-0.2.0-rc.2-win-x64.exe) / [macOS Apple 芯片](https://download.deepseek.com/dsh-desk/bin/mac-arm64/deepseek-harness-0.2.0-rc.2-mac-arm64.zip)。

需要官方 DeepSeek Harness Desktop。适配官方 Desktop 0.2.0-rc.2：macOS arm64；Windows x64 已验证独立配置安装、环境检测、技能同步、资源校验下载和更新验签。Windows 已完成 0.12.6 → 0.13.0 的真实退出、安装和重新打开验收。

1. **推荐安装：一行命令**（自动下载最新签名版 → 校验 SHA256 → 从本地文件安装 → 重开 DSH；只用 DSH 自带运行时，不需要另装 Node.js、管理员权限，也不改官方程序）。先装好官方 DSH，再把整条命令粘进终端：

   macOS（终端；会退出 DSH、安装插件并重新打开）：

   ```bash
   DSH="/Applications/DeepSeek Harness.app/Contents/MacOS/DeepSeek Harness"; T=$(mktemp -d) && cd "$T" && curl -fL -o p.tgz "https://github.com/xiuxiudebobo/cui-dsh-plugin-releases/releases/latest/download/cui-dsh-plugin.tgz" && curl -fL -o latest.json "https://github.com/xiuxiudebobo/cui-dsh-plugin-releases/releases/latest/download/latest.json" && H=$(ELECTRON_RUN_AS_NODE=1 "$DSH" -e 'console.log(JSON.parse(JSON.parse(require("fs").readFileSync("latest.json","utf8")).payload).asset.sha256)') && tar xzf p.tgz && ELECTRON_RUN_AS_NODE=1 "$DSH" package/scripts/manual-install.cjs p.tgz "$H"
   ```

   Windows（PowerShell；**先从右下角托盘图标 → 退出，完全关闭 DSH 后再运行**；`$exe` 按默认安装位置推测，装在别处请改成实际路径，尚未在 Windows 实机验证）：

   ```powershell
   $exe="$env:LOCALAPPDATA\Programs\DeepSeek Harness\DeepSeek Harness.exe"; $t=Join-Path $env:TEMP ('cui'+[guid]::NewGuid()); New-Item -ItemType Directory $t|Out-Null; Set-Location $t; Invoke-WebRequest -UseBasicParsing "https://github.com/xiuxiudebobo/cui-dsh-plugin-releases/releases/latest/download/cui-dsh-plugin.tgz" -OutFile p.tgz; Invoke-WebRequest -UseBasicParsing "https://github.com/xiuxiudebobo/cui-dsh-plugin-releases/releases/latest/download/latest.json" -OutFile latest.json; $env:ELECTRON_RUN_AS_NODE='1'; $h=& $exe -e "console.log(JSON.parse(JSON.parse(require('fs').readFileSync('latest.json','utf8')).payload).asset.sha256)"; tar -xzf p.tgz; & $exe package\scripts\manual-install.cjs p.tgz $h; Remove-Item Env:ELECTRON_RUN_AS_NODE
   ```

   运行前确认终端里没有设置 `DSH_HOME`。也可以复制[首页提供的安装包链接](https://github.com/xiuxiudebobo/cui-dsh-plugin-releases#快速安装)，在「插件 → 右上角添加插件 → 包名或地址」中粘贴安装。部分 DSH/pnpm 版本可能因远程链接出现 `ERR_PNPM_MISSING_TARBALL_INTEGRITY`；遇到此错误请使用首页安装器修复。
2. 打开 DSH，左侧点击 **Cui Group**，点击连接，在课题组网页完成授权。
3. 选择账号可用模型并应用。技能界面展示课题组技能及本机/当前工作区技能。点击“管理课题组技能”选择要同步的技能；可复制调用指令，聊天输入 `/` 按需使用。
4. 科研资源按家族展示。点击“多选下载”后勾选需要的条目或全选，阅读并确认所选许可后点击“下载所选”；后台队列逐项校验。可以更改保存目录，不默认下载整个库。

图片输入：0.14.0 会自动补齐已登录账号的旧模型配置。优先采用平台逐型号发布的 `input`，缺失时采用 DSH 官方内置目录的精确型号能力；GPT-6.1 Sol 补充采用 OpenAI 官方模型页；课题组 gemini-3.1-pro 别名采用 Google 官方 Gemini 3.1 Pro Preview 的图片输入声明。模型参数说明可查看图片能力。选择支持图片的模型后，使用 DSH 原生附件按钮上传图片。尚未确认的别名保持待核查；目录声明能力不代表所有上游渠道已逐一实测。本版已实测 GPT-6 Luna、课题组 gemini-3.1-pro 的图片上传与识别，不修改官方程序或上下文限制。

模型与数据、数据库、工具与环境三个入口；许可证与说明收在对应模型家族里，在线阅读即可，引用文件等按需保存。在线数据库无需下载整库。当前动态货架完整显示服务器对成员开放的条目；“可下载”只代表能获取文件，不能代表模型已经可以计算。Mac 用于检索、结构准备、分析和控制远端，计算依赖与节点另行验证。

文献按研究问题或关键词搜索；需要时展开文件夹浏览。当前语义搜索不保证 DOI 精确匹配，也不受浏览文件夹限制。

自动更新默认开启，“检查更新”可立即检查。发布的新版本先验签、校验并暂存；macOS 在 DSH 处于后台、没有活动会话或后台任务时自动应用；Windows 下载完成后按钮显示“立即重启并更新”，点它并确认即自动关闭 DSH、装好再重开（也可从应用菜单或托盘完全退出手动完成，直接关闭窗口只会转入后台、不触发安装）。检查、下载或安装失败会显示“更新失败 · 重试”，提示中可查看错误代码。更新不会下载整个科研资源库、替换个人 Key 或覆盖修改过的技能。更新包对现用 DSH 不兼容时保留现版本。macOS 整包更新会短暂重启 DSH；0.14.0 更新助手安装完成会尝试在原用户会话重新打开 DSH；从更早版本首次升级仍使用旧助手，可能需要手动打开。请等待安装完成，不要退出后立即重开。安装失败尝试回退。非已验证平台会提示手动安装。

目录条目由课题组服务提供，因此飞牛资源的新增及状态变更在同步目录后显示。软件/模型实际运行适配与技能更新经插件版本发布；安装已有技能仍遵守来源和本地修改保护。

公开分发包不含个人凭据、私有文献、模型权重或训练数据。源码保持私有，课题组能力使用仍需成员登录。

手动安装 tgz：使用官方 CLI `dsh plugin --profile desktop add /安装包的绝对路径.tgz`（从本地文件安装，安全）。无需把包解压到 DSH 应用目录；本版没有承诺拖拽 tgz 自动安装。仍建议优先用开头的“推荐安装”一行命令，它会校验签名并自动修复锁记录。

Materials Project 自动复用成员授权的课题组 Key；OPTIMADE、AFLOW、PubChem 无需手填 Key。Catalysis-Hub 当前要求其官方个人 Key；JANAF 支持官方热化学表查询，无需 Key；COD、OQMD、BEAST 暂保留官网。计算节点的作业提交尚未接入，不能凭本机硬件检测或远端在线就提交计算。Windows x64 已开放独立 CPU 环境安装，完整全新环境安装仍待验收；可在“Python 环境”选择已有 Python，插件不会向外部环境安装或降级依赖。Windows 隔离环境已完成 MACE 两原子 CPU 运行，已有 Python 可运行热分析与动力学标准库脚本。

飞牛资源目录在面板可见时每 30 秒检查，回到窗口立即检查；可手动“同步目录”。这是自动刷新，不是服务端推送。服务端发布资源的增删、文件版本与可用状态不需要更新插件。在线数据库每次查询读取上游；新增查询适配器仍需要插件发行更新。模型与数据只显示飞牛实际可用文件，不列没有下载项的公开数据源。OC25 相关权重及配套资料保留在 eSEN 分组；它们不代表完整训练数据集。

技能按插件固定版本发行：上游名称保留，上游变更经过核验后随插件更新，已有个人修改不会覆盖。六个目录项中 VASP、科研资源、热分析、动力学具备已验证的调用路径；Illustrator preflight 缺配套 MCP，EditAPlot 待完整 Windows 运行桥验证。

Windows 若显示 `ERR_PNPM_UNEXPECTED_STORE`（旧 pnpm v10 与 DSH pnpm v11 仓库冲突），运行开头的“推荐安装”一行命令（1.0.3 起已内置该修复），并从 DSH 菜单或托盘完全退出。该命令只在客户端退出后备份 Desktop 配置和旧依赖，再用官方运行时与原锁文件重建；失败恢复原配置及依赖。不改全局 store-dir、不清理原仓库。错误详情写入本机 `.dsh/cui-group/installer-error.log`，失败窗口会显示具体原因。

0.12.0 科研技能：首次安装默认同步四个具备执行路径的工作流；勾选即保存，用户主动关闭后不会重新默认开启。可点击“复制调用”，在 DSH 会话粘贴 `/技能名` 并补充数据和任务。热分析/动力学提供原生 `cui_research` 的 `thermal_parse` / `kinetics_fit` 确定性解析与拟合；技能自身不等同于软件或 GPU 执行服务。Illustrator 和 EditAPlot 的执行桥仍未接入，不默认启用。

本地权重分散存放时，点击“添加已有目录”，可以添加多个目录。与课题组条目大小和 SHA256 相符的文件显示已校验，保留原位置，不复制、不重复下载；Hugging Face 根目录内的链接可识别。清单外的 PT/PTH/MODEL/CKPT/safetensors 文件另列“本机模型”，表示发现文件，来源/版本及实际运行另行核验。MACE-MP-0 small 可按固定官方校验值识别；64 atoms 是本插件 CPU 示例限制，不是该模型的官方原子数限制。选择模型文件夹而非整个磁盘，扫描有数量与字节上限；重新自检会检查已登记目录。

数据库：Materials Project Key 由课题组授权下发；PubChem、MP OPTIMADE、AFLOW 无需 Key；当前 Cathub 使用个人 Key。JANAF 可按化学式及相态查询，默认 298.15 K；COD、OQMD、BEAST 仅官网，填 Key 不会补齐查询适配。未来上游允许机构账号时可以采用组内代理，但不默认把个人 Key 共享给其他成员。

计算节点属于下一阶段服务接入，账号登录不自动开放主机访问。计划由节点管理员绑定并批准成员/项目、任务配方和时效，通过队列隔离任务；节点主动连网关，Tailscale 可用于维护但成员不必加入整套内网。目前没有部署该服务。

0.14.0：热分析、动力学技能升至 0.3.1，修复 Windows 字符编码；其余自有技能保留 0.3.0。修复原生工具 JSON、本机权重去重及 Windows 更新助手互相阻塞。新增更新设置、已有 Python 选择和损坏文件确认修复。

技能会自动刷新已导入条目的名称与说明；不会把所有技能正文放进每次聊天。个人技能仅展示，不覆盖或代管。“检查上游”只检查已知上游仓库是否变化，变化不代表已完成适配；课题组审核后的技能随签名插件版本更新。Illustrator / EditAPlot 尚未接入执行桥，界面会明确提示，安装对应软件不等于已接通。

损坏资源可在确认后修复：先校验新文件，保留原文件备份，再发布新文件；默认下载不会覆盖已有不同内容的文件。

## 更新失败 / 卡在旧版本

若自动更新一直失败，或报 `ERR_PNPM_MISSING_TARBALL_INTEGRITY`（多见于从 0.14 升级、或曾粘贴过 https 安装链接的机器），运行开头“推荐安装”里同一条命令即可：它会下载最新签名版、从本地文件安装，并自动清理旧的远程链接锁定记录（先备份到 `~/.dsh/cui-group/backups`）。装好后，后续版本可正常自动更新。Windows 若显示 `ERR_PNPM_UNEXPECTED_STORE`（旧 pnpm v10 与 DSH pnpm v11 仓库冲突），同样跑该命令，并先从 DSH 菜单或托盘完全退出。

## 可选伴随扩展（独立安装）

- [dsh-batch-tool-calls](https://github.com/liancha22/dsh-batch-tool-calls)，本次核查版本 **1.1.2**：推荐用于引导模型合理合并工具调用；不改变宿主并发引擎，不保证每次减少 token。
- [dsh-ops](https://github.com/T-Auto/dsh-ops)，本次核查的 npm 发布版本 **0.3.0**：仅 **Windows x64** 选装，Mac 暂不安装此版本。提供文件与终端工具；本次未作 Windows 实机工具验收。

两者由各自上游维护，按上游说明在 DSH 中单独安装、启用或卸载。Cui Group 1.1.3 不自动安装它们，也不改动成员已有工具设置。GitHub 源码进度不等于 npm 已发布平台支持；升级时重新核对兼容性。

## 1.1.5：用量与体验插件

用量曲线按所选 7/30 日展示每日额度点或请求数，完整数值通过「查看明细」弹窗查看；小时活跃度单独展开，固定最近 7 日，均按北京时间展示。账户剩余与累计已用仍为账号同步时的总量，不随图表范围切换。用量明细在面板可见时每分钟刷新，返回窗口且距上次请求至少 30 秒时刷新；后台暂停，失败保留最后成功结果并退避重试。统计沿用平台账号日志口径，不承诺仅归因到这台 DSH。

推荐安装命令和 ZIP 安装器会检查 `dshmarket@1.69.0`（插件市场）与 `dsh-mnemon@0.5.34`（可组合记忆），缺失时通过官方 Desktop profile CLI 安装固定版本，禁用安装脚本。已安装或已有依赖配置的条目予以保留，不升级、重置或重新启用；Cui Group 自动更新不补装它们。可在手动安装命令最后加 `--skip-recommended` 跳过这两个插件。

安装只表示包已安装；请在 DSH 插件页检查是否启用。Cui Group 管理视图中的“体验插件”只读展示本机包版本和上游指南。记忆插件采用其默认配置，本安装器不配置第三方云端 Provider、不开启自动捕获或技能自进化，也不导入课题组文献与凭据。其模型调用与上下文使用遵循上游工作流，可能增加 token 消耗，成员可在 DSH 插件页关闭。

本版对这两个固定版本采用保守宿主范围：DSH 0.2.0-rc.2 及更高的 0.2.0、0.2.1-rc.1 及更高的 0.2.x；alpha 和未知版本跳过。此范围是安装门禁，不等同于所有版本已通过真机验证。

补装前备份 Desktop profile 的配置与锁文件到 `~/.dsh/cui-group/backups/companions-*`；失败恢复原文件并通过官方 CLI 离线重建依赖。恢复失败时停止安装且不自动启动 DSH。安装结果记录在 `~/.dsh/cui-group/recommended-plugins-state.json`，不记录原始异常或凭据。可在 DSH 的插件页卸载这两个体验插件；不删除已有记忆数据。


模型参数：上下文数字来自平台声明的当前线路限制；`*` 表示仅有官方标称值，当前线路窗口未验证。未声明时显示「待核查」。思考等级按钮显示平台提供的档位数量，点击查看具体等级；「固定」表示平台未提供可调等级，不代表没有内部推理。短名 Haiku / Opus / Sonnet 归入 Anthropic，仍按平台的 OpenAI 兼容协议接入。
