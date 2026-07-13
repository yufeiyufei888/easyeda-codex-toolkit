# 嘉立创EDA连接与重连记忆

更新时间：2026-07-13

## 适用范围

当用户要求“连接嘉立创EDA”“连接 EasyEDA”或“重新连接嘉立创EDA”时，直接执行本流程，不重复询问基础路径、端口或连接方式。只做连接时，不主动打开或修改工程。

## 本机配置

- 首选 CLI/daemon：`%USERPROFILE%\.local\bin\easyeda.exe`
- daemon 版本：`easyeda-agent v0.11.0`
- 嘉立创EDA V3：`C:\Program Files (x86)\lceda-pro\lceda-pro.exe`
- EasyEDA Agent Connector：`0.11.3`
- 默认监听：`127.0.0.1:49620-49629`，通常为 `49620`
- 旧版 `%USERPROFILE%\.codex\bin\easyeda.exe` 为历史副本，不作为默认入口

## 快速连接

1. 检查 daemon：

   ```powershell
   & "$env:USERPROFILE\.local\bin\easyeda.exe" daemon health
   ```

2. 若返回 `status: not_found`，用隐藏后台进程持久启动：

   ```powershell
   Start-Process -FilePath "$env:USERPROFILE\.local\bin\easyeda.exe" `
     -ArgumentList @('daemon','start','--autosave-debounce','3s') `
     -WindowStyle Hidden
   ```

3. 查找并激活当前嘉立创EDA V3 窗口；若未运行，启动上述 V3 可执行文件。
4. 在顶栏 `EasyEDA Agent` 菜单中确认自动连接已开启；必要时执行 `Reconnect`。
5. 再次运行 `daemon health`，根据数据判定是否成功。

## 成功判定

必须同时满足：

- `status: found`
- `service: easyeda-agent`
- `windows` 至少有一个当前 V3 窗口
- 窗口项含 `connectorVersion`、`easyedaVersion`、`connectedAt`、持续更新的 `lastSeen`
- `capabilities` 至少包含 `schematic.v1` 或 `pcb.v1`

本机当前同时提供：

- `schematic.v1`：原理图能力
- `pcb.v1`：PCB 能力

可选只读验证：

```powershell
& "$env:USERPROFILE\.local\bin\easyeda.exe" project info
```

若首页状态返回 `EDA_CALL_FAILED: No current project is open.`，说明 typed API 已到达连接器，但当前没有打开工程；不能把它描述成工程读取成功，也不能误判为连接失败。

## 版本一致性说明

daemon `0.11.0` 与 connector `0.11.3` 当前可以通信，但健康数据可能显示 `connectorVersionOk: false`。这表示版本一致性检查未通过，不等于连接断开。报告时应分别说明：

- 实际通信是否建立；
- 版本是否完全匹配。

## 常见故障

- daemon 不存在：只启动一个首选 daemon，轮询到 `found`。
- daemon 在线但 `windows` 为空：启动/激活嘉立创EDA V3，启用自动连接后执行 `Reconnect`。
- 菜单没有 EasyEDA Agent：检查扩展是否存在、启用，以及“允许外部交互”是否开启；安装、更新或卸载扩展前另行确认。
- `connectorVersionOk: false` 但 `lastSeen` 更新：连接有效，另行提示版本风险。
- 首页 `documentType: home`：只是未打开工程。
- 客户端重启后 window ID 会变化：每次重新发现窗口，不复用旧 ID。

