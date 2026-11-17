# Validation report — expanded build

## Automated checks completed in packaging environment

- PASS: Node.js syntax checks of server.js, public/game.js and public/world-data.js.
- PASS: server logic test with mocked WebSocket transport and fake clock.
- PASS: real local HTTP /health response within the test harness.
- PASS: content counts: 20 cars, 5 boats, 30 houses, 5 apartments, 3 penthouses, 2 planes, 1 helicopter, 15 legal jobs, 3 crimes.
- PASS: test scenarios listed in README.md.
- PASS: ZIP integrity and required-file inspection.

## Not tested here

- Actual browser/WebGL rendering and GLSL shader compilation.
- Real WebSocket upgrade/framing or multiple real browser clients.
- Sustained performance on target hardware.
- End-to-end Render deployment or durable disk behavior.
- Every mission destination/property doorway in a rendered world.

## Manual smoke test before release

1. Run npm install, npm run check, npm test, npm start.
2. Join from two different browser profiles; move and chat.
3. Complete two courier routes. Buy a Sunrunner and complete a taxi fare.
4. Use Jobs → Locate, visit each dispatch and verify Start is available when near.
5. Try timed mechanic work, sanitation multi-stop, security defense and photography.
6. Launch each boat at a marina, visit all island landings and test freight/fishing/rescue.
7. Fly both planes and the helicopter, checking climb, descent, obstacles, landing and exit.
8. Test ferry restrictions and $150 fee.
9. Buy each property class, enter, change outfit and return outside.
10. Complete each robbery, defend with F/Q, flee and clear wanted; test clinic recovery.
11. Try high/balanced quality, night/day, resizing, map guidance and tab focus changes.
12. Reconnect and verify saved cash, possessions and crime reputation. Confirm disk persistence after a Render redeploy.

The package should be treated as a prototype pending these manual checks.
