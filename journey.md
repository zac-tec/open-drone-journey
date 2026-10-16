# 2026-10-15 — Project foundation

## User intent

Build and understand our own open drone setup; manufacture our hardware; use OpenDrone repositories and videos as references; investigate Indian component availability and alternatives; document the full process in zac-tec on GitHub to help others.

## Learning preference

New to the setup but comfortable following theory. Explain deeply with concrete reasoning, not superficial beginner treatment. Discuss unclear topics as they arise. Understanding of individual topics has not yet been assessed.

## Work completed

- Created fact.md, separate history, glossary, sources, upstream map, roadmap, sourcing process, and reusable experiment/decision records.
- Preserved earlier radio and basic theory notes with their review limitations.
- Inspected OpenDrone repository index and identified incomplete areas.
- Checked local GitHub CLI: reported invalid authentication. GitHub integration discovery reported not installed in this session; connection requested through the available integration flow.

## Not completed

At the earlier foundation checkpoint no GitHub repository had been created; see the setup follow-up below. No stock checks, component approval, circuit changes, manufacturing, or bench tests occurred.

## Open questions

aircraft purpose/size; budget; equipment and experience; intended scope of self-manufacture.

## Next session

Pin a flight-controller reference commit. Begin a power-flow and interface walkthrough. Record questions and learner-confirmed understanding rather than assuming it.

## Repository setup follow-up

User authorized creating a repository under zac-tec. Created the public open-drone-journey repository using the signed-in browser after CLI authentication failed. Prepared these documents for the initial upload. No hardware work or stock verification has occurred.

## Initial GitHub publication

Verified the GitHub CLI is authenticated as zac-tec with admin access to this repository after network access was granted. Earlier token-invalid reports were misleading because the CLI could not reach GitHub; both stored accounts subsequently validated, with zac-tec active. The connector file-write route returned 403, so publication uses the authenticated CLI and Git. Initial commit contains 13 documentation files. No component stock checks, manufactured hardware, or flight results are claimed.

## Motor/ESC-first direction

Learner confirmed no hardware or tools and requested a fresh schematic-based start, studying necessary physics, mathematics, materials, electronics, and firmware toward independent product manufacturing. Created motor-esc-study.md and pinned OpenESC-30x30 to bf306934b5decc130ab1df6b653563ea16165e8e. Retrieved its channel schematic; identified major part values, but no complete circuit audit or experiment is claimed. FC-first order replaced by motor/ESC-first. Next: discuss rotation, commutation, and the first equations; then trace the power stage.

## Communication reference review

Reviewed the supplied six-interface video transcript. Created communication-protocols.md mapping timestamps and drone relevance; corrected UART detection, I²C addressing/loading, 1-Wire power/ground, SPI naming, and CAN reliability simplifications using primary sources. DShot remains the immediate ESC command topic and is not covered by this video. No hardware test or learner mastery claimed.

## DShot introduction

Started conceptual DShot lesson separating command signaling, power-stage PWM, commutation, and speed regulation. Added dshot-lesson.md; implementation and physical tests remain pending.

## Hardware and firmware together

User requested using the available OpenDrone ESC firmware as a guide toward our own similar design. Inspected the OpenDrone AM32 fork and pinned its hardware-specific branch. Documented command decoding, target configuration, input processing, commutation landmarks, bootloader/application distinction, and the unresolved 20x20-versus-30x30 baseline. We will learn theory alongside actual schematic/code instead of treating firmware as a black box.

## First live KiCad schematic session

Prepared the pinned OpenESC-30x30 checkout and its pinned shared library. Launched verified official KiCad 10.0.6 from its mounted image due to insufficient space for full installation. Opened root schematic and ESC1 successfully. Next discussion starts with Q1/Q2 and their phase-A switch node, then driver U4. No circuit edits or electrical tests. See kicad-walkthrough.md.

## Purchased versus open-source ESCs

User requested actual developer-backed differences. Reviewed full ESC-video transcript and published description, checked local hardware files/license and prior firmware inspection. Recorded access/reproduction benefits separately from unproven performance, cost, and reliability claims. Exact purchased comparator remains unspecified.

## Named T-Motor comparator

User supplied Velox V45A V2 and its Robokits link. Recorded listing claims/stock and identity inconsistencies; compared closed BLHeli_32 with AM32 source access and OpenDrone hardware files. Recorded BLHeli_32 lifecycle separately in history.md. No purchase, compatibility approval, or performance ranking. See velox-v45a-v2-comparison.md.

## MOSFET alternatives in India — 2026-10-15

User identified SP40N01GHNK sourcing difficulty and asked whether replacement requires bootcode changes. Reviewed original MOSFET and driver datasheets, distinguished bootloader from application timing, and recorded a qualification checklist. TI CSD18540Q5B is an educational candidate only, not approved or stock-verified. No hardware or firmware changed. See mosfet-substitution.md.

## OpenRX hardware study — 2026-10-16

Cloned the family hub and all four split receiver repositories with pinned libraries. Opened Lite and its detailed core sheet in KiCad. Recorded architecture, design differences and a quotation-based India manufacturing process. Cost and local stock remain unverified. See openrx-india-study.md.
