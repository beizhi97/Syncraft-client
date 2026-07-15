# Syncraft Windows 客户端

这是 Syncraft 的**用户下载仓库**。无需安装 Node.js、pnpm 或 Docker：从 [Releases](https://github.com/beizhi97/Syncraft-client/releases) 下载已打包的 Windows 客户端即可。

服务端管理员请使用 [Syncraft-server](https://github.com/beizhi97/Syncraft-server) 部署服务。完整开发源码与协议合同保留在 [Syncraft](https://github.com/beizhi97/Syncraft)。

## 下载与启动

1. 在最新 Release 下载 `SyncraftDesktop.zip` 和同名 `SyncraftDesktop.zip.sha256`。
2. 在 PowerShell 校验下载文件：

   ```powershell
   Get-FileHash .\SyncraftDesktop.zip -Algorithm SHA256
   ```

   输出必须与 `.sha256` 文件中的首列一致；不一致时停止使用并重新下载。
3. 解压到用户可写、不会被清理的目录，例如 `C:\Tools\Syncraft\`。不要直接在 ZIP、下载临时目录或系统受保护目录中运行。
4. 双击 `SyncraftDesktop\Syncraft.exe`。首次启动后由管理员提供一个新的 SyncKey；在设置页导入它。
5. 选择本地同步文件夹、同步方向和计划任务，再先运行预览。镜像同步会删除目标端多余文件，确认无误后才执行。

`SyncraftClient.zip` 是兼容性回退包；正常情况下优先使用桌面包 `SyncraftDesktop.zip`。

## 升级

先退出 Syncraft，保留旧目录和 `%LOCALAPPDATA%\Syncraft\data` 作为回滚副本。把新版 ZIP 解压到一个新目录后启动；确认任务与同步历史正常，再删除旧包。

客户端不会修改系统代理、路由、DNS、防火墙或安装系统服务。遇到问题请在设置页导出脱敏诊断包，切勿上传 SyncKey、VLESS URI 或任何密钥。

## 校验文件

仓库内 `checksums/` 保存当前候选版本的 SHA-256 侧车文件，Release 中的同名侧车文件才是每个发布版本的权威校验值。

当前交付版本：`v0.3.0-rc.1`。
