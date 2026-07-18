# EasyEDA Codex Toolkit

嘉立创EDA（EasyEDA）相关的 Codex skills、连接记忆与设计参考备份。内容覆盖电子方案分析、原理图绘制与审查、PCB 布局布线、质量门禁、客户端连接、BOM/网表和扩展 API。

> 仓库默认按私有资料库创建。这里包含机器相关的连接经验；如需公开，请先复核路径、版本与第三方许可。

## 内容导航

| 路径 | 定位 | 主要内容 |
| --- | --- | --- |
| [`skills/easyeda-agent`](skills/easyeda-agent/) | 社区 typed 自动化工作流 | 原理图/PCB 操作、设计流程、布局布线约定、DRC/lint、BOM 与器件选择脚本 |
| [`skills/easyeda-api-skill`](skills/easyeda-api-skill/) | EasyEDA API 与 Bridge 参考 | API 索引、原理图/PCB 文档格式、扩展开发指南、WebSocket Bridge |
| [`skills/电子方案分析`](skills/电子方案分析/) | 方案阶段 | 需求澄清、器件选型、系统框图、电源树、风险与成本评估；默认不改工程 |
| [`skills/schematic-design-review`](skills/schematic-design-review/) | 原理图阶段 | 设计/审查分流、器件与网络检查、原理图 DRC、PCB 转换准备 |
| [`skills/easyeda-pcb`](skills/easyeda-pcb/) | PCB 阶段 | 布局、布线、差分对、铺铜、DRC、DFM、Gerber/BOM/装配输出 |
| [`skills/easyeda-quality-gates`](skills/easyeda-quality-gates/) | 验证门禁 | 先原理图后 PCB 的分阶段检查、DRC/check/layout-lint 证据与发布结论 |
| [`memory/easyeda-connection-workflow.md`](memory/easyeda-connection-workflow.md) | 本机连接记忆 | daemon、客户端、连接器、重连步骤、成功判定与故障处理 |
| [`memory/easyeda-skill-routing.md`](memory/easyeda-skill-routing.md) | 技能路由记忆 | 何时选用方案、原理图、PCB、Agent、API 与质量门禁技能 |
| [`memory/easyeda-read-only-learning.md`](memory/easyeda-read-only-learning.md) | 只读学习记忆 | 工程学习/审查的边界、证据标准与输出结构 |
| [`docs/verified-connection.md`](docs/verified-connection.md) | 本次验证快照 | 已验证的版本、端口、能力和当前文档状态 |

## 能力范围

- 连接与重连嘉立创EDA V3，验证 daemon、connector 与 typed API 通道。
- 方案：从需求、选型、系统架构和风险评估进入设计。
- 原理图：器件放置、连线、网络标识、分页规划、规则检查与 PCB 转换准备。
- PCB：同步、器件布局、走线、铺铜、层/网络检查、DRC、layout lint 与 DFM。
- 质量门禁：将原理图、PCB 与制造检查的结果分类为通过、有条件通过或未通过。
- 器件与制造：LCSC/JLC 器件选择、BOM 丰富、网表和制造资料参考。
- 扩展开发：EasyEDA API 类、枚举、接口、文档源格式和 Bridge 调试。

## 使用原则

1. 按“方案分析 → 原理图 → PCB → 质量门禁”选择最小适用技能集。
2. 任何设计操作前先检查连接健康、当前工程与文档类型。
3. 修改前先读取工程、页面、元件、引脚、网络、层和规则；审查和学习默认只读。
4. PCB 与原理图坐标单位不同；API 参数、枚举和返回类型必须查文档，不猜值。
5. 以 `check`、`drc`、`layout-lint` 等数据结果判断正确性，截图只作为视觉验证。

## 安装到 Codex

将需要的 skill 目录复制到个人 Codex skills 目录，并保持目录名不变：

```powershell
Copy-Item -Recurse .\skills\easyeda-agent "$env:USERPROFILE\.codex\skills\easyeda-agent"
Copy-Item -Recurse .\skills\easyeda-api-skill "$env:USERPROFILE\.codex\skills\easyeda-api-skill"
Copy-Item -Recurse .\skills\电子方案分析 "$env:USERPROFILE\.codex\skills\电子方案分析"
Copy-Item -Recurse .\skills\schematic-design-review "$env:USERPROFILE\.codex\skills\schematic-design-review"
Copy-Item -Recurse .\skills\easyeda-pcb "$env:USERPROFILE\.codex\skills\easyeda-pcb"
Copy-Item -Recurse .\skills\easyeda-quality-gates "$env:USERPROFILE\.codex\skills\easyeda-quality-gates"
```

`easyeda-api-skill` 的 Bridge 依赖不随仓库提交；需要时在该目录运行 `npm install`。

## 来源与许可说明

- `easyeda-agent` 是社区工作流，skill 内标注来源：<https://github.com/zhoushoujianwork/easyeda-agent>。
- `easyeda-api-skill` 的 `SKILL.md` 元数据标注 MIT，作者为 JLCEDA；本仓库保留其原始元数据与文档。
- 根目录不对所有第三方内容统一重新授权；公开分发前应按各来源许可复核。

## 2026-07-18 更新说明

这是基于原有连接与 API 资料完善的第二版：新增电子方案分析、原理图审查、PCB 设计与质量门禁四个阶段的资料，并补充只读审查和技能路由记忆。`easyeda-quality-gates` 由既有工作流规则整理为独立 Skill，用于把检查结果和发布结论建立在可复核证据上。
