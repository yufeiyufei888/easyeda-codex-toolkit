# PCB Quality

Apply this reference to every PCB creation, edit, or review.

## Context And Placement

- Read the board linkage, parts, pads, nets, layers, stackup, outline, keep-outs,
  live DRC rules, and mechanical constraints before placement or routing.
- Place fixed connectors, mounting holes, panel controls, antennas, and other
  enclosure datums first. Verify protrusion, travel, height, tool access, and
  service orientation.
- Assign top/bottom side roles deliberately. Keep user-facing controls and
  labels on the service side; use the opposite side when shorter critical paths
  justify two-sided assembly and inspection remains practical.
- Place by current and signal flow. Use orthogonal rotation by default; accept a
  non-orthogonal IC rotation when measured topology reduces crossings, length,
  congestion, or layer changes without sacrificing courtyard, polarity,
  assembly, or silkscreen clarity.
- Place accessible test points for power, ground, raw inputs, reference nodes,
  interstage signals, and outputs as the product's test strategy requires.

## Power, Return, Signal, And Thermal Paths

- Preserve one continuous ground reference by default. Carry every intentional
  ground-domain bridge from the schematic into the exact PCB element, location,
  copper ownership, and return path.
- Judge decoupling by the full IC-pin -> capacitor -> ground/plane loop. On two
  layers, keep the loop short with close copper and vias; on four or more layers,
  minimize pad-to-via-to-plane inductance and reserve via escape room.
- Keep switching-converter input hot loops compact, switching-node copper small,
  and sensitive circuits outside the noisy current path.
- Size power copper, necks, vias, and thermal structures from current, copper
  thickness, temperature rise, voltage drop, and fabrication capability.
- Use GND stitching vias where they close a real return path: beside signal
  layer transitions, shields/connectors, RF containment, and board edges. Judge
  connectivity and plane continuity rather than raw via count.
- Give RF antennas an edge-appropriate position and electrical keep-out on every
  copper layer. Keep matching networks and their ground returns compact.
- For each differential pair, record lengths and intra-pair skew, maintain one
  continuous reference plane, minimize unmatched stubs and layer changes, and
  add nearby return vias at unavoidable transitions. Use the exact interface
  and fabrication constraints from primary documentation.

## Routing, Silkscreen, And Fabrication

- Define net classes before routing so width, clearance, via, and length choices
  are auditable. Prefer planes or pours for power and ground where appropriate.
- Establish board outline, keep-outs, component placement, and critical
  silkscreen before routing. Put connector labels beside the actual pads and
  make bottom labels readable in a physically correct bottom view.
- Distinguish intentional connector-body overhang from copper outside the board.
  Keep pads and required copper manufacturable for the selected edge process.
- Use live project DRC rules as the primary constraint source; use bundled JLC
  rules only as a fallback or clamp.

## Verification Gate

Use the evidence ladder from the parent skill:

1. Read back schematic linkage, placement side, bboxes/courtyards, pads, nets,
   tracks, vias, layers, planes, pours, keep-outs, outline, and rule assignments.
2. Make overlap checks side-aware. Inspect the bottom only after a physical flip
   or correct mirror; use 3D/top/side/bottom views when mechanics or height matter.
3. Inspect critical current paths, return paths, diff pairs, RF, decoupling,
   copper-to-edge, thermal structures, and assembly/service access.
4. After every authorized change affecting copper or geometry, rebuild all
   affected pours, run native DRC, then `check`/`layout-lint`, then visual QA.
   Repeat this loop after any repair.
5. Classify dangling ends, acute angles, free-angle segments, track-over-pad,
   flipped silkscreen, overlapping/single-layer vias, duplicate segments,
   outside-outline items, antenna keep-out, and netless-pour findings using
   physical side, net data, geometry, mechanical intent, and native DRC.

**Complete when:** every component and critical net is placed/routed or explicitly
accounted for, the final copper is current, native DRC is clean or every exception
is documented, all secondary findings are classified, and physical views match
the intended assembly.
