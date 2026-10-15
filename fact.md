# Technical facts

This file contains current technical knowledge, not historical anecdotes or untested design promises. Established principles, documentation claims, and our measurements have different evidence levels.

## Entry format

ID; claim; scope/conditions; source and section or timestamp; hardware/firmware revision; evidence status; checked date; limitations; related experiment/decision. Statuses: sourced, measured, hypothesis, disputed, superseded. “Sourced” does not mean independently measured by us. Video claims remain source claims until checked. Never silently remove a disproven claim: mark it superseded and link the correction.

## Initial entries — checked 2026-10-15

### F-001 — Roles of radio protocols
Claim: UART-based ExpressLRS receivers commonly communicate with the FC using CRSF. ExpressLRS and CRSF refer to different layers of this connection.
Scope: UART receivers; not a statement about every receiver architecture.
Source: https://www.expresslrs.org/quick-start/receivers/wiring-up/
Evidence: sourced; no project measurement.

### F-002 — UART signal wiring
Claim: The receiver's TX supplies control data to the FC's RX; the receiver's RX accepts telemetry from the FC's TX. Check the board's actual labels, voltage requirements, and interface implementation.
Source: https://www.expresslrs.org/quick-start/receivers/wiring-up/
Evidence: sourced; hardware not selected.

### F-003 — Bidirectional DShot
Claim: Compatible ESCs can send RPM telemetry back on the motor-command signal wire. Motor pole count is used to interpret electrical RPM as mechanical RPM.
Source: https://betaflight.com/docs/wiki/guides/current/DSHOT-RPM-Filtering
Evidence: sourced; requires compatible firmware and configuration.

### F-004 — RPM filters
Claim: Motor RPM telemetry can position notch filters to attenuate motor-related vibration. Four motors, three harmonics, and three axes give 36 individual notches in the documented example; this is not a universal fixed configuration.
Source: https://betaflight.com/docs/wiki/guides/current/DSHOT-RPM-Filtering
Evidence: sourced; exact pipeline depends on firmware revision/settings.

### F-005 — Firmware targets
Claim: ExpressLRS distinguishes hardware-specific targets from generic targets intended for DIY/pre-production designs. Hardware and firmware configuration must match.
Source: https://www.expresslrs.org/quick-start/getting-started/
Evidence: sourced; target compatibility must be rechecked for our board.

### F-006 — Sensor example
Claim: BMI270 combines a three-axis accelerometer and three-axis gyroscope.
Source: https://www.bosch-sensortec.com/en/products/motion-sensors/imus/bmi270
Evidence: sourced. Not a final IMU selection or proof of suitability for our aircraft.

### F-007 — ESC switching devices
Claim: MOSFET on-resistance and gate charge affect loss and switching behavior; component current ratings alone cannot establish an assembled ESC's operating current.
Sources: https://wiki.am32.ca/development/Hardware-Design.html ; https://www.ti.com/lit/pdf/slva714
Evidence: sourced. Actual thermal and transient limits require calculation and measurement.

## Claims needing further verification

- Video explanations of LoRa processing gain and numeric gain examples: verify against the selected transceiver documentation and modulation settings.
- RF range, receiver sensitivity, and interference performance: do not convert demonstration distances into guaranteed specifications.
- Upstream ESC current ratings: retain as upstream claims until test conditions and our reproduction are verified.
- Drop-in IMU compatibility: verify exact pinout, supplies, orientation, driver, sampling behavior, and filtering. A matching package is insufficient.
- Indian supplier availability, prices, delivery, and sourcing authenticity: not checked yet.
- Manufacturing scope for motors, propellers, batteries, frame, and radio handset: unresolved; no claim that upstream supplies open designs for all of them.

## Measurement record rule

Measured entries must link raw files plus instruments, calibration limitations, firmware commit, board revision, supply conditions, load, and repeat count. Corrections require a date and explanation.

## Motor/ESC study additions — 2026-10-15

### F-008 — Pinned reference architecture (sourced)
OpenESC-30x30 architecture notes at commit bf306934b5decc130ab1df6b653563ea16165e8e describe four channels, each using AT32F421G8U7, NSG2065Q, and six SP40N01GHNK devices. The channel schematic was retrieved and these values identified; nets, ratings, layout, and firmware have not been fully audited. Source: https://github.com/OpenDrone-hw/OpenESC-30x30/blob/bf306934b5decc130ab1df6b653563ea16165e8e/AGENTS.md .

### F-009 — Back-EMF startup limitation (sourced)
Rotation-generated back-EMF vanishes at standstill, so a sensorless method relying on that signal needs a suitable startup strategy. Source: https://www.ti.com/document-viewer/lit/html/SSZTBP2/GUID-E16F6FD4-B74F-4AB0-990E-C89D493A2398 . Not measured here.

### F-010 — Electrical/mechanical speed (sourced)
For p rotor pole pairs, electrical frequency in Hz equals p times mechanical RPM divided by 60. Source: https://ww1.microchip.com/downloads/en/Appnotes/AN3998-Sensorless-BLDC-MC-AVR-MCU-Fam-DS00003998.pdf . Numerical examples in motor-esc-study.md are instructional, not selected motor specifications.

## Communication corrections — 2026-10-15 (sourced, not measured)

### F-011 — UART error detection
Optional parity offers limited error detection; no automatic correction is implied. Source: ADI UART clock-accuracy article linked in communication-protocols.md.

### F-012 — I²C address capacity
Seven-bit addressing has reserved ranges; usual non-reserved addresses are 0x08–0x77 (112). Ten-bit addressing exists. Physical loading and address conflicts also limit a real bus. Source: NXP UM10204 Rev. 7.0, linked in communication-protocols.md.

### F-013 — 1-Wire supply and return
DS18B20 uses a data line and ground, with external or supported parasite power. One data wire does not remove the ground return. Source: manufacturer product/datasheet linked in communication-protocols.md.

## Firmware inspection — 2026-10-15

### F-014 — OpenDrone AM32 target (source-inspected)
At OpenDrone-hw/AM32 commit 5f8978eeb618c14bb396af7ac049d2a5e7b5a508 on feat/openesc-20-target, Inc/targets.h defines OPENESC_20_F421 and selects hardware groups AT_B and AT_045. Default main is a different commit. This does not establish compatibility with the previously studied 30x30 board. See esc-firmware-guide.md for exact links and limitations.

### F-015 — DShot input handling (source-inspected)
At the same commit, Src/dshot.c computeDshotDMA() decodes capture timing, validates check bits, reconstructs a command, and conditionally updates newinput. Startup, arming, and programming modes affect behavior; no hardware execution has been verified.
