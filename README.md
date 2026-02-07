# Project introduction


To access all the information about this project, please use the link:  
[https://oshwlab.com/iosnaaente/v3s_idf_s2](https://oshwlab.com/iosnaaente/v3s_idf_s2)

To edit the project, use:  
[https://pro.easyeda.com/editor#id=](https://pro.easyeda.com/editor#id=)


This project is a **VSSS (Very Small Size Soccer) autonomous robotic platform**, designed for research, development, and competition in robotic soccer environments.  
This version is based on the **ESP32-S2-MINI** module and integrates closed-loop DC motor control, inertial sensing, wireless communication, and on-board debugging interfaces.

The robot is designed to operate reliably under dynamic conditions typical of VSSS matches, including rapid acceleration, frequent direction changes, and wireless command reception with low latency. The hardware architecture prioritizes modularity, robustness, and ease of replication.

---

# Project function

This project implements a complete mobile robotic platform with the following core functions and application scenarios:

- Differential drive control using **two N20 DC motors with quadrature encoders**, enabling precise velocity and position feedback.
- Closed-loop motion control based on encoder feedback and inertial data.
- Real-time orientation and angular velocity estimation using an **MPU6050 IMU** (accelerometer + gyroscope).
- Wireless bidirectional communication using a **2.4 GHz nRF24L01 SPI radio**, suitable for multi-robot coordination and external strategy control.
- On-board **OLED display (128×32)** for debugging, telemetry visualization, and system state monitoring.
- Power management designed for battery operation, with voltage protection and regulation to ensure stable operation during high current motor loads.
- Designed specifically for **VSSS robotic soccer**, but adaptable for general-purpose mobile robotics, swarm robotics, and educational platforms.

---

# Project Parameters

- **Main controller:**  
  ESP32-S2-MINI  
  - Single-core Xtensa LX7 @ up to 240 MHz  
  - Native USB support  
  - 3.3 V logic level  

- **Motor system:**  
  - 2× N20 DC motors with integrated quadrature encoders  
  - Differential drive configuration  
  - Controlled via **TB217A dual H-bridge motor driver**

- **Inertial sensing:**  
  - MPU6050 (3-axis accelerometer + 3-axis gyroscope)  
  - I²C interface  

- **Wireless communication:**  
  - nRF24L01+ 2.4 GHz transceiver  
  - SPI interface  
  - Low latency, multi-node capable  

- **Display:**  
  - OLED 128×32 pixels  
  - I²C interface  
  - Used for debug and system feedback  

- **Power architecture:**  
  - Battery input with **reverse polarity protection diode**  
  - **XL6009 boost converter** to regulate motor supply to a stable 12 V  
  - **Buck converter** to generate 5 V rail  

- **Typical operating voltages:**  
  - Motor rail: 12 V  
  - Logic rail: 5 V / 3.3 V  

---

# Principle analysis (Hardware description)

The hardware design is divided into the following functional blocks:

## 1. Power Supply and Protection
The robot is powered by a battery pack connected through a **reverse polarity protection diode** to prevent damage from incorrect battery insertion.  
An **XL6009 boost converter** is used to maintain a stable 12 V supply for the motors, ensuring consistent performance even as battery voltage drops.  
A buck converter generates the required logic supply rails for the control electronics.

## 2. Main Control Unit
The **ESP32-S2-MINI** acts as the central processing unit, handling:
- Motor control algorithms
- Encoder signal processing
- IMU data acquisition
- SPI and I²C communications
- System-level decision making

## 3. Motor Driver and Actuation
A **TB217A dual H-bridge motor driver** controls both N20 motors, allowing bidirectional control with PWM speed modulation.  
Encoder signals from the motors are fed back to the ESP32, enabling closed-loop velocity and position control.

## 4. Sensor System
The **MPU6050 IMU** provides acceleration and angular velocity data, which can be fused with encoder data for improved motion estimation and control stability.

## 5. Communication and Debug
Wireless communication is implemented via an **nRF24L01 SPI transceiver**, enabling low-latency command and telemetry exchange.  
An **OLED display** provides real-time debug information such as system state, sensor readings, and communication status.

---

# Software code

The firmware is developed using **ESP-IDF** and implements:

- Real-time motor control loops
- Encoder interrupt handling
- IMU data acquisition and filtering
- SPI communication with nRF24L01
- Debug output to OLED display

The complete source code, including firmware and system configuration, is available at:

[https://github.com/TauraBots/V3S_IDF_S2_Firmware](https://github.com/TauraBots/V3S_IDF_S2_Firmware)

---

# Announcements

- Keep SPI traces to the nRF24L01 short and well-routed to avoid communication instability.
- Proper decoupling capacitors near the ESP32-S2, IMU, and radio module are essential for reliable operation.
- The boost converter should be tested under peak motor load conditions to ensure voltage stability.
- Ensure correct grounding and current return paths for motor and logic supplies.

---

# Assembling processes

1. Solder all SMD components (power regulation, ESP32-S2 module, IMU, passive components).
2. Assemble and solder the motor driver and motor connectors.
3. Mount the nRF24L01 module and OLED display.
4. Connect motors and battery.
5. Flash firmware via USB and perform initial power-on tests.
6. Calibrate IMU and verify encoder readings.

---

# Finished product display

After assembly, the final product is a compact, fully autonomous VSSS robot featuring:

- Integrated motors and encoders
- On-board processing and sensing
- Wireless communication
- Native USB programming and debugging
- Real-time debug display


# Author

**Designed by:** Bruno Gabriel Flores Sampaio  
**Date:** October 2025  


## Authorship and Attribution Notice

This project is provided for use in **academic research, scientific publications, competitions, and public demonstrations**.

**Authorship attribution is mandatory** for any use that results in:

- Academic articles, papers, theses, or dissertations  
- Technical reports or research documentation  
- Robotics competitions and official team descriptions  
- Public presentations, showcases, or media mentions  

In such cases, the author **must be credited** as:

- **Author:** Bruno Gabriel Flores Sampaio  
- **Citation format:** Sampaio, F.; Bruno, G.  
- **Email:** bruno.bielsam.1205@hotmail.com  
- **Institution:** UFSM — Universidade Federal de Santa Maria  

Failure to provide proper attribution is **not permitted** under the terms of use of this project.
