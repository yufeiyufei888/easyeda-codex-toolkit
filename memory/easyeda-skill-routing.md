# EasyEDA 技能路由记忆（V3）

## 基本原则

- 技能决定工作方法，不授予修改工程的权限。
- 设计判断、实时工具操作、质量验收和社区包维护分层处理。
- 只加载完成当前任务所需的最小技能集和引用资料。
- 当前工作区的 `easyeda-agent` 优先于任何历史或用户级操作副本。

## 阶段路由

| 场景 | 首选技能 | 需要时组合 |
| --- | --- | --- |
| 实体硬件需求、选型、系统架构、电源树和资源预算 | `hardware-architecture-analysis` | 形成具体电路后转原理图技能 |
| 具体原理图设计、计算或审查 | `schematic-design-review` | 实时工程加 `easyeda-agent`；验收加 `easyeda-quality-gates` |
| 具体PCB布局、布线、叠层、DRC或DFM | `easyeda-pcb` | 实时工程加 `easyeda-agent`；验收加 `easyeda-quality-gates` |
| 当前EasyEDA工程的识别、读取、获准修改、检查、保存或导出 | 工作区 `easyeda-agent` | 电气判断加原理图/PCB技能；验收加质量门禁 |
| 只读学习、完整审计、检查结果分类或最终验收 | `easyeda-quality-gates` | 实时工程同时使用工作区 `easyeda-agent` |
| CLI/daemon/Connector安装升级、版本兼容、连接/动作故障、块库维护 | `easyeda-agent-community-maintenance` | 不接管普通工程设计 |
| 扩展、`eda.*` API、库对象、源格式或Bridge开发 | `easyeda-api` | 需要实时工程操作时再加工作区 `easyeda-agent` |

## 关键分界

- `easyeda-agent` 是操作层，不负责独立给出电路或PCB工程结论。
- `easyeda-quality-gates` 是证据和验收层，不负责连接客户端或执行CLI。
- `easyeda-agent-community-maintenance` 只在用户明确要求维护社区包或排查工具链故障时使用。
- 纯App、网站、桌面、后端和算法任务不触发电子方案技能；只有请求涉及实体硬件设计或变更时才进入硬件路线。

## 证据与交付

跨原理图和PCB的任务先完成原理图检查，再完成PCB检查。证据顺序为：权威设计数据、原生DRC/check/layout-lint、正确视角的视觉检查。报告应写明准确工程/文档、只读或修改状态、检查结果、问题分类、保存点和未完成门禁；不得把健康检查、静态规则或截图描述为实板验证。
