---
name: easyeda-agent
description: >-
  Live operations on the currently open EasyEDA/嘉立创EDA Pro project through this workspace's easyeda-agent CLI, daemon, and connector. Use only when the task requires connecting to or identifying the active window; reading a named project, schematic page, or PCB; performing explicitly authorized placement, wiring, layout, routing, synchronization, or saving; running native DRC/check/layout-lint; or exporting project artifacts. Do not use for offline electronics architecture, schematic theory, PCB-rule questions, screenshot-only review, package installation/upgrades, CLI/connector version compatibility, typed-action maintenance, or community block-library contribution; the last four use easyeda-agent-community-maintenance. Pair with easyeda-quality-gates when the live project is being designed, studied, reviewed, or finalized.
---

# EasyEDA Agent

Use the local `easyeda` CLI, daemon, and connector for typed, observable EasyEDA
operations. This skill owns tool usage; use `easyeda-quality-gates` for design
quality, domain rules, read-only audit behavior, and acceptance criteria.

This is an operation layer, not a circuit- or PCB-design encyclopedia. If no live
EasyEDA access or action is required, route the task to `电子方案分析`,
`schematic-design-review`, or `easyeda-pcb` instead.

## Step 1: Establish Context

Run `easyeda daemon health`, identify the current EasyEDA window, and verify the
exact project, document, page, and document type before any scoped action.

**Complete when:** the daemon reports a live EasyEDA connector with schematic or
PCB capability and the active project/document matches the authorized target.

## Step 2: Inspect Before Acting

Use typed read actions to recover documents, parts, pins, nets, board linkage,
layers, rules, and the relevant current state. Load only the branch references
listed below. Use `debug.exec_js` only when no typed action exists and the user
has accepted the debug path.

**Complete when:** the planned operation has a verified target, inputs,
constraints, units, and expected result; no mutation is needed merely to learn
the current state.

## Step 3: Apply Authorized Changes

Use typed actions and small, reviewable batches. Read back each batch before the
next one. Ask before destructive or broad actions such as bulk delete, clear,
import, or reroute. Save explicit verified checkpoints; treat debounced autosave
as recovery only.

**Complete when:** every intended primitive changed once, every changed object
reads back with the expected properties and connectivity, and unrelated project
content is unchanged.

## Step 4: Verify

Use design data first, then native DRC/check/layout-lint, then live visual
inspection. Treat a blank or byte-identical stale capture as a rendering-state
problem when design data proves the document exists; bring EasyEDA and the target
tab to the foreground before recapturing.

For recording, demos, tutorials, or screenshot deliverables, read the
`Recording / Demo Mode` section in [design-flow.md](references/design-flow.md) and
use the staged snapshot gate.

**Complete when:** current-document checks have result counts, every finding is
resolved or classified, the visible document matches the data, and any requested
capture is current and correctly identified.

## Step 5: Deliver

Report the target project/document, changed primitives or read-only status,
commands and checks run, saved checkpoints, unresolved evidence, and exported
artifact paths. Label each screenshot as native EasyEDA or data-rendered.

**Complete when:** every requested output and verification gate is accounted for
and the completion claim matches the recorded evidence.

## Reference Router

Load only the files required by the active operation:

- Whole-board or multi-stage work: [design-flow.md](references/design-flow.md)
- Schematic actions: [schematic.md](references/schematic.md) and
  [actions.md](references/actions.md)
- PCB actions: [pcb.md](references/pcb.md)
- Schematic presentation: [schematic-layout-conventions.md](references/schematic-layout-conventions.md)
- PCB placement/routing: [pcb-layout-conventions.md](references/pcb-layout-conventions.md)
- Automated placement/routing pitfalls: [auto-layout-sop.md](references/auto-layout-sop.md)
- Part selection: [part-selection.md](references/part-selection.md) and
  [standard-parts.json](references/standard-parts.json)
- Flag/port orientation: [orientation.json](references/orientation.json)
- Sheet geometry: [sheet-templates.json](references/sheet-templates.json)
- JLC fallback rules: [fab-rules-jlcpcb.json](references/fab-rules-jlcpcb.json)

## Bundled Scripts

- `scripts/lint.sh <project>`: live schematic lint and optional diff baseline.
- `scripts/tests/run.py`: validate orientation and linter behavior after rule or
  connector changes.
- `scripts/bom-enrich.py`, `parts-add.py`, `parts-select.py`: deterministic part
  selection and BOM enrichment.
- `scripts/calibrate.js`: recalibrate flag/port bboxes after connector changes.
