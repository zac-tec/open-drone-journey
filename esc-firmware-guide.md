# OpenDrone ESC firmware — source study guide

Reviewed 2026-10-15. This is source inspection, not a compiled or tested firmware release.

## Reference identity

- Repository: https://github.com/OpenDrone-hw/AM32
- Default branch observed: main, commit 2738df3240baa5bd4295b460cf0c5cfe0bd49d97.
- Hardware-specific branch inspected: feat/openesc-20-target.
- Pinned study commit: 5f8978eeb618c14bb396af7ac049d2a5e7b5a508.
- Target preprocessor definition found: OPENESC_20_F421.
- Upstream AM32: https://github.com/am32-firmware/AM32 . This is an OpenDrone fork of an existing firmware project, not entirely original firmware written by OpenDrone.

Previously pinned hardware was OpenESC-30x30 commit bf306934b5decc130ab1df6b653563ea16165e8e. The explicit target inspected here names the 20x20 board. We have NOT established interchangeability with the 30x30 board or our eventual single-channel derivative. Hardware/firmware baseline alignment is an open task; do not flash by name similarity.

## Three separate deliverables

1. Source code: editable C, headers, startup and build files.
2. Built application: binary/HEX generated for a specific MCU, pin map, memory layout, and options.
3. Bootloader: separate initial firmware enabling later application updates. The README says a blank ESC requires an appropriate bootloader matched to MCU and input pin. Exact memory layout and programming procedure need validation before use.

The pinned README describes supported MCU families including AT32F421 and links to AM32-bootloader. It describes Keil builds and update/configuration routes. A Makefile also exists; toolchain setup, target enumeration, linker files, and a reproducible build remain unverified. No build or flash command is approved by this note.

## Source map (links pinned to the inspected commit)

Base: https://github.com/OpenDrone-hw/AM32/blob/5f8978eeb618c14bb396af7ac049d2a5e7b5a508/

| File | Evidence inspected | Learning purpose |
|---|---|---|
| Inc/targets.h, lines 699–707 | OPENESC_20_F421, hardware groups, DEAD_TIME 60 | Translate selected board into compile-time configuration |
| Inc/targets.h, lines 4638 onward | HARDWARE_GROUP_AT_B: PB4 command input, timer/DMA selection, phase-control GPIOs | Match firmware pins to schematic |
| Inc/targets.h, lines 4850 onward | HARDWARE_GROUP_AT_045 comparator selection | Match phase feedback mapping |
| Src/dshot.c, computeDshotDMA(), line 72 onward | DMA edge differences, bit classification, checksum comparison, command extraction | Convert wire timing into an input value |
| Src/main.c, processDshot(), line 1563 onward | Dispatches frame processing/telemetry work and calls setInput() | Understand scheduling and input handling |
| Src/main.c, setInput(), line 975 onward | Input interpretation, mode handling, startup/duty pathways | Understand how commands become motor demand |
| Src/main.c, commutate(), line 860 onward | Six-step state progression, comStep(step), comparator input update | Connect rotor timing to phase selection |
| Src/main.c, PeriodElapsedCallback(), line 908 onward | Timer callback, commutation timing/advance bookkeeping | Understand timed commutation |
| Src/main.c, around line 1545 | SET_DUTY_CYCLE_ALL(adjusted_duty_cycle) | Trace final PWM update into MCU-specific definitions next |
| Makefile | Build structure and target generation exist | Reproduce only the selected target after toolchain review |

These are landmarks, not a complete linear call graph. Processing is spread across loops, timers, DMA, and interrupts. The exact capture producer, comStep implementation, low-level PWM macros, and comparator interrupt path still need tracing.

## What the code says about DShot

computeDshotDMA() measures differences between captured edge timestamps, classifies 16 bits, calculates a check value, and compares it with the received check bits. It reconstructs an 11-bit value. In the normal input path, a value greater than 47 updates newinput only when EDT_ARMED permits it. Special commands and zero input follow separate branches; programming mode can change interpretation.

This is why “send throttle and it spins” is incomplete. Firmware state, arming, modes, initialization, and safety behavior also matter. A checksum check is data-integrity logic, not authentication or proof of safe motor output.

## Concrete target findings

OPENESC_20_F421 enables HARDWARE_GROUP_AT_B and HARDWARE_GROUP_AT_045. In the inspected definitions, command input is PB4. Phase-control GPIO definitions are A-high PA10/A-low PB1, B-high PA9/B-low PB0, C-high PA8/C-low PA7. Comparator selection comments map phase feedback to PA0, PA4, PA5.

These are source definitions, not verified board net assignments. Driver polarity, timer configuration, physical pin numbering, analog networks, and package must be reconciled with the actual schematic.

DEAD_TIME 60 is a firmware constant. Do not call it 60 microseconds or 60 nanoseconds: actual hardware timing requires tracing how the MCU timer uses it and its clock/encoding.

## Study sequence

1. Understand one winding, torque, induction, and current continuity.
2. Draw the three half-bridges and their current paths.
3. Match target GPIO definitions to driver and sensing nets.
4. Trace DShot input capture, decoding, invalid frames, and loss-of-signal behavior.
5. Trace arming, startup, duty limits, and normal commutation separately.
6. Trace back-EMF comparator selection, timing, and desynchronization recovery.
7. Review bootloader, linker layout, build options, compiler versions, and output artifacts.
8. Reproduce a build without changing behavior, then design a hardware test sequence before energizing a motor.
9. Only after a working reference is understood, design a derivative and validate every hardware-dependent change.

## Independence and product work

Open source enables inspection, modification, and reproducibility; it does not eliminate all suppliers or validation work. Preserve AM32 attribution and its GPL-3.0 license requirements when distributing firmware; review the actual license text before product distribution. Hardware licensing is separate. Component alternatives in India can change gate polarity, drive strength, sensing ratios, timing, and thermal behavior, so they must be evaluated against hardware AND firmware.

## Outstanding evidence

No target build, binary identification, bootloader compatibility verification, 30x30 target equivalence, schematic net audit, hardware measurement, or motor test completed. README claims, code observations, and future test outcomes must remain separate.
