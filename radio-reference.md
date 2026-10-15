# Drone project: radio link reference

Saved 2026-10-15. Project intent: learn and eventually design custom drone electronics, including a flight controller, ESC, and radio receiver. Aircraft size, budget, payload, and autonomy requirements remain undecided.

## References and scope

- Radio reference: OpenDrone, “How LoRa (ExpressLRS) Drone Receivers Work”: https://www.youtube.com/watch?v=ssmQkRkXE84
- Flight controller reference: https://www.youtube.com/watch?v=XDYZoMRJFeQ
- ExpressLRS documentation: https://www.expresslrs.org/
- Receiver wiring: https://www.expresslrs.org/quick-start/receivers/wiring-up/
- DIY hardware/target guidance: https://www.expresslrs.org/quick-start/getting-started/
- Open hardware organization: https://github.com/OpenDrone-hw

The radio video demonstrates receivers and explains the control link. It is not an ESC design tutorial or a complete handheld transmitter design. Although called receivers, these devices can transmit telemetry.

## System architecture

Pilot sticks → handset/TX module → RF link → aircraft RX → CRSF over UART → flight controller → DShot → ESC → motor.
Telemetry travels back from the aircraft through the receiver to the handset. FPV video is a separate link.

## Keywords and theory

| Term | Working definition |
|---|---|
| TX / RX | Transmit / receive; also labels for serial pins. Context matters. |
| Transceiver | Radio device that both transmits and receives. |
| ExpressLRS | Open-source radio-control system; not the name of the underlying modulation alone. |
| LoRa | Chirp spread-spectrum modulation used by relevant ExpressLRS modes. Not every ExpressLRS mode uses LoRa. |
| CRSF | Serial control/telemetry protocol commonly connecting an ExpressLRS receiver to the FC. |
| UART | Asynchronous serial interface; normally receiver TX → FC RX and receiver RX → FC TX. Check voltage levels and board documentation. |
| Carrier / frequency / wavelength | RF oscillation; wavelength = propagation speed / frequency. |
| AM / FM | Analog amplitude / frequency modulation. |
| ASK / FSK / PSK | Digital amplitude / frequency / phase shift keying. |
| QAM | Quadrature amplitude modulation; symbols differ in amplitude and phase. |
| Symbol | One modulation state or waveform encoding information. |
| Chirp | Signal whose instantaneous frequency sweeps over time. |
| Dechirping | Mixing a received chirp with a reference to convert symbol information into a tone-like result. |
| FFT | Fast Fourier transform; efficient computation of frequency content. |
| Processing gain | Benefit of spreading/correlation and observation time when recovering a signal from noise. It has tradeoffs in rate, bandwidth, and latency. |
| Bandwidth | Frequency span occupied or processed; distinct from data rate. |
| Packet rate / latency | Frequency of packet transmission / elapsed delay through the system. |
| dB | Logarithmic ratio; not an absolute power unit. |
| dBm | Absolute power relative to 1 milliwatt; captions saying dpm are incorrect. |
| RSSI | Received signal strength indication. |
| SNR | Signal-to-noise ratio, with specified measurement bandwidth. |
| LQ | Link quality; successful packet reception measure, not the same as RSSI. |
| Sensitivity | Minimum input signal meeting a specified reception/error criterion for a particular mode. |
| Noise floor | Noise level over a specified measurement bandwidth. |
| Link budget | Transmit power plus gains minus losses, evaluated against receiver sensitivity and required margin. |
| Diversity / Gemini | Multiple reception paths / ExpressLRS multi-radio functionality; exact behavior depends on hardware and mode. |
| Characteristic impedance | Traveling-wave voltage/current relationship determined by transmission-line geometry and materials. Not DC trace resistance. |
| 50 ohms | Common nominal RF interface impedance; not universal to all RF systems. |
| Matching / reflection | Matching impedances reduces reflected energy at discontinuities. |
| Via / ground stitching | Layer transition / nearby ground connections that help maintain the RF return path. |
| U.FL / ceramic antenna | Small coaxial connector / compact antenna requiring its intended layout and keepout. |
| OTA update / binding | Wireless firmware update / associating compatible radio devices. |

## Facts and qualifications to retain

1. LoRa can recover signals below the noise power measured across the receiver bandwidth by using processing gain. This does not violate information theory. The video's 24 dB example is not a universal gain value.
2. Range depends on transmit power, antennas, orientation, interference, bandwidth, mode, terrain, and installation. Demonstrated kilometer ranges are not guaranteed specifications.
3. Lower frequency gives a lower free-space loss for equal antenna gains, but does not guarantee a better installed link or penetration through every material. Band choice also depends on antenna size, interference, and regional rules.
4. RF traces and vias must be designed with a continuous reference and controlled return path. Vias are not forbidden in RF; poorly designed transitions cause problems.
5. Return current concentrates near the signal trace on an adjacent reference plane at high frequency; it is distributed, not literally atom-for-atom directly underneath.
6. MCU Wi-Fi used for updates is distinct from the dedicated ExpressLRS control-radio path. A Wi-Fi-capable MCU alone does not reproduce this receiver architecture.
7. Open-source firmware does not automatically make a commercial PCB open hardware. Check hardware files and license separately.
8. Design a custom receiver from a documented reference, including the manufacturer's RF layout and matching guidance. Firmware must match actual hardware; RF validation is required.

## Future project decisions

Decide aircraft purpose, size, target mass, payload, flight time, budget, existing tools, electronics experience, and operating region before freezing a BOM or radio band. Develop custom boards incrementally against working reference hardware.

## Context note

When this note was requested, the selected Chrome tab had navigated to “Drone Theory 101: Part 1” (https://www.youtube.com/watch?v=K05UwsiqZ_E). No separate selection was exposed by the context tool. This note intentionally records the preceding ExpressLRS reference identified by the user, rather than treating the newly opened video as the radio source.
