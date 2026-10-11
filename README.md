# Cui Group for DeepSeek Harness

公开安装包和签名更新源。源码私有；模型、文献与飞牛私有资源使用仍需课题组成员登录。

## 安装

1. 安装官方 DeepSeek Harness Desktop（当前验证 macOS arm64 0.2.0-rc.2）。
2. [下载 macOS 安装器](https://github.com/xiuxiudebobo/cui-dsh-plugin-releases/releases/latest/download/Cui-Group-macOS-installer.zip)，解压，双击 `Install-Cui-Group.command`。
3. 安装完成后，在 DSH 左侧打开 **Cui Group** 并连接课题组账号。

[全部安装包](https://github.com/xiuxiudebobo/cui-dsh-plugin-releases/releases/latest)。其他平台可通过官方CLI安装tgz，但平台验证范围请以版本说明为准。

## 使用与更新

- 模型按账号权限选择；默认用量为7天＋额度。
- 技能勾选后同步，聊天输入 `/` 调用。
- 科研资源按实际类别同步，选择需要的资产与保存目录，不自动下载整个资源库。
- 默认自动检查签名发行包，下载后在没有活动会话/后台任务时冷更新；忙碌时等待，失败可回退。
- 飞牛目录内容通过同步直接更新；代码、适配器与技能随插件发行更新，已修改的技能保留。

下载不等于模型能运行，GPU节点与软件依赖需分别验证。Mac适合作为检索、准备与控制端。
