---
name: easyeda-quality-gates
description: >-
  Verify an EasyEDA schematic, PCB, or complete board before release. Use for
  read-only design review, DRC/check/layout-lint interpretation, electrical
  verification, PCB/DFM review, and before any authorized schematic or PCB
  change is declared complete.
---

# EasyEDA Quality Gates

Use this skill with the selected `easyeda-agent` for live project data. For a
normal engineering task, load the applicable schematic or PCB skill as well.
Use `easyeda-api` only for extension, API, or source-format work.

## Authority and Evidence

- Treat review, learning, checking, and diagnosis as read-only. Skill loading,
  a live connection, and a passing checker never authorize project changes.
- Identify the exact project, document, sheet, and board before any action.
- For whole-board work, inspect the linked schematic first, then inspect the
  PCB against that recovered intent.
- Prefer typed design data; use native DRC/check/layout-lint next; use the
  visible editor as corroborating evidence. Treat an automated finding as a
  candidate until it is located and explained.

## Gate 0 — Scope and Connection

1. Confirm the authorized target and whether the request is review or a named
   edit scope.
2. Verify `easyeda daemon health`, the current EasyEDA window, connector,
   active document type, and schematic/PCB capability.
3. Record the initial read-only or dirty state. Do not open, save, sync, or
   alter another project to obtain context.

Stop when the target or permission is ambiguous.

## Gate 1 — Schematic Readiness

Apply for schematic work or before PCB review:

- Confirm symbols, pin numbers, packages, power nets, network labels, ports,
  and no-connect markers from design data.
- Check power rails, decoupling, interface direction/pull-ups, protection,
  voltage domains, critical enable/boot/reset pins, and component ratings
  against the applicable datasheet.
- Check readable module boundaries, signal and power flow, meaningful labels,
  differential-pair naming, and unique references.
- Run schematic DRC/check. Classify every error and warning as fixed,
  accepted-with-rationale, false positive, or unresolved.
- Before a PCB handoff, confirm packages, nets, differential pairs, net
  classes, length groups, and the intended schematic-to-PCB update scope.

Do not claim electrical correctness merely because DRC passes.

## Gate 2 — PCB Readiness

Apply after Gate 1 for PCB work:

- Confirm board outline, holes, layers/stackup, fabrication limits, rules,
  component placement, keepouts, and connectors against mechanical intent.
- Check placement and routing from the schematic context: power loops and
  decoupling, return paths and plane continuity, high-current width/copper,
  sensitive analog routing, switching-node area, clock/crystal region,
  differential pairs, length constraints, vias, and copper pours.
- Check silkscreen, polarity, pin-one marks, exposed copper, board-edge
  clearance, assembly accessibility, test/debug access, thermal relief, and
  manufacturability.
- Run PCB DRC/check/layout-lint. Rebuild any derived copper only when an
  authorized change makes that necessary; rerun checks after that rebuild.

## Gate 3 — Release Evidence

Report a gate table with evidence rather than a binary assurance:

| Gate | Result | Evidence | Open items |
| --- | --- | --- | --- |
| Scope and connection | pass / blocked | target, health, capabilities | permission or context gaps |
| Schematic | pass / conditional / fail | DRC and inspected nets/components | classified findings |
| PCB | pass / conditional / fail | DRC/lint and inspected geometry | classified findings |
| Manufacturing | pass / conditional / fail | Gerber/BOM/assembly review if requested | missing exports or DFM risks |

State the project/document, checks and result counts, findings with locations
and severity, accepted exceptions with rationale, any unsatisfied gates, and
whether the result was strictly read-only. Only say a board is ready for the
requested release when every applicable gate is passed or the user explicitly
accepts documented exceptions.
