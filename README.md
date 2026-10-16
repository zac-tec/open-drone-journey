# Open Drone Journey

Learn, design, manufacture, assemble, test, and explain our own drone setup in India using open references. The aim is engineering understanding and reproducible work that helps others.

## Working agreement

- Explain the real engineering, equations, assumptions, and tradeoffs in plain language. Define unfamiliar terms without reducing the project to a superficial beginner tutorial.
- Pause on concepts the learner finds uncomfortable, discuss them, and record the clarified explanation. Never infer understanding simply because an explanation was delivered.
- Use OpenDrone repositories and related videos as guides. Check claims against datasheets, source code, and measurements.
- Build our own hardware progressively. Reference modules may be used as test equipment or comparison hardware; they do not replace the end goal.
- Investigate component availability and alternatives in India before freezing footprints or manufacturing a PCB.
- Record failed experiments, uncertainty, and corrections alongside successful results.
- Preserve upstream attribution and applicable licenses. A public repository is not automatically a complete, validated, reproducible product.

## Records

| File or folder | Purpose |
|---|---|
| fact.md | Current technical claims, evidence, scope, and limitations |
| history.md | Historical milestones and superseded project context |
| glossary.md | Terminology and plain-language explanations |
| sources.md, repositories.md, radio-reference.md, basic-theory-reference.md | Sources, review coverage, and upstream revision records |
| india-components.md | India procurement and engineering substitution evaluations |
| journey.md | Learning sessions, questions, changes, and next steps |
| experiment-template.md | Test procedures, conditions, raw evidence, and results |
| decision-template.md | Design choices and reasons |
| roadmap.md | Learning and manufacturing milestones |

## Current state

Documentation started on 2026-10-15. No aircraft specification, finalized BOM, schematic, PCB, manufactured board, or flight test has been completed in this project. Repository: https://github.com/zac-tec/open-drone-journey . Initial documentation published on 2026-10-15; experimental and manufacturing milestones remain pending.

Current study: [Motor and ESC, from schematics to our own hardware](motor-esc-study.md). Start with one motor-drive channel; no hardware purchases are needed for Lesson 1. This replaces the earlier FC-first suggestion.

Communication study reference: [reviewed video and corrected protocol notes](communication-protocols.md).

Firmware study: [OpenDrone AM32 source guide](esc-firmware-guide.md).

- [MOSFET substitution: electrical requirements, firmware impact and qualification](mosfet-substitution.md)

- [OpenRX receiver designs and India manufacturing study](openrx-india-study.md)
