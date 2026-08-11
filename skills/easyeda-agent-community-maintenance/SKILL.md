---
name: easyeda-agent-community-maintenance
description: >-
  Maintenance and troubleshooting for the community easyeda-agent package. Use only when the user explicitly asks to install or upgrade its CLI/daemon/connector, diagnose version or connection/action failures, inspect upstream releases/plugin-market behavior, or query/contribute its circuit-block library. Do not use for ordinary EasyEDA project connection, reading, editing, schematic/PCB design, review, DRC, or export; those use the workspace easyeda-agent plus the relevant domain and quality-gate skills. Implicit invocation is disabled.
---

# EasyEDA Agent Community Maintenance

Maintain or diagnose the upstream/community automation package without taking
over routine project work. Ordinary access to the currently open EasyEDA project
uses the workspace `easyeda-agent`.

## Scope and routing

Use this Skill only for one of these explicit tasks:

- install, upgrade, remove, or compare community CLI/daemon/connector versions;
- diagnose daemon, connector, typed-action, or package compatibility failures;
- inspect upstream releases, plugin-market lag, or supported commands;
- search, validate, or contribute community circuit blocks.

Do not load this Skill merely because a task mentions EasyEDA, a schematic, PCB,
DRC, or connection. Project-level electrical judgment remains with
`schematic-design-review` or `easyeda-pcb`; live project operations remain with
the workspace `easyeda-agent`; source-project audit and acceptance use
`easyeda-quality-gates`.

## Step 1: classify the maintenance request

Record:

- requested outcome and whether changes are authorized;
- installed CLI, daemon, connector, and extension locations if relevant;
- whether the failure is installation, version mismatch, connection, typed
  action, or block-library related;
- exact error text and the smallest reproducible command.

Inspection and diagnosis are read-only. Installation, upgrade, removal, external
issue creation, pull requests, or project mutation require explicit user
authorization for that action.

**Completion standard:** one failure class and one authorized scope are stated;
an EasyEDA design project is not used as an unapproved test target.

## Step 2: collect evidence before changing anything

Prefer exact command output and version identifiers over screenshots or memory.
For connection faults, use `easyeda daemon health`, then inspect connector/window
state and version compatibility. A healthy daemon or nonempty window list does
not prove access to the user's named project.

Preserve:

- CLI/daemon/connector versions and installation source;
- command, arguments, exit status, and relevant error text;
- whether the failure reproduces without project mutation;
- any version skew between GitHub release and plugin-market package.

**Completion standard:** the observed state can be reproduced or the missing
evidence is named; no target-project access claim is based on health alone.

## Step 3A: installation or upgrade

Follow the current upstream README/release instructions rather than historical
commands in this Skill. Keep CLI, daemon, and connector versions compatible.
After an authorized change, restart only the required components and verify:

1. the expected executable/version is active;
2. `easyeda daemon health` reaches the expected daemon/connector;
3. a read-only command returns the expected command schema or context;
4. no unrelated EasyEDA project was opened or modified.

**Completion standard:** requested components report the intended compatible
versions and a read-only smoke test succeeds, or the exact remaining blocker is
reported.

## Step 3B: daemon, connector, or typed-action diagnosis

Use the smallest failing typed action. Consult the action reference for the
current signature; do not guess parameters. Use raw/debug execution only when no
typed action exists and the user explicitly accepts that diagnostic path. If a
test could mutate a project, use a disposable test document or stop for explicit
authorization.

Distinguish among:

- daemon unavailable;
- connector absent or attached to the wrong app/window;
- CLI/connector version mismatch;
- invalid or changed typed-action schema;
- stale document context;
- a real EasyEDA/API limitation.

**Completion standard:** the failure is isolated to one layer with supporting
output, and the proposed repair is limited to that layer.

## Step 3C: circuit-block library maintenance

Use offline `easyeda blocks ls/show/search` to inspect existing blocks. A block is
a candidate reference, not permission to alter an open design. For a new or
corrected block, follow the contribution reference, record exact parts and port
semantics, and run the package's validation/tests. Creating an external issue or
pull request requires the user's explicit approval.

**Completion standard:** the queried block is identified with its validation
status, or a contribution passes the documented checks and has an approved
external-publication step.

## References

Load only the branch needed for the explicit maintenance task:

- install/version/connector: `references/environment-setup.md`
- typed-action signatures and debug boundaries: `references/actions.md`
- block validation and contribution: `references/standard-blocks-contributing.md`

Do not load the community board-design workflow for routine project work.

## Final report

Report the diagnosed layer, evidence collected, changes actually made, validation
result, and any remaining blocker. State explicitly whether an EasyEDA project
was accessed or modified; maintenance success is not schematic/PCB acceptance.
