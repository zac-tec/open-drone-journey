# Drone project: basic theory reference

Reference requested by user: Riley Morgan, “Drone Theory 101: Part 1. The basics, and how an fpv quadcopter functions!”
https://www.youtube.com/watch?v=K05UwsiqZ_E

Role: introductory reference for understanding the complete quadcopter and component relationships. This is a learning reference, not a frozen component specification.

## Fundamentals carried forward

- Frame: supports components; stiffness, mass, geometry, and vibration affect flight.
- Battery: supplies propulsion and electronics. Cell count, capacity, and current capability are separate properties.
- Power distribution / PDB: routes battery power to ESCs and other loads. A separate distribution board is one implementation; distribution can be integrated elsewhere.
- Regulator / BEC: supplies appropriate voltage to electronics; do not assume all components accept battery voltage.
- Flight controller: reads motion sensors and pilot commands, then computes individual motor commands.
- ESC: converts battery DC into switched three-phase power for a brushless motor.
- Receiver: supplies pilot commands to the FC; its compatible transmitter is on the ground.
- FPV camera → video transmitter (VTX) → video receiver/display: video path, separate from the control link.
- Roll, pitch, yaw: three rotation axes. Throttle changes collective motor demand; it does not directly guarantee a height or climb rate.
- A conventional quad uses two clockwise and two counterclockwise propellers. Diagonally opposite motors generally share rotation direction. Verify the chosen mixer and propeller arrangement.
- Propeller hand, motor direction, motor order, and FC sensor orientation must agree.
- Common electrical ground and correct voltage levels are necessary for wired signal interfaces.
- Motors, propellers, battery voltage, and ESC ratings must be selected as a combination using measured performance data.

## Evidence and limits

The earlier page context identified this video and supplied a transcript; the visible ending discussed propeller rotation and reaction torque. Its caption phrase “four different ways” should not be retained literally: there are two rotation directions.

At this save request, the live tab had already changed to “I Made the Drone I Couldn’t Buy” by The Tinkering Techie. No separate selection or full transcript for the newly opened video was returned. A web fetch of the requested older video failed. Therefore this note is a general theory reference, not a claim to have newly reviewed every statement in either video.

Older component examples and wiring protocols must be checked against the actual hardware selected for the project. Design decisions remain open.
