# Communication interfaces — reviewed video reference

Source: “Every Hardware Protocol Explained Simply in 10 Minutes!”
https://www.youtube.com/watch?v=2LaiScfoYGQ
Reviewed 2026-10-15 using the full auto-generated English transcript (0:00–10:28). Visual demonstrations were not independently reviewed. This is a source review, not a hardware test. The title is broad: the video surveys six interfaces, not every communication protocol.

## Video map

| Time | Topic | Project relevance |
|---|---|---|
| 0:30 | UART | Receiver, debug, GPS connections, when supported |
| 2:07 | SPI | IMU and storage communication on applicable boards |
| 3:42 | I²C | Addressed sensor/peripheral bus |
| 5:24 | CAN | Possible future distributed devices; not assumed present on our ESC |
| 7:01 | RS-232 | Electrical-interface distinction and external instruments |
| 8:46 | 1-Wire | Example of timing-based shared sensor communication |

## Engineering distinctions

Separate electrical signaling, timing/framing, and message meaning. UART hardware moves framed bits; CRSF defines control/telemetry messages transported over a serial interface. RS-232 defines electrical interfacing and can carry UART-formatted traffic through a suitable transceiver. They are not competing alternatives at one identical layer.

Count power and ground separately from signal lines. Two data pins do not mean a complete two-conductor powered circuit. Establish compatible voltage thresholds, reference/return paths, timing, and firmware support before connecting anything.

## Corrected interface notes

### UART

Asynchronous serial communication: no separate shared clock wire. TX and RX commonly permit simultaneous communication in both directions. Both ends must match bit rate, data length, parity, stop bits, and polarity. Simple on-board UART normally also needs a common ground. A usual connection crosses TX to RX.

The video conflates lack of automatic correction with lack of detection: parity can detect some errors and UART peripherals commonly expose framing/overrun status. End-to-end integrity needs an appropriate message protocol. Standard UART use is point-to-point, while additional physical layers or special peripheral modes can support other arrangements.

For ordinary binary UART, 115200 baud corresponds to 115200 transmitted bits/s. With 8N1 (one start, eight data, one stop), maximum continuous data-byte throughput is 115200/10 = 11520 bytes/s before message overhead. Baud means symbols/s in general, not universally bits/s.

### SPI

A common arrangement uses SCLK, controller-to-target data, target-to-controller data, and chip select. Correct legacy names: MOSI = Master Out Slave In; MISO = Master In Slave Out. Captions mis-expand these terms. Controller/target terminology is useful, but datasheets may retain older names.

Match clock polarity (CPOL), clock phase (CPHA), bit order, frequency, and chip-select timing. One chip-select per target is common, not universal; daisy-chain and other variants exist. A shared clock does not eliminate propagation and setup/hold constraints. Speed comparisons depend on actual devices and bus modes.

### I²C

Ordinary bidirectional I²C shares SDA and SCL using open-drain outputs and pull-ups. Targets respond to addresses; duplicate fixed addresses may require a mux or separate bus.

The video's 127-device limit is inaccurate: seven-bit encoding has 128 combinations with reserved ranges; 0x08–0x77 are the usual 112 non-reserved addresses. Ten-bit addressing also exists. Address availability does not guarantee device count: capacitance, rise time, pull-ups, loading, and device capabilities matter. Adding devices does not inherently change the selected clock rate, although shared transactions consume bandwidth and loading can constrain the usable speed.

### CAN

High-speed CAN commonly uses differential CAN_H/CAN_L wiring, transceivers, and appropriate end termination. A CAN controller alone does not directly provide the physical bus interface.

Arbitration resolves simultaneous transmission by bitwise priority under protocol rules. This does not guarantee no data loss or failure under every fault/load condition. Termination, topology, timing, error handling, and application deadlines still require design. CAN is not automatically supported by a board because its MCU can emit digital signals. Higher-level protocols and firmware must also match.

### RS-232

Uses electrical levels and polarity different from typical 3.3 V MCU UART pins. A proper line driver/receiver bridges them. Never connect an RS-232 signal directly to an ordinary MCU logic input. The physical connector does not by itself identify the signaling standard; the familiar nine-pin serial connector is more precisely DE-9.

### 1-Wire

One data conductor plus a ground return. The DS18B20 supports either external supply or parasite power; parasite power is optional and imposes supply/pull-up requirements. It does not power itself without an energy source and return path. Its ROM includes a unique 64-bit code for selection on a shared bus. Follow actual timing, cable, and power requirements rather than treating device count as unlimited.

## Application to our build

| Connection | Candidate interface | Decision state |
|---|---|---|
| Test MCU to ESC command input | DShot, subject to selected firmware | Study exact frame/timing/arming requirements next |
| ESC MCU to gate driver | Control/PWM signals determined by schematic | Not automatically SPI or UART |
| FC to IMU | Often SPI; exact board decides | Check selected schematic |
| Receiver to FC | CRSF over UART for our referenced UART receiver setup | Check hardware and configuration |
| Optional slow sensors | I²C if supported | Not yet selected |
| Future distributed peripherals | CAN with matching hardware/software | Not part of the current prototype |

The video's six protocols omit our immediate ESC command protocol, DShot. PWM used inside a motor power stage is also a different role from a message protocol. Do not infer gate-driver interfacing from the list in this video.

## Primary references for corrections

- NXP UM10204 Rev. 7.0, I²C addressing, electrical behavior, and timing: https://www.nxp.com/docs/en/user-guide/UM10204.pdf
- ADI UART timing/parity: https://www.analog.com/en/resources/technical-articles/determining-clock-accuracy-requirements-for-uart-communications.html
- ADI SPI naming: https://www.analog.com/en/resources/app-notes/spii2c-bus-lines-control-multiple-peripherals.html
- TI CAN architecture and error behavior: https://www.ti.com/lit/an/sloa101b/sloa101b.pdf
- ADI DS18B20 product/datasheet: https://www.analog.com/en/products/ds18b20.html
- TI RS-232 driver/receiver example: https://www.ti.com/product/TRS3221E/part-details/TRS3221EIRGTR

Historical origin dates mentioned in the video are not adopted as verified technical facts. Learner understanding and hands-on tests remain pending.
