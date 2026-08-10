# Development Board Patterns

Use this reference for MCU/SoC development boards, dense breakouts, USB
interfaces, external high-speed memories, SiP devices, and RF-enabled modules.

## Schematic

- Maintain one traceable mapping from device pin/ball -> schematic net -> onboard
  consumer and connector -> PCB pad and silkscreen -> firmware mux. Classify
  every simultaneous-use conflict and keep physical connector order visible.
  Record each IO's electrical class, voltage tolerance, pull-up rail, required
  series element, and applicable errata condition.
- Check the latest errata for the exact silicon revision before accepting a
  vendor reference circuit. Maintain an errata constraint table with affected
  revisions, pins or blocks, trigger conditions, schematic/PCB/firmware
  mitigation, and verification evidence; apply newer guidance only within its
  stated scope.
- Use semantic names that remain consistent with firmware and test notes; append
  the MCU pin where it materially speeds review.
- Draw complete interface topology. For USB Type-C, verify both CC pins, device
  role, pull resistors, D+/D-, shield, ESD, and series damping against the exact
  controller. For a hub/bridge, show upstream and every downstream channel,
  preserve pair identity, and mark unused ports NC.
- Classify memory topology before applying routing rules. For SiP or in-package
  memory, do not invent an external bus or board-level length-matching
  requirement; still verify every memory rail, VREF, calibration/ZQ/ZN network,
  decoupling, and startup dependency. Apply full bus-topology and matching checks
  only to external memory.
- Derive crystal capacitors from the exact crystal load specification and board
  parasitics. Document the intended state of backup or optional power domains.
- For a multi-rail SoC, build a rail-domain table covering pin group, source,
  voltage, enable path, default state, decoupling, and test access. Express the
  required startup order as a dependency graph and trace every PMU, translator,
  and load-switch enable.
- For boot and mode straps, record the sampled phase, default and override
  levels, resistor state, and resulting mode in a truth table.
- Maintain a programming and recovery matrix for normal boot, SWD/JTAG,
  UART/USB bootloader entry, reset, strap state, target power, and competing
  masters. Every supported state needs a deterministic entry and rescue path.
- For a core board plus carrier or accessory, define an interface contract for
  every mating state: physical orientation transform, pad order, direction,
  voltage, source/load ownership, current budget, default level, pulls,
  isolation, and backfeed risk. Verify the mapped pins after mirror/rotation;
  equal pin numbers alone are not evidence of a correct mating connection.
- Build a protection-coverage table for every external interface. Record the
  entry-side protection part, protected signal or rail, working/clamp voltage,
  parasitic capacitance, pulse rating, and short return path; do not generalize
  one protected USB port to the rest of the headers.
- Treat schematic-to-PCB synchronization as an independent gate. Designators,
  footprints, pad numbers, and nets must agree; an electrically equivalent PCB
  with renamed parts still fails traceability, assembly, and future import
  safety.
- When authoritative sources differ, preserve their scope and terminology, such
  as nominal versus effective performance or silicon versus board limits,
  instead of collapsing them into one apparently corrected value.
- Use a separate documentation page when licensing, revision policy, or usage
  notes would crowd the electrical page. Match title, revision, page count, and
  page-size metadata to the actual sheet.

## PCB

- Treat long header rows, castellated edges, USB connectors, buttons, and
  antennas as mechanical and electrical anchors. Preserve pitch, pin 1,
  numbering, protrusion, and the schematic breakout order.
- Place the MCU near the routing center unless mechanics, RF access, or a lower
  crossing topology justifies another position. Record why a diagonal rotation
  or other non-orthogonal exception improves the measured fanout.
- Place external high-speed memory beneath its controller only when
  pad-to-via-to-pad routing shortens the bus and keeps a continuous reference
  plane. Verify escape routing, returns, thermal interaction, probe access,
  courtyard, and two-sided assembly cost.
- On four layers, keep an uninterrupted GND reference adjacent to the dominant
  critical signal layer whenever practical. Use power planes for distribution,
  not as a substitute for the return reference.
- Place RF antennas at the required edge with all-layer keep-out and a compact
  matching/ground network. Use stitching vias for real return/containment paths.
- Quantify each high-speed pair with routed length, intra-pair skew, via count
  against any documented budget, reference-plane continuity, and return-via
  placement. Record electrical limits from primary interface or silicon
  documentation, but derive trace geometry from the actual fabrication stackup
  rather than another board.
- Verify top, physically flipped bottom, side, and 3D views. Interpret projected
  top/bottom overlap and intentional edge-body overhang with side and mechanical
  evidence before classifying a defect.
- Inspect the assembled module stack, not only each bare board: connector
  insertion direction, standoff height, underside clearance, control and debug
  access, cable bend space, and power-source interaction must all pass.

## Completion Criterion

The pattern is closed when the complete device-to-consumer/connector mapping and
schematic-to-PCB identity are verified; applicable errata, every power domain,
enable chain, boot/recovery state, and module mating state are accounted for;
each memory topology is treated correctly; every external protection and
high-speed/RF path has explicit evidence; and the bare-board plus assembled-stack
mechanics, labels, and access are correct in their physical viewing orientation.
