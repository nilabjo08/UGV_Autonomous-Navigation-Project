# UGV Autonomous Navigation — Assignment README

## 1. Project overview
This assignment presents a system design for an **autonomous Unmanned Ground Vehicle (UGV)**. An operator selects a destination on a map, and the UGV plans a safe route, navigates while avoiding obstacles, confirms arrival, and can perform a task.

## 2. Proposed hardware
- **2D 360° LiDAR:** obstacle detection, mapping and localization.
- **Camera:** live visual monitoring and optional target verification.
- **Wheel encoders + IMU:** odometry and heading feedback.
- **Motor controller + MCU:** wheel-speed control using PID, encoder feedback and PWM.
- **Onboard computer:** runs perception, planning and the operator interface.
- **Touchscreen / remote GUI:** displays the map, camera and mission status.

These are proposed design components, not a claim that the HTML demo is connected to physical hardware.

## 3. Software architecture and workflow
The design uses **ROS 2** nodes and separates the system into layers:
1. **Perception:** LiDAR scan processing, camera stream and sensor data.
2. **Mapping/localization:** SLAM builds the occupancy map; odometry and IMU help estimate robot pose.
3. **Navigation:** a global planner (A*) finds a route; a local planner (DWA) adjusts motion around nearby obstacles.
4. **Motor interface:** converts linear/angular velocity commands into left/right wheel commands.
5. **Mission manager + GUI:** handles destination selection, mission states, status and task execution.

Typical flow: **Mapping/Idle → Planning → Navigating → Arrived → Action → Idle**. If progress fails, the robot enters recovery and may report failure. The operator can cancel a mission; a hardware emergency stop overrides normal operation.

## 4. Important control and safety concepts
- Differential-drive kinematics convert vehicle velocity into left and right wheel speeds.
- Each wheel uses closed-loop PID speed control with encoder feedback.
- A command watchdog, LiDAR-based stop/slow zones and a hardware E-stop provide safety layers.
- Arrival is confirmed using position/heading tolerance and a short settling period.

## 5. Validation approach
The design proposes a staged process: **Gazebo simulation → recorded sensor-data (rosbag) replay → low-speed field testing**. The numerical values in the assignment are illustrative design parameters and must be validated against the actual robot.

## 6. Interview summary
“I designed the system concept for a differential-drive UGV. The operator selects a goal on the map. LiDAR and SLAM provide mapping and localization, the global and local planners generate and adjust a safe path, and the motor controller tracks wheel-speed commands using PID and encoder feedback. I also considered fault recovery, watchdog protection and emergency stopping. The assignment is a system-design proposal; the accompanying HTML is a browser-based simulation demo, not a physical ROS 2 implementation.”

## 7. Key terms
**UGV:** Unmanned Ground Vehicle · **ROS 2:** Robot Operating System 2 · **SLAM:** Simultaneous Localization and Mapping · **EKF:** Extended Kalman Filter · **A*:** graph-search path planner · **DWA:** Dynamic Window Approach · **PID:** Proportional–Integral–Derivative control · **PWM:** Pulse-Width Modulation · **E-stop:** emergency stop.
