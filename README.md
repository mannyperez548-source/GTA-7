# COASTLINE EXPANDED — Islands & Ambition

A browser-based, stylized 3D online sandbox. This is version 2 of the included Coastline prototype, expanded with a larger county, islands, property catalog, aircraft, jobs and a fictional criminal progression loop. No real-money transactions or PvP combat.

## Quick start

Requires Node.js 20 or newer, an internet connection for browser-side CDN libraries, a modern WebGL-capable desktop browser, mouse and keyboard.

```sh
npm install
npm start
```

Open http://localhost:3000. Enter a name, join, and use the coral Courier marker beside spawn. You begin with $1,200. Two $650 deliveries make a $2,400 Sunrunner affordable. Use Tab to browse the collection, Jobs to locate work, and H for full controls.

## What is actually implemented

| Content | Count | Notes |
| --- | ---: | --- |
| Cars | 20 | Named procedural variants: compact, coupe, GT, supercar, convertible, SUV, pickup, van, classic, rally, sedan, limousine, buggy, hypercar, wagon, muscle, off-road, roadster, luxury and shuttle bodies; different caps and prices |
| Boats | 5 | Runabout, yacht, jet ski, fishing boat, catamaran |
| Houses | 30 | Original 3 homes plus 27 suburban residences; several exterior variants |
| Apartments | 5 | Purchasable units represented by separate towers |
| Penthouses | 3 | Purchasable towers with rooftop details |
| Planes | 2 | Skylark Trainer and Nimbus Executive Jet |
| Helicopters | 1 | Kestrel with animated main and tail rotors |
| Legal jobs | 15 | Route, multi-stop, timed work, defense, marine and aviation tasks |
| Criminal contracts | 3 | Store raid, container heist, civic vault raid |
| Offshore islands | 3 | Beacon, Aurelia and Crescent |
| Airports | 2 | Mainland international airport and Aurelia airfield |
| Marinas / ferry destinations | 4 | Mainland and one landing on each island |

The nominal playable bounds are approximately 2.13 km east-west by 1.6 km north-south; much of that is ocean. The expanded mainland is roughly 820 by 1,420 metres. These are game-space dimensions, not real-world locations.

Other features: private furnished property interiors, clothing equipment, server-side balances/purchases/earnings, JSON saves, minimap and full map, point-of-interest guidance, shared player movement, text chat, camera orbit/zoom, a 24-minute synchronized day, custom animated ocean, sky scattering, stars/moon, moving clouds, palm sway, emissive nighttime lighting, soft shadows, tone mapping and bloom. Repeated building windows use instancing to reduce draw calls. Balanced mode disables expensive effects and lowers render resolution.

## Legal careers

1. Courier Dispatch — $650 parcel delivery; no vehicle required.
2. Taxi Dispatch — $1,000 county trip in an owned car.
3. Ocean Freight — $2,200 offshore route in a boat.
4. Sunset Pizza — $800 neighborhood delivery.
5. Roadside Mechanic — $1,100 timed repair at a destination.
6. County Sanitation — $1,500 three-stop collection route in a car.
7. Harbor Construction — $1,250 timed on-site shift.
8. Emergency Response — $1,800 drive-and-assist call.
9. Event Security — $2,100 protect a zone against fictional NPC raiders.
10. Pelican Fishing — $1,700 hold position offshore.
11. Coastguard Rescue — $2,400 reach and assist at a beacon.
12. Island Air Cargo — $4,800 fly a plane to Aurelia and land.
13. Rotor Charter — $3,900 land a helicopter on Beacon Island.
14. Coastal Photographer — $1,300 three viewpoint stops.
15. County Bus Route — $2,600 four-stop route; any owned car accepted in this prototype.

Use the Jobs tab to locate a dispatch. At a nearby job marker, press E and choose **Start** on the desired card. This lets you choose among jobs sharing a dispatch area. Timed tasks advance automatically while stationary within their destination ring and in the required transport mode. A route's required mode is shown in the card.

## Fictional criminal pathway and defense

Approach a red marker on foot and press E. A raid sets a wanted level and spawns personal police-like mission pursuers. Stay inside the zone until the timer fills, then escape to the gold hideout marker to receive the payout. Store raids pay $1,600, container heists $3,400, vault raids $6,200. Completed crimes increment a persistent crime reputation counter. Container heists unlock after 2 completed raids; vault raids unlock after 5. Your reputation is shown in Collection.

F fires a non-graphic auto-targeted stun tool at the nearest mission NPC within 32 metres. Hold Q to reduce incoming damage. NPCs have hit points, proximity damage and a temporary stun state; there is no blood, weapon inventory, player-vs-player combat or real-world criminal guidance. After finishing/cancelling the mission, stay more than 85 metres from active pursuers or stun them all for 24 seconds to clear the wanted level. Contacts have a 90-second cooldown. At zero health you return to the clinic and pay a capped-by-balance fine. Wanted level and contact cooldown persist in the save; logging out does not intentionally clear them.

## Vehicles, aircraft and property

Purchase in the collection/shop menu, then use **Spawn & enter**. Cars spawn on dry land; boats require a nearby marina; aircraft require an airport aviation area. Ferry tickets cost $150, bought from the Travel tab while standing at a marina on foot, with no active job or wanted level.

For planes, W accelerates; get above 22 m/s, then hold R to climb. A/D turns, C descends, Space brakes. Helicopters can climb from a hover using R. Maximum altitude is 250 metres. Descend and slow down over dry land before pressing V to exit. Physics are arcade-style, not an aviation simulator. Aircraft cannot be exited in midair.

Purple property markers open purchased private furnished interiors. E near the interior front door exits. House exteriors have several sizes/roof treatments; apartment and penthouse towers have different heights. Interiors share a room layout with type-specific styling, rather than 38 individually designed floor plans. Boats and aircraft do not have walkable interiors.

## Controls

| Input | Action |
| --- | --- |
| WASD / arrows | Walk / accelerate / steer |
| Shift | Sprint / boost |
| Space | Brake |
| Mouse drag / wheel | Orbit / zoom camera |
| E | Interact / choose a nearby dispatch / leave home |
| V | Exit vehicle, or open collection while on foot |
| R / C | Aircraft climb / descend |
| F / hold Q | Stun nearest mission NPC / guard |
| Tab | Collection and shops |
| M | Expand map |
| T | Chat |
| H | Help and graphics settings |
| Esc | Close menu |

## GitHub and Render

Push the extracted project contents to a GitHub repository (package.json should be at the repository root). On Render choose **New → Blueprint**, connect the repository, and apply render.yaml. Alternatively create a Node web service with build command `npm install` and start command `npm start`. PORT comes from Render. The browser uses secure WebSockets automatically under HTTPS; `/health` returns `ok`.

IMPORTANT: the default free-plan configuration is suitable for trying the prototype, not durable saves. Use a plan that supports persistent disk storage, mount a disk, and set DATA_DIR to that mount directory to preserve accounts across redeploys. Otherwise account files can be lost. Back up the account JSON regularly. Use one server process/replica; there is no shared database or cross-server replication.

Anonymous account keys live in browser local storage. Do not clear local storage if you want to keep using the same device profile. Open separate browser profiles/private sessions for multiplayer testing; a profile is limited to one active connection.

## Tests

```sh
npm run check
npm test
```

Parser checks cover all runtime JavaScript. The included server test uses a mocked WebSocket transport, a fake clock, a temporary account file, and a real local HTTP health check. It exercises catalog totals, courier rewards, duplicate purchases, movement distance rejection, vehicle/boat/aircraft spawning, aircraft exit rules, raid-to-escape progression, wanted clearance, ferry fees and JSON persistence. It does NOT validate WebSocket handshake/framing, real network performance, visual rendering, shader compilation, or Render deployment.

Run the manual checklist in VALIDATION.md before inviting players.

## Limitations and production readiness

This is an expanded procedural sandbox starter, not a finished AAA game/MMO. Shapes are generated in code and share construction patterns; they are not licensed photorealistic vehicle or architecture assets. Traffic is decorative and does not collide. Personal mission NPCs are not shared world entities. Home interiors are private; other players see your exterior position. No touch controls, full pedestrian population, building editor, destructible environment, sound design, detailed damage model, PvP, airline simulation, or unique narrative campaigns are included. The 15 job roles reuse route/timer/defense mechanics rather than each having a bespoke simulation.

The service uses anonymous bearer-like device keys and JSON storage. Server checks are prototype-grade, not comprehensive anti-cheat: the browser still simulates physics and geography. Add secure authentication, a durable transactional database, stronger authoritative simulation, abuse protection, monitoring and moderation before a serious public launch. Do not use this account system for payments or sensitive data. No security audit has been performed.

## Libraries and assets

Node.js + ws server; Three.js 0.170 ES modules with built-in postprocessing. Procedural meshes, textures and UI artwork are created by the project. Three.js loads from cdn.jsdelivr.net, with DM Sans and Space Grotesk loaded from Google Fonts. Internet access to those hosts is required. To self-host everything, vendor the Three.js files and fonts and edit the import map/stylesheet. Retain relevant dependency licenses when redistributing. The project code is MIT licensed.
