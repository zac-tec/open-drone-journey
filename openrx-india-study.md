# OpenRX receiver study and India manufacturing

Date: 2026-10-16. Cloned family hub and all four authoritative board repositories into sibling folders under outputs/. Initialized each board's pinned KiCad-Library submodule. Opened OpenRX Lite in KiCad 10 and navigated to its ESP32-C3/SX1281 core sheet. No circuit edits, fabrication or RF tests performed.

## Designs

| Board | Radio | Antenna interface | Study assessment |
|---|---|---|---|
| Lite | One SX1281, 2.4 GHz | Ceramic ELRS antenna | Fewest radio-chain blocks alongside Lite-UFL |
| Lite-UFL | One SX1281, 2.4 GHz | External antenna through U.FL | Useful first study option for external antenna placement |
| Mono | One LR1121, dual band | One U.FL, RF switching and PA/LNA | More RF circuitry and sourcing dependencies |
| Gemini | Two LR1121 radios, dual band | Two U.FL | Most complex of these four |

All use ESP32-C3, ExpressLRS and CRSF; published PCBs are six-layer, 1.0 mm. Statements describe source designs, not independently measured performance. Hub: https://github.com/OpenDrone-hw/OpenRX .

## Lite signal path

ELRS antenna → RF filter → SX1281 radio ↔ SPI ↔ ESP32-C3 ↔ UART/CRSF ↔ flight controller. Telemetry travels in the reverse direction. The separate Wi-Fi antenna belongs to the ESP32-C3 configuration/flashing interface, not the ELRS radio link.

Power is 5 V input → TLV75533 3.3 V regulator → MCU/radio/oscillators. SX1281 radio clock is a 52 MHz temperature-compensated oscillator; MCU crystal is 40 MHz. Lite and Lite-UFL have no external PA/LNA or RF switch. Exact source: each board's AGENTS.md and schematic.

## Can we manufacture in India cheaply?

PCB fabrication and assembly can be arranged in India with a supplier that meets this board's specifications; semiconductor sourcing may still require imports. No local fabrication/assembly quotation or current component stock has been obtained. Do not assert domestic component availability or a finished unit price yet.

The unchanged design needs six-layer fabrication, controlled RF geometry/stack-up, fine-pitch QFN assembly, stencil/reflow, inspection, firmware programming and functional/RF validation. Preserve antenna keepouts and 50-ohm RF structures. A two-layer conversion is a redesign requiring RF validation, not a simple cost-saving substitution.

Compare total delivered cost per working board: PCB + components + assembly + stencil/setup share + shipping/taxes + programming/test + rework/rejected-unit allowance. Request quantities 1/5/10/50 rather than assuming batch economics from a single-unit component cart. A first prototype may exceed the price of a retail receiver. No confirmed price ranking between Lite and Lite-UFL until the antenna and assembly costs are included.

Sourcing priorities: SX1281IMLTRT, ESP32-C3 exact package/flash variant, 52 MHz TCXO, RF filter, antenna/connector, and TLV75533 regulator. LCSC catalogue IDs in upstream docs are sourcing references, not evidence of India stock. Export the BOM from the authoritative schematic before requesting quotations; do not order from this conceptual list.

A receiver also needs a compatible ExpressLRS transmitter to test the link. A receiver alone cannot supply pilot commands. Firmware target/configuration must match the selected board; do not flash an arbitrary ESP32 image. Open hardware is CERN-OHL-S-2.0; preserve notices and review license obligations when distributing changes. Public KiCad sources exist, but the hub says fab-ready production handoffs are private, so we must generate and validate our own manufacturing exports.

## Source revisions

| Repository | Studied commit |
|---|---|
| OpenRX-Lite | `a9e5a9fdcca48be45e43ab5ba86af9a6c9e48623` |
| OpenRX-Lite-UFL | `b8c35f6de77468bdd4c66319bc5ced1b88bc6ef6` |
| OpenRX-Mono | `468146aa3fc1dccb141d2727156ff1f0c736b5a3` |
| OpenRX-Gemini | `5f5138bebfc0da1d1244512f8eef516aaa943a5c` |

Next learning sequence: regulator → MCU/boot and CRSF → SPI and radio clock → RF filter/antenna → firmware target → BOM and India quotations. Start with Lite/Lite-UFL before evaluating dual-band designs.
