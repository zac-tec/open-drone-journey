# Source register

Record exact commits, document revisions, and video timestamps when a source supports a design decision. Videos provide explanations; datasheets, schematics, source code, and measurements establish implementation evidence.

| ID | Source | Coverage so far |
|---|---|---|
| S-001 | https://github.com/orgs/OpenDrone-hw/repositories | Organization index inspected 2026-10-15; no commit-pinned design audit yet |
| S-002 | https://www.youtube.com/watch?v=XDYZoMRJFeQ | Flight-controller transcript reviewed earlier; prototype differs from current repository |
| S-003 | https://www.youtube.com/watch?v=ssmQkRkXE84 | Radio receiver transcript reviewed earlier; qualifications retained in radio note |
| S-004 | https://www.youtube.com/watch?v=K05UwsiqZ_E | Partial prior review; full review pending |
| S-005 | https://github.com/OpenDrone-hw/OpenESC-30x30 | README inspected earlier; schematic and test evidence audit pending |
| S-006 | https://www.expresslrs.org/quick-start/receivers/wiring-up/ | UART/CRSF wiring reference |
| S-007 | https://betaflight.com/docs/wiki/guides/current/DSHOT-RPM-Filtering | RPM telemetry/filter reference |
| S-008 | https://wiki.am32.ca/development/Hardware-Design.html | Introductory ESC design guidance; use component datasheets for specifics |
| S-009 | https://www.ti.com/lit/pdf/slva714 | Gate-drive reference |

Preserve upstream author, license, URL, commit/tag, accessed date, file path, applicable board revision, and firmware branch. A repository default branch may track upstream rather than contain the hardware-specific changes.

## S-010 — Communication overview

https://www.youtube.com/watch?v=2LaiScfoYGQ — full auto-generated English transcript reviewed on 2026-10-15, 0:00–10:28. Six-interface survey; corrections and primary references in communication-protocols.md. Visuals not independently reviewed.

## S-011 — OpenDrone AM32 source baseline

Repository https://github.com/OpenDrone-hw/AM32 ; branch feat/openesc-20-target; commit 5f8978eeb618c14bb396af7ac049d2a5e7b5a508. Inspected AGENTS.md, README.md, Makefile, Inc/targets.h, Src/dshot.c, and selected Src/main.c regions. Source map and unresolved hardware correspondence in esc-firmware-guide.md. No compilation or flashing.
