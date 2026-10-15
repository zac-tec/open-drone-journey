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
