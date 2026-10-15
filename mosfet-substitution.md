# SP40N01GHNK substitution study

Date: 2026-10-15. Study only: no substitute approved, hardware modified, firmware flashed, or electrical measurements performed. User reports difficulty sourcing this component in India; nationwide unavailability has not been independently established.

## Does replacement require rewriting the bootloader?

Usually no. A conventional MOSFET has no firmware or digital identity. The MCU commands the gate driver, which charges/discharges its gate. A compatible replacement leaves that interface intact.

The bootloader loads application firmware and depends on MCU, programming/input connection and memory layout. Keeping those unchanged normally leaves it unchanged. Application configuration may need adjustment for dead time, PWM frequency and sensing/commutation behavior, but only after engineering analysis and measurements. A different MCU or control topology is a separate porting task.

Pinned AM32 target OPENESC_20_F421 contains DEAD_TIME 60; physical time units are unresolved. This target explicitly names 20x20 and is not validated for our 30x30 reference. Never interpret 60 as nanoseconds or flash this target solely because the MCU matches.

## Reference evidence

OpenESC-30x30 commit bf306934b5decc130ab1df6b653563ea16165e8e, library fdf8319b3512925a7566532ae4b38a298cf54c24. Channel schematic: six SP40N01GHNK, NSG2065Q gate driver, 15-ohm gate resistors; board driver supply 10 V.

Original Siliup SP40N01GHNK datasheet v1.1:

| Characteristic | Published value and condition |
|---|---|
| Type/package | N-channel, PDFN5x6-8L |
| Drain-source limit | 40 V |
| Gate-source absolute limit | ±20 V |
| On resistance | 1.2 mΩ typical, 1.5 mΩ maximum, VGS=10 V, ID=20 A, 25°C |
| Threshold | 2–4 V at 250 µA; not a full-enhancement specification |
| Total gate charge | 126 nC typical; published test VDS=20 V, VGS=20 V, ID=30 A |
| Gate-drain charge | 15.5 nC typical under those charge test conditions |
| Junction limit | 150°C |
| Current limits | 230 A silicon / 120 A package at case 25°C; neither is an ESC current rating |

The 20 V gate-charge condition is explicitly printed in the source; do not silently replace it with 10 V or compare it directly with another manufacturer's 10 V result. Datasheet switching times also use 20 V drive and 3-ohm gate resistance, unlike our board.

NSG2065Q v1.0: 1.2 A source / 1.5 A sink typical short-circuit pulse drive at 15 V; internal dead time 100/200/300 ns min/typ/max at 15 V, 1 nF, 25°C. These are specified test conditions, not measured board behavior at 10 V. Account for driver interlocking and MCU timing together; verify actual gate waveforms.

## Replacement qualification checklist

1. Define battery voltage, transient margin, phase RMS/peak current, PWM frequency, cooling and PCB constraints. Standard 4.2 V/cell 6S is 25.2 V full, 8S 33.6 V; switching/regen can raise bus voltage further.
2. Match N-channel type, individual pin functions, exposed drain pad, land pattern, package height and stencil. A nominal 5x6 mm body is insufficient to establish compatibility.
3. Check VDS with overshoot margin and VGS including negative/positive ringing. Absolute maximum ratings are limits, not operating targets.
4. Compare maximum RDS(on) at the available gate voltage and its increase with junction temperature. Check safe operating area, pulse capability and realistic thermal paths. Do not select by headline amperes.
5. Compare Qg, Qgd, Miller behavior, Coss/Qoss and reverse-recovery behavior at comparable conditions. Faster switching can increase ringing, EMI and unintended turn-on.
6. Recheck driver peak current, gate resistor losses, gate supply loading, bootstrap charge budget and voltage droop, minimum off-time/refresh, and layout parasitics.
7. Check high/low switch overlap, dead time, body-diode conduction, switch-node settling and back-EMF sampling. Too little dead time risks shoot-through; too much increases diode losses. Do not tune from a datasheet delay number alone.
8. Reassess snubbers, decoupling, current loops, copper/vias, soldering and cooling. Avalanche rating does not make repeated uncontrolled transients acceptable.
9. Check genuine supply, exact suffix, lifecycle, MOQ, delivered India price/tax, lead time and replenishment. A distributor's India website does not prove domestic stock.
10. Validate progressively: unpowered inspection, current-limited bring-up, gate waveform verification using appropriate differential/isolated measurement, unloaded motor without propeller, then controlled load and thermal/transient testing. Never attach an earth-ground scope clip to a high-side switching node. Log results before claiming a current rating.

First-order learning equations, not a complete loss model:

- Per-device conduction: P ≈ I_RMS² × RDS(on, temperature).
- Gate-drive supply power: P ≈ Qg × Vdrive × switching frequency per switching device. Dissipation is shared across driver/gate resistance and depends on circuit details.
- Hard-switch overlap: P ≈ 0.5 × VDS × I × (tr+tf) × frequency; actual waveforms, capacitance and diode losses must also be considered.

## Example candidate for study, not an approved substitute

TI CSD18540Q5B: 60 V, SON 5x6 mm; RDS(on) max 2.2 mΩ at 10 V/28 A; Qg typical 41 nC at 10 V/30 V drain/28 A. The original's 1.5 mΩ maximum at 10 V/20 A is lower, but a complete loss comparison also needs temperature and switching behavior. Gate-charge test conditions differ, so 126/41 is not a valid demonstrated drive-loss ratio. Footprint/pinout, timing and actual India stock remain unverified. Higher voltage rating alone does not establish suitability.

## Sources

- [Pinned hardware](https://github.com/OpenDrone-hw/OpenESC-30x30/tree/bf306934b5decc130ab1df6b653563ea16165e8e/hardware)
- [SP40N01GHNK datasheet in pinned library](https://github.com/OpenDrone-hw/KiCad-Library/blob/fdf8319b3512925a7566532ae4b38a298cf54c24/datasheet/SP40N01GHNK.pdf) — local submodule PDF is evidence; upstream URL should be checked if repository naming changes.
- NSG2065Q.pdf from the same pinned library, v1.0.
- [TI CSD18540Q5B official datasheet Rev B](https://www.ti.com/lit/ds/symlink/csd18540q5b.pdf)
- [Firmware study and remaining compatibility gaps](esc-firmware-guide.md)

Next design step: specify our first bench ESC's voltage/current target, then populate a candidate matrix with matched conditions and dated sourcing evidence before changing the PCB.
