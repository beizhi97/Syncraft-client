# Syncraft Windows 客户端

这是 Syncraft 的**用户下载仓库**。无需安装 Node.js、pnpm 或 Docker：直接从 [Releases](https://github.com/beizhi97/Syncraft-client/releases) 下载已打包并通过严格发布预检的 Windows 客户端压缩包即可使用。

服务端管理员请使用 [Syncraft-server](https://github.com/beizhi97/Syncraft-server) 部署服务。完整开发源码与协议合同保留在 [Syncraft](https://github.com/beizhi97/Syncraft)。

## 下载与启动（目录优先双码接入流程）

1. 在最新 [Release](https://github.com/beizhi97/Syncraft-client/releases) 下载 `SyncraftDesktop.zip` 和同名 `SyncraftDesktop.zip.sha256`。
2. 在 PowerShell 校验下载文件的 SHA-256 哈希：

   ```powershell
   Get-FileHash -LiteralPath .\SyncraftDesktop.zip -Algorithm SHA256
   ```

   输出必须与 `.sha256` 文件中的首列一致；不一致时停止使用并重新下载。
3. 解压到用户可写、不会被系统清理的固定目录，例如 `C:\Tools\Syncraft\`。不要直接在压缩包预览目录、下载临时目录或系统受保护目录中运行。
4. 双击运行 `SyncraftDesktop\Syncraft.exe`。首次启动后进入分步接入向导：
   - **第一步（导入通道配置码）**：粘贴管理员提供的通道配置码，填写设备名称并提交设备身份申请。
   - **第二步（输入一次性身份验证码）**：管理员在服务端控制台为您的申请勾选授权目录并签发一次性身份验证码后，在客户端输入该验证码完成身份核验。
5. **选择同步目录与本地文件夹**：
   - 从服务端已授权目录列表中选择要同步的服务端目录（同步方向由服务端授权决定）。
   - 点击**“浏览…”**使用 Windows 原生文件夹选择器选择本地同步文件夹（或手动粘贴本地路径），保存任务。
6. **首次双向冲突保护与初始化确认**：
   - 首次执行双向同步前，客户端会自动扫描双端同名不同内容冲突。若存在冲突，可一键点击**“保存双方版本”**保留两份副本，再显式点击**“初始化双向”**建立双向同步基准，随后即可按手动或定时计划自动同步。

`SyncraftClient.zip` 是便携式兼容回退包；正常情况下优先使用 Electron 桌面包 `SyncraftDesktop.zip`。

## 日常使用与故障恢复

- **一键修复连接**：遇到网络波动或通道异常时，可在主界面点击**“修复连接”**自动检测并恢复控制通道与 SFTP 数据通道。
- **服务端重设连接配置不断任务**：当服务端更换端口/密钥并签发新通道配置码时，直接导入新通道配置码即可沿用既有授权关系、已保存任务和双向同步基准，无需删除任务或重新初始化。
- **误删历史版本恢复**：服务端误删文件后，可在客户端历史恢复面板查看并从本地历史版本恢复。
- **传输自愈**：客户端自有 `sing-box.exe` 数据通道在传输中途若发生瞬时异常退出，会自动重算安全计划并重试恢复传输。

## 升级

先退出 Syncraft，保留旧目录和本地 `data/`（或 `%LOCALAPPDATA%\Syncraft\data`）作为回滚副本。将新版 ZIP 解压到新目录后启动；确认既有任务、授权关系与同步历史正常后，再清理旧版本目录。

客户端仅对受管 `rclone.exe` 子进程注入本地回路代理，不会修改 Windows 系统代理、路由表、DNS、防火墙或安装系统服务。遇到问题请在“设置”抽屉导出脱敏诊断包，切勿上传通道配置码、一次性身份验证码、SyncKey、VLESS URI 或任何私钥。

## 当前发布版本与校验信息

仓库内 `checksums/` 与 `releases/` 保存已发布版本的 SHA-256 侧车文件与构建溯源清单，Release 页面中的同名 `.sha256` 文件为对应发布包的权威校验值。

- **当前已发布版本**：[`v0.3.0-rc.3-sfsc-4765c02d125a`](https://github.com/beizhi97/Syncraft-client/releases/tag/v0.3.0-rc.3-sfsc-4765c02d125a)
- **构建批次（`buildId`）**：`sfsc-4765c02d125a`
- **主仓源码指纹（`sourceTreeHash`）**：`4765c02d125a54861f7e467e127b401a22548ad9ecb10583f44cffc3116c8822`
- **安装包 SHA-256**：
  - `SyncraftDesktop.zip`: `9f53d0585110bfbb80f12442c4c714bf95c9cf90d9f6f61f61279b9c8340e3ee`
  - `SyncraftClient.zip`: `68cb128fc056d5752dd24ed16dfde749312aaeb4c19e10366c51c51c1765f151`
