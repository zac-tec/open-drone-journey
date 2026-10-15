# KiCad walkthrough — original OpenESC design

## Reference files

Hardware repository: https://github.com/OpenDrone-hw/OpenESC-30x30
Pinned commit: bf306934b5decc130ab1df6b653563ea16165e8e
Pinned shared library: fdf8319b3512925a7566532ae4b38a298cf54c24

- Open hardware/4in1.kicad_pro in the KiCad project manager.
- Open hardware/4in1.kicad_sch for shared power, current measurement, connectors, and four motor-channel instances.
- Enter a motor-channel hierarchical sheet to study hardware/ESC.kicad_sch in context.
- hardware/4in1.kicad_pcb is the physical implementation, not a separate electrical design.

The original checkout is a study baseline. Do not save circuit edits, update PCB from schematic, or refresh pinned libraries while merely exploring. The upstream notes warn that some bulk capacitors exist only on the PCB.

## Walkthrough order

1. Find battery positive and ground. Distinguish high-current propulsion power from regulated driver and MCU supplies.
2. Identify one motor channel and its MCU, gate driver, and six power MOSFETs.
3. Find a high/low MOSFET pair sharing one phase node. Trace the supply-to-phase and phase-to-ground paths.
4. Follow gate-driver outputs to gate resistors and MOSFET gates. Match driver pin functions to its exact datasheet.
5. Follow motor-phase feedback toward the MCU; explain scaling and rotor-position sensing only after reading the actual network.
6. Trace DShot command input to the MCU and compare against the selected firmware pin definitions.
7. Return to the root sheet: locate shared current sensing and power conversion. Do not assume board-current measurement equals per-motor current.
8. Later compare schematic nets with physical copper, current loops, decoupling, and thermal paths on the PCB.

## Reading discipline

A net label connects matching nets according to KiCad hierarchy; an apparent visual gap does not prove disconnection. A wire crossing needs its connection semantics checked. Symbol pin numbers, physical package pin numbers, and MCU GPIO names must be matched carefully. An unused pin marker is not a ground connection.

Questions will be recorded as questions until checked against nets, component datasheets, and firmware. No hardware operation or manufacturability validation follows merely from opening the project.

## Session outcome — 2026-10-15

KiCad 10.0.6 launched from the official mounted disk image; full installation was not completed because the application is about 4.8 GB and free disk space was insufficient. Verified downloaded DMG SHA-256 against GitHub release digest: ef4dcd4278c46d3efcd28c8db273d5957d68efda028f6bf79b4811fc5302dc68.

Opened 4in1.kicad_pro, launched its Schematic Editor, and entered ESC1. Visually confirmed MCU U2, driver U4, BEMF feedback block, and three half-bridges. Phase A uses Q1/Q2 with gate resistors R76/R80 marked 15R in this sheet instance; GHA/GLA label the gate-drive nets, MotorA is the switch node, and A is the motor output sheet connection. These identifiers are specific to the displayed hierarchical instance. No circuit edits made.
