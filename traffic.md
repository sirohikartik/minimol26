# Problem Statement: Autonomous Intersection — Decentralized Multi-Agent Traffic Control

## Objective
Program autonomous driving agents for **20 vehicles** navigating a busy 4-way intersection controlled by dynamic traffic lights.

Each vehicle operates as an **independent decentralized agent**. Vehicles must obey traffic laws, prevent collisions, avoid deadlocks, and maximize throughput across the intersection.

---

## Frontend & Visualization Mandate
* **Runtime:** Runs directly in a standard web browser (HTML/CSS/JavaScript).
* **Libraries Allowed:** Any JavaScript library of your choice (e.g., HTML5 Canvas, p5.js, PixiJS, Three.js, Babylon.js, Phaser, or D3/SVG).
* **Dimension & Style:** Teams are free to render the simulation as a **2D top-down view** or an interactive **3D perspective scene**.
* **Visual Requirements:**
  * Must visually render the 4-way intersection, traffic lanes, moving cars, and dynamic traffic light signals (Red, Yellow, Green).
  * Must display a real-time HUD / metrics overlay showing: Collision counter (must be 0), active vehicles, and total vehicles safely cleared.

---

## The Core Constraint: Strict Local Observability
**No global coordinates, central coordinator, or omniscient map data is permitted.**

Each car agent receives **only local sensor telemetry**:
1. **Front Sensor:** Distance and relative velocity of the vehicle directly ahead.
2. **Rear Sensor:** Distance and relative velocity of the vehicle directly behind.
3. **Side / Blind-Spot Sensors:** Proximity of adjacent vehicles in left/right lanes.
4. **Traffic Signal Sensor:** Current state of the traffic light facing the vehicle's active lane (`RED`, `YELLOW`, or `GREEN`) and distance to the intersection stop line.

Agents cannot query other vehicles' planned routes, destinations, or global positions.

---

## Hard Requirements
1. **Zero Collisions:** Under no circumstance may any vehicle make physical contact with another vehicle.
2. **Traffic Law Compliance:**
   * Stop behind the stop line on `RED`.
   * Obey safe stopping distance rules on `YELLOW` (stop if safe, clear if past point-of-no-return).
   * Maintain safe following distance (Time-to-Collision > threshold).
   * Do not block the intersection box on yellow/red (no gridlocking).
3. **Decentralized Decision-Making:** Every vehicle executes its own independent decision loop per simulation tick based strictly on its local sensor readings.
4. **Throughput Efficiency:** Vehicles must not freeze indefinitely. Cars must cross the intersection safely and efficiently when right-of-way is clear.

---

## Strictly Prohibited
* **NO Global State Access:** Agents querying the simulation world object for positions, speeds, or intentions of vehicles outside their immediate local sensor ranges.
* **NO Central Traffic Dispatcher:** No single "god-mode" controller telling all 20 cars when to move or stop.
* **NO Teleportation or Instant Braking:** Vehicles are subject to physical acceleration and deceleration limits; cars cannot stop instantaneously from full speed.
* **NO Lane Hopping:** Vehicles must respect lane boundaries and follow their designated straight/turn lanes.
