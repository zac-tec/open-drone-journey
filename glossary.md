# Glossary

| Term | Meaning and design relevance |
|---|---|
| FC | Flight controller: reads motion and commands, computes actuator outputs. |
| ESC | Electronic speed controller: switches power into motor phases. |
| IMU | Inertial measurement unit: typically gyro plus accelerometer here. |
| MCU | Microcontroller running embedded firmware. |
| PID | Proportional/integral/derivative feedback control; behavior depends on implementation and tuning. |
| Setpoint | Requested value, such as angular velocity in rate mode. |
| CRSF | Serial control/telemetry protocol commonly used between UART ExpressLRS receivers and FCs. |
| DShot | Digital ESC command protocol; bidirectional operation requires support. |
| SPI / I²C / UART | Different digital interfaces; not interchangeable wiring. |
| MOSFET / gate driver | Power switch / circuit that drives the switch gate. |
| Commutation | Sequencing motor phase excitation according to rotor position. |
| Back-EMF | Voltage induced by motor rotation, useful for sensorless position estimation. |
| Dead time | Gap preventing simultaneous high/low-side conduction. |
| Shoot-through | Unwanted direct supply current through a switching leg. |
| BOM / MPN | Bill of materials / exact manufacturer part number. |
| Footprint | Physical pad geometry; does not prove electrical compatibility. |
| ERC / DRC | Schematic electrical-rule / PCB design-rule checking. |
| Drop-in alternative | Replacement needing no circuit, layout, firmware, or manufacturing change; must be demonstrated. |
| Functional alternative | Can perform the role but may require redesign and new validation. |

See the radio reference for RF terminology. These are study definitions; detailed engineering claims belong in fact.md with evidence.
