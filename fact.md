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
