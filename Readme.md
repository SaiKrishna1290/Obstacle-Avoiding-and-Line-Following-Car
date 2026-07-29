# Arduino-Based Obstacle Avoiding and Line Following Car

An autonomous robotic car that combines **line following** and **obstacle avoidance** into a single integrated system using an Arduino Uno, IR sensors, and an ultrasonic sensor mounted on a servo motor.

Developed as a Project Exhibition submission for the degree of Bachelor of Technology in Electronics and Communication Engineering, VIT Bhopal University.

---

## Team

| Name | Registration No. |
|---|---|
| Tanya Tanu | 24BEC10116 |
| Papa Karthik Reddy | 24BEC10157 |
| Addepalli Sai Krishnam Raju | 24BEC10165 |

**Supervisor:** Dr. Monica P, Assistant Professor, SEEE, VIT Bhopal University

---

## Overview

Most robotic cars are built for a single purpose — either following a fixed path or avoiding obstacles in open space. This project solves that limitation by integrating both behaviors into one system:

- **Default mode:** Follows a black line on a white surface using IR sensors.
- **Safety override:** If the ultrasonic sensor detects an obstacle within a set threshold, line-following is paused, the car scans left/right using a servo-mounted ultrasonic sensor, turns toward the clearer side, bypasses the obstacle, and resumes line-following.

This makes the robot practical for dynamic, semi-structured environments such as warehouses, delivery paths, and educational demos — not just static tracks or open obstacle courses.

---

## Features

- Autonomous line following on black-tape/white-surface tracks
- Real-time obstacle detection and avoidance (2–30 cm range)
- Servo-based ultrasonic scanning to choose the best avoidance direction
- Seamless switching between line-following and obstacle-avoidance modes
- Low-cost, beginner-friendly, and easily reproducible build

---

## Hardware Components

| Component | Purpose |
|---|---|
| Arduino Uno | Central controller / "brain" |
| Ultrasonic Sensor (HC-SR04) | Obstacle detection |
| IR Sensors (x2) | Line detection |
| Servo Motor (SG90/TowerPro) | Rotates ultrasonic sensor to scan sides |
| L293D Motor Driver | Interfaces Arduino with DC motors |
| DC Motors & Wheels (x4) | Movement / propulsion |
| Chassis | Physical base frame |
| Rechargeable Li-ion Battery Pack | Power supply |
| ON/OFF Switch | Power control |

---

## Circuit Diagram

```
IR Sensors + Ultrasonic Sensor → Arduino Uno → Motor Driver (L293D) → DC Motors → Robotic Car Movement
```

See `Fig 3.1` in the project report for the full wiring diagram (Arduino pin mapping, motor driver connections, and sensor wiring).

**Pin Configuration (from source code):**

| Signal | Arduino Pin |
|---|---|
| Motor 1 Enable (enA) | 10 |
| Motor 1 IN1 | 9 |
| Motor 1 IN2 | 8 |
| Motor 2 IN3 | 7 |
| Motor 2 IN4 | 6 |
| Motor 2 Enable (enB) | 5 |
| Left IR Sensor (L_S) | A0 |
| Right IR Sensor (R_S) | A1 |
| Ultrasonic Echo | A2 |
| Ultrasonic Trigger | A3 |
| Servo Signal | A5 |

---

## Working Principle

1. **Line Following:** IR sensors detect the contrast between a black line and white surface. Based on which sensor detects the line, the Arduino commands the motors to turn left, right, or move straight.
2. **Obstacle Avoidance:** The ultrasonic sensor continuously measures the distance ahead. If an obstacle is detected within the threshold (default: 15 cm), the car stops, sweeps the servo to check the left and right distances, and turns toward the side with more clearance.
3. **Integration:** Line-following is the default behavior; obstacle avoidance temporarily overrides it and hands control back once the path is clear.

---

## Software

- Written in **Embedded C** using the **Arduino IDE**.
- Core logic runs in a continuous loop: read IR sensors → check ultrasonic distance → follow line or trigger avoidance maneuver.
- Full source code is included in the project report (`Arduino Code` section) and can be uploaded directly via the Arduino IDE.

### Key Functions

| Function | Description |
|---|---|
| `Ultrasonic_read()` | Returns distance in cm from the ultrasonic sensor |
| `servoPulse()` | Manually generates a servo control pulse to set angle |
| `Check_side()` | Sweeps servo left/right and records distances |
| `compareDistance()` | Decides turn direction based on left/right distances |
| `forword()`, `backword()`, `turnLeft()`, `turnRight()`, `Stop()` | Motor control primitives |

---

## Getting Started

1. Assemble the chassis, motors, wheels, Arduino, motor driver, IR sensors, ultrasonic sensor, and servo as per the circuit diagram.
2. Install the [Arduino IDE](https://www.arduino.cc/en/software).
3. Open the provided `.ino` sketch (from the project report / repository).
4. Connect the Arduino Uno via USB and select the correct board and port.
5. Upload the code.
6. Power the car using the Li-ion battery pack and place it on a track with a black line on a white surface.
7. Toggle the ON/OFF switch to start.

---

## Results

- **Line-following accuracy:** 90–95% on black tape / white surface tracks
- **Obstacle detection range:** Effective between 2–30 cm
- **Tested scenarios:** Straight tracks, curved paths, single obstacles, and multiple sequential obstacles — all handled successfully
- **Limitation:** IR sensor accuracy decreases slightly under direct sunlight; ultrasonic sensor is less effective on very small objects

---

## Future Scope

- Camera-based computer vision for advanced line/obstacle recognition
- IoT integration for remote monitoring and control
- AI-based adaptive path planning
- GPS integration for outdoor navigation

---

## References

1. Mahor, S., Singh, A., & Gupta, R. (2010). *Design and development of obstacle avoiding robot.* IJERT, 2(3), 45–49.
2. Kumar, A., & Sharma, P. (2015). *Implementation of line follower robot for industrial application.* IEEE ICACCI.
3. Sharma, P., & Verma, R. (2018). *Smart robotic car using ultrasonic and infrared sensors.* IJARCS, 9(5), 201–206.
4. Singh, H., Kaur, M., & Joshi, N. (2020). *Arduino based multi-functional autonomous robot.* IEEE GUCON.
5. [Arduino UNO R3 Datasheet](https://docs.arduino.cc/hardware/uno-rev3)
6. [HC-SR04 Ultrasonic Sensor Datasheet](https://components101.com/)
7. [SparkFun: Line Following with IR Sensors](https://learn.sparkfun.com/tutorials)
8. [L293D Motor Driver IC Datasheet](https://www.ti.com/lit/ds/symlink/l293.pdf)

---

## License

This project was developed for academic purposes as part of a B.Tech Project Exhibition at VIT Bhopal University. Feel free to reference or build upon it for educational use.
