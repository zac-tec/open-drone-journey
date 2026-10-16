# OpenRX Gemini — complete component and India sourcing list

Extracted 2026-10-16 from OpenDrone-hw/OpenRX-Gemini commit `5f5138bebfc0da1d1244512f8eef516aaa943a5c`, KiCad-Library `fdf8319b3512925a7566532ae4b38a298cf54c24`, using KiCad CLI 10.0.6. This is a generated study export from authoritative schematics, not an upstream circuit/BOM modification.

**One board: 81 components, 35 distinct MPN/footprint groups, plus five copper pads.** No DNP flags in this export. C32 is absent in the source; do not invent a part for numbering gaps. Quantities exclude assembly spares, feeder losses and supplier minimum orders. Every fitted reference is listed below and separately in source-bom.csv; reference sets were checked against the XML netlist (86 total).

- [Grouped procurement CSV](grouped-components.csv): all 35 exact MPNs, quantities, footprints, source LCSC IDs, located supplier links and explicit unverified lookup links.
- [Every reference, raw KiCad CSV](source-bom.csv): one line per schematic reference.
- [Raw KiCad XML netlist](source-netlist.xml): provenance and connectivity evidence.

Package numbers in the tables are **imperial**: 0201 = 0.6 × 0.3 mm, 0402 = 1.0 × 0.5 mm, 0603 = 1.6 × 0.8 mm. In particular 0201/0603 metric is not the larger imperial 0603 part. Match the complete footprint and part specification.

## All fitted parts

### ICs, RF parts, clocks, antenna and connectors

| References | Qty | Schematic value | Exact MPN | Footprint | Source LCSC |
|---|---:|---|---|---|---|
| AE1 | 1 | 2450AT18A100E | 2450AT18A100E | ANT-SMD_L3.2-W1.6 | [C89334](https://www.lcsc.com/product-detail/C89334.html) |
| D1 | 1 | XL-1010RGBC-WS2812B | XL-1010RGBC-2812B | LED-SMD_4P-L1.0-W1.0-TL_XL-1010RGBC-WS2812B | [C5349953](https://www.lcsc.com/product-detail/C5349953.html) |
| FL1, FL2 | 2 | 2450FM07D0034T | 2450FM07D0034T | FILTER-SMD_4P-L1.0-W0.5-L | [C2651081](https://www.lcsc.com/product-detail/C2651081.html) |
| J1, J2 | 2 | Conn_Coaxial_Small | U.FL-R-SMT-1(80) | U.FL_Hirose_U.FL-R-SMT-1_Vertical | [C88374](https://www.lcsc.com/product-detail/C88374.html) |
| OSC1 | 1 | OW7EL89CENUYO3YLC-32M | OW7EL89CENUYO3YLC-32M | OSC-SMD_4P-L2.0-W1.6-BL_TXC_7Z | [C22381772](https://www.lcsc.com/product-detail/C22381772.html) |
| T1, T2 | 2 | 0900PC16J0042001E | 0900PC16J0042001E | FILTER-SMD_10P-L2.0-W1.6-BL | [C19842466](https://www.lcsc.com/product-detail/C19842466.html) |
| U1 | 1 | ESP32-C3 | ESP32-C3FH4 | QFN-32-1EP_5x5mm_P0.5mm_EP3.7x3.7mm | [C2858491](https://www.lcsc.com/product-detail/C2858491.html) |
| U2 | 1 | TLV75533PDQNR | TLV75533PDQNR | X2SON-4_L1.0-W1.0-P0.65-TL-EP | [C2861882](https://www.lcsc.com/product-detail/C2861882.html) |
| U3, U6 | 2 | LR1121IMLTRT | LR1121IMLTRT | QFN-32-1EP_5x5mm_P0.5mm_EP3.7x3.7mm | [C7498014](https://www.lcsc.com/product-detail/C7498014.html) |
| U4, U7 | 2 | RFX2401C | RFX2401C | QFN-16_L3.0-W3.0-P0.50-BL-EP1.7 | [C19213](https://www.lcsc.com/product-detail/C19213.html) |
| U5, U8 | 2 | SKY13373-460LF | SKY13373-460LF | QFN-12_EP_2x2_Pitch0.5mm | [C150853](https://www.lcsc.com/product-detail/C150853.html) |
| U9 | 1 | TS2306A 240GF MSM 9_C2976675 | TS2306A 240gf MSM 9 | SW-SMD_4P-L3.0-W2.0-P0.85-LS3.5 | [C2976675](https://www.lcsc.com/product-detail/C2976675.html) |
| X1 | 1 | CJ17-400001010B20 | CJ17-400001010B20 | CRYSTAL-SMD_4P-L1.6-W1.2-BL | [C2875272](https://www.lcsc.com/product-detail/C2875272.html) |

### Capacitors

| References | Qty | Schematic value | Exact MPN | Footprint | Source LCSC |
|---|---:|---|---|---|---|
| C1, C3 | 2 | 15pF | GRM0335C1H150JA01D | C_0201_0603Metric | [C85891](https://www.lcsc.com/product-detail/C85891.html) |
| C2, C15, C23, C24, C36, C39, C42, C44 | 8 | 47p / 47pF | GRM0335C1H470JA01D | C_0201_0603Metric | [C85908](https://www.lcsc.com/product-detail/C85908.html) |
| C4, C10, C17, C25, C27, C28, C31, C41 | 8 | 1uF | GRM033R61A105ME44D | C_0201_0603Metric | [C76935](https://www.lcsc.com/product-detail/C76935.html) |
| C5, C6, C9, C12, C13, C14, C16, C35, C37 | 9 | 100nF | GRM033R61E104KE14D | C_0201_0603Metric | [C76939](https://www.lcsc.com/product-detail/C76939.html) |
| C7, C34 | 2 | 10pF | GRM0335C1H100FA01D | C_0201_0603Metric | [C384956](https://www.lcsc.com/product-detail/C384956.html) |
| C8, C18 | 2 | 10uF | CL05A106MQ5NUNC | C_0402_1005Metric | [C15525](https://www.lcsc.com/product-detail/C15525.html) |
| C11 | 1 | 10uF | GRM155R60J106ME44D | C_0402_1005Metric | [C76991](https://www.lcsc.com/product-detail/C76991.html) |
| C19, C33 | 2 | 2.2nF | GRM033R71E222KA12D | C_0201_0603Metric | [C161488](https://www.lcsc.com/product-detail/C161488.html) |
| C20, C38 | 2 | 470nF | GRM033R60J474KE90D | C_0201_0603Metric | [C85926](https://www.lcsc.com/product-detail/C85926.html) |
| C21, C40 | 2 | 220pF | GRM0335C1E221JA01D | C_0201_0603Metric | [C907939](https://www.lcsc.com/product-detail/C907939.html) |
| C22, C43 | 2 | 1n | GRM033R71H102KA12D | C_0201_0603Metric | [C85934](https://www.lcsc.com/product-detail/C85934.html) |
| C26 | 1 | 10nF | GRM033R61A103KA01J | C_0201_0603Metric | [C2168164](https://www.lcsc.com/product-detail/C2168164.html) |
| C29, C30 | 2 | 1.2pF | GRM0335C1H1R2BA01D | C_0201_0603Metric | [C85895](https://www.lcsc.com/product-detail/C85895.html) |

### Inductors

| References | Qty | Schematic value | Exact MPN | Footprint | Source LCSC |
|---|---:|---|---|---|---|
| L1, L6 | 2 | 10uH | MLZ1608N100LT000 | L_0603_1608Metric | [C194437](https://www.lcsc.com/product-detail/C194437.html) |
| L2 | 1 | 24nH | LQP03TN24NH02D | L_0201_0603Metric | [C206441](https://www.lcsc.com/product-detail/C206441.html) |
| L3 | 1 | 2.0nH | LQP03TN2N0B02D | L_0201_0603Metric | [C86125](https://www.lcsc.com/product-detail/C86125.html) |
| L4 | 1 | 2.5nH | LQP03TN2N5C02D | L_0201_0603Metric | [C206435](https://www.lcsc.com/product-detail/C206435.html) |
| L5, L7 | 2 | 47nH | LQW15AN47NJ00D | L_0402_1005Metric | [C192855](https://www.lcsc.com/product-detail/C192855.html) |

### Resistors

| References | Qty | Schematic value | Exact MPN | Footprint | Source LCSC |
|---|---:|---|---|---|---|
| R1, R10 | 2 | 200 | RC0201FR-07200RL | R_0201_0603Metric | [C274337](https://www.lcsc.com/product-detail/C274337.html) |
| R2, R3, R4, R5 | 4 | 10k | RC0201FR-0710KL | R_0201_0603Metric | [C106225](https://www.lcsc.com/product-detail/C106225.html) |
| R6, R9 | 2 | 220 | ERJ-1GNF2200C | R_0201_0603Metric | [C2074788](https://www.lcsc.com/product-detail/C2074788.html) |
| R7, R8, R11, R12 | 4 | 100k | RC0201FR-07100KL | R_0201_0603Metric | [C106224](https://www.lcsc.com/product-detail/C106224.html) |

## Pads and additional items

TP1 RX, TP2 TX, TP3 5 V, TP4 GND and TP5 test/boot pad are copper features: buy no component for these. J1/J2 are board-mounted U.FL receptacles, not the external antennas. Budget separately for the six-layer 1.0 mm PCB, two appropriate external RF antennas and leads, hookup wires, stencil/assembly, programming/test fixture and a compatible ExpressLRS transmitter for testing. Antenna/lead MPNs are not specified in this schematic BOM.

## Located suppliers and limits — checked 2026-10-16

India storefronts do not establish stock physically located in India. These are product listings surfaced by web research; indexed stock and prices can lag checkout. No purchases, supplier contacts, quotations or delivery commitments were made. Overseas LCSC references are separated from India-serving listings.

| Exact MPN | Located supplier | Evidence / remaining check |
|---|---|---|
| ESP32-C3FH4 | [Mouser India](https://www.mouser.in/en/ProductDetail/Espressif-Systems/ESP32-C3FH4) | Exact listing; indexed page reports stock; recheck checkout |
| TLV75533PDQNR | [Mouser India](https://www.mouser.in/en/ProductDetail/Texas-Instruments/TLV75533PDQNR) | Exact listing; price visible; stock not established |
| LR1121IMLTRT | [Mouser India](https://www.mouser.in/en/ProductDetail/Semtech/LR1121IMLTRT) | Exact listing; indexed page reports stock; recheck checkout |
| RFX2401C | [Mouser India](https://www.mouser.in/en/ProductDetail/Skyworks-Solutions-Inc/RFX2401C) | Exact listing; indexed page reports stock and long lead time |
| SKY13373-460LF | [DigiKey India](https://www.digikey.in/en/products/detail/skyworks-solutions-inc/SKY13373-460LF/5015832) | Exact listing found; stock/price unverified |
| 0900PC16J0042001E | [Mouser India](https://www.mouser.in/en/ProductDetail/Johanson-Technology/0900PC16J0042001E) | Exact listing found; stock/price unverified |
| 2450FM07D0034T | [Mouser India / DigiKey India](https://www.mouser.in/en/ProductDetail/Johanson-Technology/2450FM07D0034T) | Old MPN listing restricted in region; global MPN 2450FM07D0034001T has DigiKey listing; confirm manufacturer renumber before ordering |
| U.FL-R-SMT-1(80) | [Mouser India](https://www.mouser.in/en/ProductDetail/Hirose-Connector/U.FL-R-SMT-180) | Exact listing found; stock/price unverified |
| GRM033R61A105ME44D | [Mouser India](https://www.mouser.in/en/ProductDetail/Murata-Electronics/GRM033R61A105ME44D) | Exact listing; indexed stock 0/backorder; recheck |
| GRM033R61E104KE14D | [Mouser India](https://www.mouser.in/en/ProductDetail/Murata-Electronics/GRM033R61E104KE14D) | Exact listing found; stock unverified |
| LQP03TN2N0B02D | [Mouser India](https://www.mouser.in/en/ProductDetail/Murata-Electronics/LQP03TN2N0B02D) | Exact listing; indexed page reports stock; recheck |
| LQP03TN2N5C02D | [Mouser India](https://www.mouser.in/en/ProductDetail/Murata-Electronics/LQP03TN2N5C02D) | Exact listing; indexed page reports stock; recheck |
| OW7EL89CENUYO3YLC-32M | [LCSC, overseas route](https://www.lcsc.com/pt/product-detail/C22381772.html) | Exact overseas listing found; India delivery and domestic stock unverified |
| CJ17-400001010B20 | [LCSC, overseas route](https://lcsc.com/product-detail/Crystals_Jiangsu-Changjing-Electronics-Technology-Co-Ltd-CJ17-400001010B20_C2875272.html) | Exact overseas listing found; India delivery and domestic stock unverified |

RF filter follow-up: [DigiKey 2450FM07D0034001T](https://www.digikey.in/en/products/detail/johanson-technology-inc/2450FM07D0034001T/9477815) lists 2450FM07D0034T as an alias. Confirm manufacturer part-number-change documentation, exact footprint and supplied suffix before accepting this in an order. The schematic source MPN has been preserved.

Additional exact-MPN catalogue appearances found for GRM0335C1H150JA01D, MLZ1608N100LT000 and 2450AT18A100E, but individual product/checkout validation remains pending. The CSV conservatively marks them unverified. LED source Value is XL-1010RGBC-WS2812B but its orderable MPN field is XL-1010RGBC-2812B, C5349953; boot switch MPN is TS2306A 240gf MSM 9, C2976675. Confirm these exact items using committed datasheets rather than dropping the suffixes.

## Purchasing checks

Use exact source MPNs initially. For passives verify voltage, dielectric, tolerance, DC bias, power/current rating and package; for RF inductors also Q and self-resonance. Identical capacitance/inductance values do not establish RF equivalence. Match TCXO frequency, supply, output waveform, stability and padout; a generic 32 MHz crystal is not a TCXO replacement. ESP32-C3FH4 is a bare IC, not a development board or MINI module.

Before ordering: reconcile schematic with PCB/assembly variant, verify manufacturer datasheets and library land patterns, obtain delivered price/MOQ/lead time for every line, and include PCB/assembly/test cost. This source export has not been independently electrically validated; no alternative component is approved. Complete India sourcing is still pending for rows explicitly marked unverified.

Reproduce the source exports from the cloned project:

```sh
kicad-cli sch export bom --fields 'Reference,Value,Footprint,MPN,Manufacturer,LCSC,Datasheet,QUANTITY,DNP' -o source-bom.csv hardware/OpenRX-Gemini.kicad_sch
kicad-cli sch export netlist --format kicadxml -o source-netlist.xml hardware/OpenRX-Gemini.kicad_sch
```
