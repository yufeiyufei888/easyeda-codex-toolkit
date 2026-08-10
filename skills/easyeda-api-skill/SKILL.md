---
name: easyeda-api
description: EasyEDA/嘉立创EDA extension and API development. Use to look up or call eda.* APIs, execute through run-api-gateway, manage library objects by API, debug extensions, or analyze EasyEDA source formats. Use easyeda-agent for ordinary board design or review.
license: MIT
compatibility: Requires Node.js 18+ and an EasyEDA desktop client with extension support
metadata:
  author: JLCEDA
  version: "1.1.3"
  openclaw:
    requires:
      bins:
        - node
      env:
        - CLAUDE_SKILL_DIR
---

# EasyEDA API

Use this skill for `eda.*` API lookup, extension development, bridge execution,
and document-source analysis. Use `easyeda-agent` for ordinary schematic/PCB
inspection, drawing, placement, routing, DRC, and project learning.

## Route The Task

Load only the active branch:

- Bridge startup, connection, window selection, execution, units, or state:
  [bridge-and-execution.md](references/bridge-and-execution.md)
- Extension main-process or iframe behavior:
  [extension-runtime.md](references/extension-runtime.md)
- Common project, schematic, PCB, library, or DRC calls:
  [api-patterns.md](references/api-patterns.md)
- API discovery: [API index](references/_index.md), then the exact class,
  enum, interface, or type file; use [_quick-reference.md](references/_quick-reference.md)
  only to locate a candidate method.
- Source-format analysis or generation: [format/index.md](format/index.md), then
  the applicable `format/project`, `format/schematic`, or `format/pcb` files.

## Step 1: Fix The API Contract

Identify the API domain (`DMT`, `SCH`, `PCB`, `LIB`, or `SYS`), target project and
document, read/write authorization, expected return value, and whether the task
needs live execution, extension code, or source-format work.

**Complete when:** one branch and one target context are selected, ordinary
design work has been routed to `easyeda-agent`, and the expected observable
result is stated.

## Step 2: Verify Runtime Context

For live execution, verify the bridge identity and EasyEDA connection, list
connected windows, select the exact window when more than one exists, and read
the current project/document state.

**Complete when:** health reports `service: "easyeda-bridge"`, one intended
window is selected, and its active document type matches the planned API domain.

## Step 3: Resolve The Exact API

Read the complete class method entry, including parameters, return type,
remarks, enum values, interfaces, units, and document-state requirements.
Treat the published references as the source of truth.

**Complete when:** every call has a documented method, exact signature, explicit
enum/interface values, known units, and a defined success or failure result.

## Step 4: Execute A Minimal Observable Call

Start with a read call that proves the selected project/document. Execute the
smallest authorized mutation or extension behavior, `await` each Promise, return
the result, and read back changed state before expanding the batch.

**Complete when:** the bridge returns a matched result, the target state reads
back as expected, and unrelated documents or primitives are unchanged.

## Step 5: Close Failures By Evidence

Classify a failure as connection/window, document state, signature/type,
permission, runtime-context, or unsupported API. Re-read the relevant reference
before changing code. Use an `eda.sys_*` alternative when an extension runtime
forbids a browser API.

**Complete when:** the call succeeds, or the exact failing category and next
supported action are identified without inventing an undocumented API.

## Step 6: Deliver

Report the selected window/project/document, references consulted, code or
source files changed, calls executed, returned results, readback evidence, and
remaining permission or API limitations.

**Complete when:** every requested behavior has a reproducible API path and
evidence, or a documented limitation with no unsupported completion claim.

## Execution Contract

- Run bridge code inside `async function (eda) { ... }` and use `return` for the
  captured result.
- `await` every `Promise`-returning API.
- Use documented enum members and interfaces instead of guessed numeric values.
- Verify active document type before calling `SCH_*` or `PCB_*` APIs.
- Keep units explicit: PCB coordinates use 1 mil; schematic coordinates use
  0.01 inch (10 mil).
- Treat the extension main process as an EasyEDA API runtime, not a general DOM
  or Node.js environment; follow [extension-runtime.md](references/extension-runtime.md).
