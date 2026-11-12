# Autonomous UGV Navigation & Ground Station

A browser-based **Unmanned Ground Vehicle (UGV) ground-station simulation** and accompanying system-design proposal. The project demonstrates how an operator can select a destination on a LiDAR-style map, monitor a simulated mission, inspect navigation and motor-control telemetry, and test fault-handling scenarios.

<p align="center">
  <a href="https://nilabjo08.github.io/UGV_Autonomous-Navigation-Project/"><strong>🚀 Open Live Ground Station Demo</strong></a>
  &nbsp; · &nbsp;
  <a href="UGV_Autonomous_Navigation_Professional%20(1).pdf">📄 Read the Technical Design PDF</a>
</p>

> **Note:** The live demo is a self-contained browser simulation. It is not connected to a physical UGV, ROS 2 network, LiDAR, camera, or motor controller. Hardware and ROS 2 elements in the design document describe a proposed system architecture. Simulation parameters are illustrative and are not validated hardware performance results.

## Project contents

| File | Description |
|---|---|
| [`index.html`](index.html) | Interactive browser-based ground-station simulation and GitHub Pages homepage |
| [`UGV_Autonomous_Navigation_Professional (1).pdf`](UGV_Autonomous_Navigation_Professional%20(1).pdf) | Technical design note covering architecture, mapping, navigation, motor control and safety |
| `README.md` | Project overview, live demo link and documentation |

## Demo features

- **Map and destination selection:** Click or tap the map to set or change a destination.
- **Mission scenarios:** Run nominal navigation, obstacle, no-route, LiDAR-dropout and motor-link-loss scenarios.
- **Navigation visualization:** Inspect the simulated robot pose, route, goal distance, map exploration and recovery events.
- **Camera panel:** View the simulated camera feed.
- **Motor-control view:** Inspect wheel-speed response, PID metrics, step tests and optional CSV log loading.
- **Fault and safety controls:** Inject selected faults, cancel or resume a route, use manual-drive controls, and test the simulated E-stop.
- **Telemetry:** Review topic rates, data age, subsystem health and the event log; export the log as CSV.

## Proposed system architecture

The accompanying design note describes a layered ROS 2 architecture:

1. **Perception:** 2D LiDAR scan processing and camera data.
2. **Mapping and localization:** SLAM, occupancy-grid mapping, wheel odometry, IMU and EKF fusion.
3. **Navigation:** A* global path planning, costmaps and DWA local obstacle avoidance.
4. **Motor interface:** Differential-drive kinematics and wheel-speed commands.
5. **Low-level control:** MCU-based encoder feedback, PID speed loops and PWM motor control.
6. **Mission and operator interface:** Goal selection, mission-state handling, status display and destination actions.

The proposed validation path is **Gazebo simulation → rosbag replay → staged, low-speed field testing**.

## How to run locally

1. Download or clone this repository.
2. Open `index.html` in a modern web browser.
3. Click or tap the map to set a destination, then run one of the demo scenarios.

No build step or package installation is required for the standalone HTML demo. An internet connection may be needed to load the externally hosted fonts.

## GitHub Pages deployment

GitHub Pages is configured to deploy from the `main` branch and the repository root (`/(root)`). The simulation file is named **`index.html`**, so the project homepage opens the interactive ground-station demo directly:

**[Open the live UGV Ground Station](https://nilabjo08.github.io/UGV_Autonomous-Navigation-Project/)**

If you update the simulation, commit the changes to the `main` branch and allow GitHub Pages to finish deploying. The root URL above remains the live demo address.

## Project scope

This repository contains a system-design assignment, a static HTML/JavaScript simulation and supporting documentation. It does not include a deployed ROS 2 package, physical robot firmware, hardware drivers, or a real sensor connection.

---

**Author:** [nilabjo08](https://github.com/nilabjo08)  
**Repository:** [UGV_Autonomous-Navigation-Project](https://github.com/nilabjo08/UGV_Autonomous-Navigation-Project)
