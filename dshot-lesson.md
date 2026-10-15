# DShot — first lesson

2026-10-15. Conceptual lesson only; no motor energized, transmitter implemented, or understanding assessed.

DShot carries a command from a controller to an ESC. Firmware inside the ESC interprets it and controls motor commutation. The message wire is separate from the battery/motor power path. Our standalone test controller can eventually replace an FC for this bench task.

A standard frame contains 11 command bits, one telemetry-request bit, and four check bits. Value 0 represents disarmed/zero throttle; 1–47 are special commands; 48–2047 are throttle values. These are not RPM units.

Bits have equal total duration but different high-pulse lengths. DShot300 means 300000 bits/s, not 300000 motor revolutions or messages/s. A 16-bit frame therefore occupies approximately 53.33 microseconds, before any gap or reply time.

The classic telemetry-request bit is not by itself bidirectional DShot. Supported bidirectional operation returns telemetry on the command wire and has additional signaling and timing rules. The four-bit check detects some corruption; it is not authentication and cannot catch every error.

Primary references: https://betaflight.com/docs/development/API/Dshot ; https://betaflight.com/docs/wiki/guides/current/DSHOT-RPM-Filtering . Exact AM32 startup, framing implementation, voltage levels, and timeout behavior must be reviewed before building a transmitter.

## Project distinction

Command interface: what the controller asks the ESC to do.
Power-stage PWM: how the ESC switches electrical power.
Commutation: how excitation is sequenced with rotor position.
Speed regulation: how measured/estimated speed is compared against a target.

These are separate functions. We will not infer accurate speed regulation from the ESC name or a throttle command. Next exercise: trace where a received command enters the chosen firmware and where it affects motor output.
