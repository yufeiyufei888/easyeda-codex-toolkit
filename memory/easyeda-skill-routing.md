# EasyEDA 技能路由记忆

## 选择原则

- 技能决定工作方法，不授予修改工程的权限。
- 优先选用当前工作区的 `easyeda-agent`；仅在没有工作区版本时使用用户级版本。
- 只加载完成任务所需的最小技能集和引用资料。

## 阶段路由

| 场景 | 首选技能 | 补充技能 |
| --- | --- | --- |
| 需求、选型、系统架构 | `电子方案分析` | 需要落地时转原理图技能 |
| 原理图设计或审查 | `schematic-design-review` | `easyeda-agent` + `easyeda-quality-gates` |
| PCB 布局、布线或审查 | `easyeda-pcb` | `easyeda-agent` + `easyeda-quality-gates`；先读关联原理图 |
| 连接或重连 | `easyeda-agent` | 仅在需要 GUI 证据时使用界面控制 |
| 扩展、`eda.*` API、库对象或源格式 | `easyeda-api` | 需要实时工程操作时再加 `easyeda-agent` |

## 证据与交付

对跨原理图和 PCB 的任务，先完成原理图检查，再完成 PCB 检查。以设计数据为主证据，原生 DRC/check/layout-lint 为第二层，界面视觉为补充。报告中应写明目标工程/文档、是否只读、检查结果、已分类问题和未完成门禁。
