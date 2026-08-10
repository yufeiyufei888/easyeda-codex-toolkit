# NE555 Patterns

Use this reference for NE555 schematic design, contest tasks, and review.

- Verify the exact NE555 variant, package pinout, supply range, output behavior,
  thresholds, discharge transistor behavior, and timing equations from the
  manufacturer datasheet.
- Place about 100 nF directly between pin 8 (`VCC`) and pin 1 (`GND`) for local
  supply decoupling unless the selected datasheet specifies another network.
- When control-voltage pin 5 is otherwise unused, connect about 10 nF from pin 5
  to ground unless the application or datasheet requires another value. This pin
  is connected, not NC; mark every truly unused pin explicitly NC.
- Derive charge/discharge paths, thresholds, pulse width, high/low intervals,
  frequency, duty cycle, polarity, and expected waveform from the exact circuit.
  Recalculate with final values and explicit units; check tolerance bounds when
  the task has a narrow acceptance range.
- Put independent contest tasks on separate pages. Keep each NE555, timing
  network, output stage, supply/ground symbols, formulas, expected values, and
  waveform notes readable without wire or text overlap.

**Complete when:** pin mapping and every timing path are datasheet-backed, local
decoupling and pin 5 treatment are explicit, calculated nominal/tolerance values
meet the task, every pin is connected or NC, and the rendered page matches the
authoritative net data.
