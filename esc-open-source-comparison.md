# Purchased and open-source ESCs — what actually differs

Reviewed 2026-10-15. These are two independent properties: purchasing describes how a board is obtained; openness describes available design/source materials and their licenses. A purchased ESC can be open hardware and run open firmware. A commercial board may also have closed hardware while running AM32 or another open firmware.

## Developer-video evidence

OpenDrone, “How Drone ESCs Work (so I built my own)”:
https://www.youtube.com/watch?v=TwAmmPxOpTM
Full auto-generated English transcript reviewed; chapter labels also read. The video prototype and later repository revisions are not automatically identical.

| Time | What the developer describes | What it establishes / does not establish |
|---|---|---|
| 1:46–3:46 | Six-step commutation and back-EMF-based timing | Motor-control principles used by this design; not a unique benefit of open source |
| 3:49–4:03 | First board lacked a virtual star reference; added resistors corrected twitching | A reported prototype fault and correction, not proof that every revision has been validated |
| 4:28–6:18 | Six MOSFETs, gate driver, bootstrap, AT32, feedback network | Main circuit blocks described by its designer |
| 6:20–6:51 | Four channels, regulation, capacitors, shared current sensing | Integration into a custom four-channel PCB |
| 7:00–7:12 | ST-Link bootloader programming followed by firmware flashing to all four channels | Uses AM32; the creator did not write an entirely new motor-control stack for this video |
| 7:30–7:55 | Three-inch aircraft with 1408 3700-KV motors and 6S supply | Described demonstration setup, not a required or approved combination for our prototype |
| 9:09–9:44 | Full-throttle run, reported battery exhaustion after about 90 seconds and surviving drone | Demonstration outcome; no controlled equal-condition competitor comparison or complete current/thermal rating established |

The description says the creator designed the board, ordered it from JLCPCB, and published hardware files. That is PCB design plus outsourced fabrication/assembly, not manufacture of the MCU or MOSFET silicon.

## Comparison by evidence, not labels

| Question | Purchased ESC with closed design | Open hardware with open firmware, such as our reference |
|---|---|---|
| Can it run a motor? | Yes if suitable and correctly configured | Yes if built, programmed, and validated appropriately |
| Can we study editable hardware? | Only if the vendor publishes it; otherwise teardown/reverse engineering may be needed | The reference publishes editable KiCad schematic and PCB sources |
| Can we study motor-control source? | Depends on firmware, not whether purchased | AM32 source and hardware-target definitions are available |
| Can we manufacture the same design? | Buying a board does not supply design files or reproduction rights | Published source plus license enables a licensed reproduction path; procurement/manufacturing/test work still required |
| Can we change a MOSFET/MCU? | Documentation and firmware access may constrain redesign | Can evaluate and modify source/design, but compatibility is not automatic |
| Is it faster/cooler/more efficient? | Requires measured comparison | Requires measured comparison; openness supplies no performance guarantee |
| Is it cheaper? | Depends on delivered price and services | Prototype PCBs, assembly, parts, shipping, taxes, equipment, rework, and failures must be counted |
| Is repair easier? | Depends on documents, packaging, tools, parts, and support | Schematics/source improve diagnosis; physical repair is still skill/tool dependent |
| Is quality guaranteed? | Must evaluate vendor's actual evidence and support | Must evaluate actual evidence; a public design is not a qualification report |

## What we directly inspected

OpenESC-30x30 commit bf306934b5decc130ab1df6b653563ea16165e8e has hardware/4in1.kicad_sch, hardware/ESC.kicad_sch, hardware/4in1.kicad_pcb, and a pinned library. We opened the original schematic in KiCad. Its LICENSE identifies CERN-OHL-S-2.0.

OpenDrone-hw/AM32 branch feat/openesc-20-target at 5f8978eeb618c14bb396af7ac049d2a5e7b5a508 exposes an OPENESC_20_F421 definition and source for command processing and commutation. The explicit 20x20 target has not been validated for the 30x30 design. AM32's README/license identifies GPL-3.0. Hardware and firmware licenses are separate; use their actual terms for distribution decisions.

Hardware source: https://github.com/OpenDrone-hw/OpenESC-30x30/tree/bf306934b5decc130ab1df6b653563ea16165e8e
Firmware source: https://github.com/OpenDrone-hw/AM32/tree/5f8978eeb618c14bb396af7ac049d2a5e7b5a508

## The concrete advantage for our goal

We gain design access, an inspectable implementation, and a route to modify/reproduce the hardware and firmware under their licenses. We still depend on component suppliers, materials, PCB processing, assembly, instruments, and validation. India sourcing alternatives are engineering candidates, not approved replacements.

No purchased ESC model has been specified. Therefore we cannot honestly claim a difference in its algorithm, MOSFET losses, latency, protection features, current capability, or reliability compared with this reference.

For a product-level comparison, use the same supply, motor, propeller/load, cooling, command conditions, and measurement method. Record supply and phase current separately where relevant, transient bus voltage, temperature over time, startup/desync behavior, efficiency, and fault behavior. Nominal amp labels or one flight are insufficient for a complete rating comparison.
