# Contest Control Board Patterns

Use this reference for dense intelligent-vehicle and other contest mainboards.
Treat chassis geometry and proven project-specific circuits as constraints that
still require evidence; generalize only the review gate.

## Schematic

- Split pages by controller/power, camera or sensor acquisition, and motor or
  actuator drivers. Keep cross-page power and signal interfaces explicit.
- Use aligned functional zones and derive repeated driver channels from one
  reviewed template. Preserve channel order, conditioning, values, naming, and
  connector mapping; mirror only for a clear signal-flow benefit.
- Name buffer, isolation, level shifting, and conditioning stages by their actual
  electrical function. Record supply, enable, default input states, and unused
  channels.
- Keep raw battery, regulated rails, camera power, and noisy/sensitive returns
  semantically distinct. Give every intentional ground-domain relationship one
  documented schematic-to-PCB connection strategy.
- Build decoupling coverage for controllers, camera/FIFO devices, logic, buffers,
  and gate drivers from their exact datasheets.
- Treat a repeatedly built and measured circuit as project evidence. Before
  changing an unusual driver topology, verify the exact part revision, pin map,
  datasheet conditions, and measured behavior.

## PCB

- Group by current and signal flow: controller near the routing center, camera
  interfaces together, conversion near power entry, and each driver beside its
  switches, local capacitors, and load connector.
- Keep repeated power channels geometrically comparable so gate loops, current
  paths, thermal spreading, silkscreen, and fault measurements can be audited.
- Size battery, bridge, and motor-phase copper plus via arrays from current,
  copper thickness, temperature rise, voltage drop, and fabrication limits.
- Preserve a continuous reference plane where practical. When the design uses a
  0 ohm ground bridge, place it at the documented transfer boundary with short,
  broad copper and the required vias; record any intentional bottom-side
  assembly exception.
- Define net classes for logic, camera bus/clocks, gate drive, regulated power,
  battery, and motor phases before routing.
- Treat stitching and thermal via arrays as electrical structures. Verify net,
  connected layers, pour ownership, antipads, and current/return purpose before
  classifying automated via warnings.
- Preserve the competition/chassis outline, mounting datums, keep-outs,
  copper-to-edge clearance, connector access, switch travel, daughterboard
  height, and support strategy. Verify top, side, 3D, and physical bottom views.

## Completion Criterion

The pattern is closed when every repeated channel maps consistently from
schematic to PCB, high-current and return structures have calculated evidence,
unusual proven circuits are verified against their exact device and measurements,
mechanical constraints are satisfied, and every checker finding is classified
against net data and the correct physical view.
