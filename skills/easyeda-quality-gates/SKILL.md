---
name: easyeda-quality-gates
description: >-
  EasyEDA/嘉立创EDA source-project quality gates and acceptance evidence. Use only for read-only study, audit, or review of a named schematic/原理图 or PCB; for final verification after actual design edits; or to classify DRC/check/layout-lint findings. It owns scope freeze, datasheet-backed criteria, visual/electrical/DFM closure, and completion claims. It does not connect to EasyEDA, execute CLI actions, or answer standalone circuit/PCB theory; pair it with the workspace easyeda-agent for live projects.
---

# EasyEDA Quality Gates

Use this skill as the quality and acceptance layer. Use the current workspace
`easyeda-agent` as the operational source for CLI commands, connector behavior,
library lookup, document access, and exports.

Do not use this skill as a second design manual. Circuit design belongs to
`schematic-design-review`, PCB engineering belongs to `easyeda-pcb`, and early
hardware architecture belongs to `hardware-architecture-analysis`. Load this skill alongside those
only when an EasyEDA source project needs an auditable acceptance loop.

## Route The Task

Load only the references required by the active branch:

- Schematic creation, editing, or review: [schematic-quality.md](references/schematic-quality.md)
- PCB creation, editing, or review: [pcb-quality.md](references/pcb-quality.md)
- Learning or auditing an existing project: [read-only-audit.md](references/read-only-audit.md)
- MCU development boards, USB, RF, or dense breakout boards:
  [development-board-patterns.md](references/development-board-patterns.md)
- Intelligent-vehicle or other dense contest mainboards:
  [contest-control-board-patterns.md](references/contest-control-board-patterns.md)
- NE555 circuits or contest tasks: [ne555-patterns.md](references/ne555-patterns.md)

For a task spanning schematic and PCB, complete the schematic branch first, then
the PCB branch. Apply every applicable branch before declaring completion.

## Evidence Ladder

Judge each gate in this order:

1. Authoritative design data: parts, pins, nets, primitives, layers, rules, and
   schematic-to-PCB linkage.
2. Native checks: EasyEDA DRC plus the relevant `check` and `layout-lint` output.
3. Visual evidence: readable schematic zoom, physically correct PCB top/bottom
   views, and 3D/mechanical inspection when geometry matters.

Treat automated findings as candidates until the netlist, primitive geometry,
physical side, and design intent agree. Classify each finding as confirmed,
intentional/project-specific, checker limitation, or unresolved.

## Step 1: Freeze Scope

Record the exact project, document or pages, requested deliverables, and whether
the task is read-only or authorizes mutation. Keep reference projects and pages
outside that list untouched.

**Complete when:** the target and allowed actions are explicit, the active
EasyEDA project/document matches them, and every planned action fits the granted
authority.

## Step 2: Build The Design Contract

Recover or define the power tree, functional modules, interfaces, major ICs,
clocks, reset/programming paths, critical calculations, mechanical constraints,
and expected page split. Resolve uncertain electrical facts from the exact
manufacturer datasheet or application note.

**Complete when:** every functional requirement maps to a schematic block or PCB
constraint, every major rail and interface has a source and destination, and no
unverified assumption is presented as final.

## Step 3: Close The Schematic Gate

Apply [schematic-quality.md](references/schematic-quality.md) and any conditional
reference selected above. Work by functional module, then read back connectivity
and run the evidence ladder.

**Complete when:** every pin is connected or intentionally NC, calculated values
meet their stated requirement, the authoritative net data has no unexplained
short/open/mismatch, all check findings are classified, and every page passes
readable visual QA including title-block metadata.

## Step 4: Close The PCB Gate

Confirm schematic linkage, then apply [pcb-quality.md](references/pcb-quality.md)
and any conditional reference. Preserve the priority order: mechanical and
safety constraints, critical current/signal loops, return paths, thermal needs,
functional grouping, DFM, then cosmetics.

**Complete when:** placement and routing are electrically and mechanically
accounted for; critical nets, planes, pours, vias, keep-outs, and both physical
sides have been inspected; authorized changes are followed by copper rebuild and
a clean final verification loop; every remaining finding is classified.

## Step 5: Close The Evidence

For mutation work, read back every changed primitive and save only the verified
checkpoint. For read-only work, preserve project content and state any final gate
that would require mutation. Report the project/document identity, changes or
read-only status, checks run, result counts, unresolved evidence, and artifact
paths.

**Complete when:** the report accounts for every requested deliverable and every
finding, identifies the saved or unchanged state, and makes no completion claim
stronger than the available evidence.
