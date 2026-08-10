# Read-Only Project Audit

Use this branch when the user asks to learn, inspect, compare, or review an
existing EasyEDA project without authorizing design changes.

## Steps

1. Confirm the exact project, schematic pages, and PCB documents in scope.
   Operate only inside that set.
2. Connect and read the schematic first. Recover function blocks, power and
   signal flow, part/pin/net connectivity, calculations, presentation, and
   current native check evidence.
3. Read the linked PCB second. Compare placement, routing, planes, returns,
   mechanics, silkscreen, and both physical sides against the schematic intent.
4. Use view switching, readable zoom, physical flip, 3D, data readback, and
   documented read-only checks. Preserve project content: no save, import,
   update, auto-fix, move, repour, rebuild, or rules change.
5. Classify each observation as confirmed defect, intentional/project-specific,
   checker limitation, or unresolved because proof would require mutation.
6. Extract only transferable rules into skills. Keep project-specific geometry,
   values, and exceptions in the audit report unless they define a reusable gate.

## Completion Criterion

The audit is complete when the schematic and PCB have both been inspected in
order, every reported issue has evidence and a classification, useful patterns
are separated from project-specific choices, missing mutation-only gates are
stated, and the final report explicitly confirms that project content remained
unchanged.
