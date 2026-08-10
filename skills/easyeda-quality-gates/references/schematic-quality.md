# Schematic Quality

Apply this reference to every schematic creation, edit, or review.

## Parts And Electrical Intent

- Use an exact EasyEDA/JLC library device with footprint and BOM linkage when a
  suitable part exists. Prefer verified LCSC C-numbers and the workspace
  `standard-parts.json`; record newly verified selections there when authorized.
- Verify symbol pin numbers, package mapping, polarity, transistor pin order,
  power domains, and required support circuitry against the exact datasheet.
- Build a power-pin-to-decoupling coverage map. Place ordinary local ceramics
  near the pins they serve and apply datasheet-specific values or filters to
  analog, RF, core, reference, and high-transient domains.
- Mark every electrically unused pin with an NC marker. Represent optional or
  unpopulated components with a distinct DNP/assembly convention.
- Name rails by meaning: use `VCC` or `BAT` for raw/unspecified inputs and an
  explicit voltage such as `+5V`, `+3V3`, or `+12V` after regulation. Give one
  continuous rail one name.

## Page And Module Presentation

- Plan in the hierarchy page -> functional zone -> repeated submodule -> part.
  Put electrically independent tasks on separate pages and divide integrated
  pages by real electrical function.
- Keep a continuous aligned zone grid on dense pages. Place headings at one
  consistent edge outside wiring channels; let a dominant function span cells
  rather than fragmenting it to satisfy a visual grid.
- Place inputs left, outputs right, positive supplies above, and ground below
  when symbol orientation permits. Keep support parts beside the served pins.
- Derive repeated channels from one reviewed template. Keep ordering, values,
  orientation, spacing, naming, and annotation consistent unless signal flow
  justifies a deliberate mirror.
- Keep the drawing within the sheet and title-block keep-out. Keep equations,
  functional notes, values, designators, symbols, wires, and junction dots
  visually separate.
- Name each section by its implemented electrical function. Keep annotations
  concise and associate them unambiguously with the relevant block.

## Connectivity

- Use short visible orthogonal wires inside a module and semantic net labels for
  cross-zone or cross-page connections.
- Give every connection a non-zero wire. Insert a visible wire between adjacent
  component pins instead of relying on direct pin contact.
- Put power and ground symbols on short stubs with their bodies pointing away
  from the circuit. Reserve flags for power rails and justified long-distance
  ports.
- Chain multi-pin nets through anchored segments. Route each segment through an
  empty channel so it cannot touch an unrelated pin or symbol body.
- Keep one naming convention across schematic, PCB, firmware notes, connectors,
  test points, and silkscreen. Choose names that remain true in every operating
  state.

## Theory And Calculations

- Derive thresholds, timing, frequency, duty cycle, transfer functions, expected
  waveforms, current, and thermal assumptions from primary documentation.
- Calculate with the final schematic values and explicit units. State supply,
  initial state, polarity, charge/discharge path, tolerance assumptions, and the
  event that defines each interval.
- Cross-check related quantities independently, such as `T = 1/f`,
  `T = T_HIGH + T_LOW`, and duty cycle from both interval and component-value
  equations. Evaluate tolerance bounds when the acceptance margin is narrow.
- Put concise verified formulas and expected values beside the stage they
  describe without entering a wiring channel.

## Verification Gate

Use the evidence ladder from the parent skill:

1. Read back parts, pins, wires, flags, labels, NC markers, nets, sheet geometry,
   page number/count, title, revision, and title-block page size.
2. Check floating pins, dangling ends, zero-length wires, flag-on-pin,
   pin-to-pin contact, wire-over-pin, crossings, multi-net wires, marker
   mismatches, bbox overlap, title-block collisions, and decoupling coverage.
3. Recalculate documented values from the final component values.
4. Run current-document DRC/check/lint and classify every finding against the
   authoritative netlist and primitive geometry.
5. Inspect every module at readable zoom for overlaps, symbol orientation,
   junction ambiguity, unnecessary crossings, inconsistent repeated geometry,
   and text readability.

**Complete when:** every pin and named requirement is accounted for, every
calculation is reproducible, every automated finding is classified, and the
rendered page communicates the same connectivity as the design data.
