# Roadmap

Each topic follows: principle → governing relationships → reference circuit/code → calculations → alternatives → experiment → evidence → explanation for others.

1. Define mission, aircraft size/mass, payload, flight time, voltage range, budget, workshop tools, and manufacturing scope.
2. Map system interfaces and power flow. Explain voltage domains, grounding, current paths, and fault behavior.
3. Select an upstream FC revision. Study schematic blocks, MCU resources, IMU acquisition, timing, target configuration, and logging.
4. Audit its BOM for India procurement. Evaluate alternatives before layout changes.
5. Prepare manufacturing files and test plan; fabricate/assemble FC; validate rails, boot, sensor axes, communication, and output behavior.
6. Study one ESC channel: motor model, half-bridges, gate drive, timing, sensing, protection, switching/thermal losses. Validate on a suitable fixture before expanding to four channels.
7. Study radio hardware and firmware: link budget, matching, RF layout, antenna integration, telemetry, failsafe, and measured performance.
8. Design/fabricate mechanical parts as chosen; characterize propulsion combinations; integrate electronics.
9. Progress from bench checks to controlled flight testing, data analysis, tuning, and reproducible documentation.

Reference hardware can provide comparison measurements. Designing every board at once is not required to reach the goal of our own system.

For any flight/radio operation, investigate applicable Indian requirements using current primary sources at the time of that decision. No legal conclusions or band selections are recorded yet.

## Current learning order — 2026-10-15

User chose motor and ESC first, starting from schematics with no hardware. Module 1 is motor-esc-study.md. This supersedes the earlier proposed FC-first ordering. Study one motor-drive channel, then prototype and validate it before integration. Hardware purchases depend on requirements, tools, and sourcing review.
