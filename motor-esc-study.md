# Module 1 — Motor and ESC, from schematics to our own hardware

## Starting position and goal

2026-10-15: learner has no motor, ESC, battery, supply, or tools. Start from schematics, theory, and calculations. End goal: design, assemble, test, and eventually manufacture our own motor-control products. No purchase is approved or needed for this first study.

First milestone: explain and calculate the behavior of one three-phase motor-drive channel. A full quadcopter, radio, and flight controller are not required to understand or bench-control one motor. Later, a small MCU can generate a compatible command signal, with startup/arming behavior verified against the firmware.

## Reference baseline

OpenDrone-hw/OpenESC-30x30 commit bf306934b5decc130ab1df6b653563ea16165e8e.

- Architecture notes: https://github.com/OpenDrone-hw/OpenESC-30x30/blob/bf306934b5decc130ab1df6b653563ea16165e8e/AGENTS.md
- One-channel schematic: https://github.com/OpenDrone-hw/OpenESC-30x30/blob/bf306934b5decc130ab1df6b653563ea16165e8e/hardware/ESC.kicad_sch
- Shared circuitry: hardware/4in1.kicad_sch at the same commit.

The notes describe four channels with AT32F421G8U7 MCUs, NSG2065Q drivers, and six SP40N01GHNK MOSFETs per channel. The channel schematic was retrieved and these part values identified. This is not a net-by-net audit or validation. Shared power, sensing, PCB-only capacitors, firmware, and layout must also be reviewed. Do not manufacture from the channel sheet alone. Component alternatives remain unapproved.

## Prerequisites, learned alongside the circuit

| Topic | What we will learn | Why it matters |
|---|---|---|
| Arithmetic and units | ratios, scientific notation, unit conversion | prevent voltage/current/speed mistakes |
| Circuits | Ohm's law, Kirchhoff's laws, power, capacitors, inductors | trace supply and switching current |
| Magnetism | current-generated fields, force, flux linkage, induction | explain torque and back-EMF |
| Mechanics | torque, inertia, angular speed, acceleration, load | explain startup and speed changes |
| Mathematics | graphs, sine waves, derivatives, simple differential equations | model time-dependent current and motion |
| Power devices | MOSFETs, gate charge, body diodes, half-bridges | understand how the motor receives power |
| Embedded systems | GPIO, timers/PWM, interrupts, ADC/comparators, flashing | implement commutation and sensing |
| Measurement | voltage reference, probing, current/RPM/temperature measurement | distinguish evidence from assumptions |
| Materials | copper, insulation, magnets, steel laminations, adhesives | eventual motor manufacture and thermal limits |
| Battery chemistry | voltage limits, energy, internal resistance, charging | later power-source selection and operation |

Chemistry enters when materials or batteries require it; it is not a prerequisite course to finish before studying rotation.

## Lesson 1 — Why a brushless motor needs switching

The stator is stationary and contains windings; the rotor rotates and carries permanent magnets in the usual drone outrunner. Current in windings creates a magnetic field. The interaction with the rotor field produces torque. The drive must keep changing the excitation as the rotor turns so useful torque continues.

A fixed DC connection to a pair of phases does not produce continuous controlled rotation: the rotor may move toward an alignment and then stall while current heats the winding. The ESC electronically performs commutation. The battery supplies DC, while the motor phases see time-varying switched voltages and currents.

Six power MOSFETs form three half-bridges. Each phase can be connected toward the positive supply or ground through controlled switches. Never turn on both switches in the same leg together; that creates shoot-through. Winding current does not instantly stop when a MOSFET turns off; its recirculation path matters.

For idealized six-step commutation, one illustrative sequence is A+ B-, A+ C-, B+ C-, B+ A-, C+ A-, C+ B-. The third phase is undriven in this simplified model. These are logical states, not firmware pin commands or a ready-to-energize procedure. Actual PWM, dead time, freewheeling, and sensing must follow the selected driver and firmware implementation.

## The first mathematical model

For a simplified winding model:

v = R i + L di/dt + e

v: winding voltage; R: resistance; i: current; L: inductance; e: induced back-EMF. This is an introductory model, not a complete coupled three-phase model.

For consistent motor-constant conventions:

e = Ke * omega; torque approximately = Kt * i

J d(omega)/dt = motor torque - load torque - friction torque

Ke and Kt depend on voltage/current conventions; line/phase and peak/RMS definitions must be checked before using datasheet numbers. omega is mechanical rad/s. This explains why applying a duty command is not the same as holding a precise RPM: supply and load change the operating point. Accurate speed regulation needs measured/estimated speed and a speed-control loop.

P_electrical = V * I; P_mechanical = torque * omega; copper loss = I_rms squared * R.

Example: 12 V at 2 A is 24 W electrical input. If total losses were 6 W, mechanical output would be 18 W. This is an invented arithmetic example, not a motor rating or measured efficiency.

PWM duty = on-time / switching period. With an ideal single-leg simplification, average output voltage is duty * DC-bus voltage; the actual motor phase-to-phase waveform depends on which legs switch. PWM frequency, commutation frequency, and mechanical RPM are distinct.

Electrical frequency = pole pairs * mechanical RPM / 60.

Example: 14 magnetic poles means 7 pole pairs. At 6000 mechanical RPM, electrical frequency is 700 Hz. Conventional six-step operation makes 4200 commutation transitions per second. These numbers are illustrative and do not select a motor.

Sensorless back-EMF commutation has a startup problem: at standstill there is no rotation-generated back-EMF. Startup needs a suitable method before normal back-EMF tracking. We will examine the actual AM32 implementation rather than inventing timing values.

## Learning and build sequence

1. Draw rotor/stator, identify phases, explain torque and induction; complete the examples above.
2. Learn half-bridge current paths and inspect one power stage in the reference schematic.
3. Trace gate driver, supply rails, bootstrap/drive arrangement, sensing, and MCU pins against exact datasheets. Resolve net names and hierarchy, not just component labels.
4. Study commutation, PWM, startup, back-EMF detection, timing, and loss calculations.
5. Match the exact MCU, pin map, bootloader, and firmware target. Study command-to-output code paths.
6. Define a modest first prototype's voltage/current/speed requirements, then evaluate India sourcing and alternatives. Do not inherit the upstream maximum ratings as our design requirements.
7. Simulate relevant circuits, design the single-channel prototype, review layout and manufacturability, define test limits, then order parts/PCBs.
8. Bring up supplies and gate signals in stages. Only then connect a restrained propeller-free motor with appropriate current limiting and measurements. A normal grounded scope clip must not be attached to an arbitrary switching node.
9. Validate loaded operation on a suitable fixture, losses, temperature, transients, startup reliability, and faults. Expand to four channels after evidence supports it.

## Equipment by phase

Now: computer, schematic viewer/KiCad, datasheets, calculations, and source control.

Before powered custom-board work: multimeter, current-limited supply selected for the prototype, suitable soldering/assembly capability, microscope as packages require, supported programmer/debugger, and an oscilloscope/probes suitable for switching measurements. RPM and temperature measurement are needed for characterization. Exact models and costs are not chosen.

## Manufacturing scope

Designing and assembling our ESC PCB and maintaining firmware is one achievable manufacturing scope. Making the motor adds magnetic design, winding, laminations, rotor balance, bearings, insulation, adhesives, tooling, and quality control. Fabricating semiconductor chips is a separate industrial undertaking. We will document and reduce dependencies through open designs, approved alternatives, and reproducible tests; purchased raw materials and ICs remain part of the supply chain.

## First understanding checkpoint

Explain: Why does fixed DC not keep the rotor turning? Why are three half-bridges used? Why does winding current continue after a switch opens? Why can two equal throttle commands produce different RPM? Which numbers in this lesson are illustrative rather than specifications?

No learner understanding is marked complete until discussed. No hardware experiment has occurred.

## Primary theory references

- Microchip AN885, BLDC Motor Fundamentals: https://ww1.microchip.com/downloads/en/Appnotes/00885a.pdf
- TI, six-step operation and back-EMF at standstill: https://www.ti.com/document-viewer/lit/html/SSZTBP2/GUID-E16F6FD4-B74F-4AB0-990E-C89D493A2398
- Microchip sensorless drive and mechanical/electrical speed: https://ww1.microchip.com/downloads/en/Appnotes/AN3998-Sensorless-BLDC-MC-AVR-MCU-Fam-DS00003998.pdf
- TI gate drive: https://www.ti.com/lit/pdf/slva714
