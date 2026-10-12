# Cui Group for DeepSeek Harness

公开安装包与签名更新源。源码仓库私有；模型、文献与私有资料仍需课题组成员登录。

## 安装

1. 先安装官方 DeepSeek Harness Desktop **0.2.0-rc.2**。
2. 下载对应安装器，**完整解压**：
   - [Windows 安装器](https://github.com/xiuxiudebobo/cui-dsh-plugin-releases/releases/latest/download/Cui-Group-Windows-installer.zip)：双击 `Install-Cui-Group.cmd`。按提示从 DSH 应用菜单或托盘选择退出，再继续安装。
   - [macOS 安装器](https://github.com/xiuxiudebobo/cui-dsh-plugin-releases/releases/latest/download/Cui-Group-macOS-installer.zip)：双击 `Install-Cui-Group.command`，确认后自动退出安装。
3. 安装后在 DSH 左侧打开 **Cui Group**，连接课题组账号，选择模型并应用。

无需管理员权限、另装 Node.js、解压到官方应用目录或拖入客户端。Windows 能识别自定义盘符；未打开 DSH 时按提示选择官方 EXE。[全部安装包](https://github.com/xiuxiudebobo/cui-dsh-plugin-releases/releases/latest)。

## 使用与更新

- 默认用量为 7 天＋额度。科研资源按家族展开，选择“多选下载”后才显示选择圈；支持自定义保存目录。
- 技能选择后同步至 DSH 原生目录，聊天输入 `/` 按需使用。热分析和动力学脚本只需要 Python 3。
- Materials Project 自动获取成员授权的课题组 Key；PubChem、OPTIMADE、AFLOW 无需手填 Key。Catalysis-Hub 需要其个人 Key。
- 自动检查、验签并下载发行包。macOS 在后台且没有活动会话/任务时冷更新；Windows 等 DSH 正常退出后安装，下次打开生效。直接关闭 Windows 窗口只会进入后台。
- 飞牛目录随同步更新；代码和技能随插件发行更新，个人 Key、已有资源和修改过的技能保留。

验证范围：macOS arm64 原生界面及工具；Windows x64 独立配置安装、环境检测、技能同步、校验下载、签名更新下载。Windows 等退出安装的完整周期仍待验收。MACE 重环境安装目前只验证 macOS arm64；Origin、Illustrator 执行桥和远端作业提交仍待接入。下载权重不代表已经可以计算。
