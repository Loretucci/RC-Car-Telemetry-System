# RC-Car-Telemetry-System
Designed and implemented a serial telemetry interface for a 1:8 scale autonomous rover, es- tablishing communication between Teensy 4.1 and Arduino boards via UART protocol using Model-Based Design in Simulink

# Autonomous Rover Telemetry System

## Project Overview
This repository contains the software and Simulink models developed for my **Bachelor's Thesis** in *Electronics and Telecommunications Engineering* at the University of Florence.

The project focuses on designing and testing a robust **real-time telemetry system** for a 1:10 scale autonomous RC car. The system enables reliable data transmission from the vehicle's onboard computer to a ground station for analysis, visualization, and closed-loop control.

## Objectives
* **Data Acquisition:** Reading IMU sensor data (Accelerometer/Gyroscope), motor RPM, and steering inputs.
* **Reliable Communication:** Establishing a wireless UART link between the rover and the base station.
* **Data Integrity:** Implementing a custom communication protocol with **Checksum validation** to handle packet loss and corruption.
* **Real-Time Monitoring:** Visualizing vehicle dynamics in **MATLAB/Simulink**.

## System Architecture

### 1. Hardware Setup
* **Rover Unit (TX):**
    * **Teensy 4.0:** Main microcontroller processing sensor data.
    * **Sensors:** IMU (Acc/Gyro), Hall Effect Sensors (RPM).
    * **Transmitter:** UART Wireless Module.
* **Ground Station (RX):**
    * **Arduino Mega:** Acts as the receiver bridge.
    * **PC:** Running MATLAB/Simulink for processing.

### 2. Communication Protocol
To ensure robustness against noise and transmission errors, a custom binary packet structure was designed:
| Start Byte | Payload (Sensors & Controls) | Checksum |
| :---: | :---: | :---: |
| `0xFF` | 16 bytes (Int16 array) | XOR Checksum |

* **Payload Data:** Acceleration (X,Y,Z), Angular Velocity (X,Y,Z), Throttle, Steering.
* **Error Handling:** A custom Simulink S-Function computes and verifies the checksum. Corrupted packets are automatically discarded to prevent control glitches.

## Technologies Used
* **MATLAB & Simulink (R2022b)**
* **Simulink Support Package for Arduino Hardware**
* **C/C++** (Embedded firmware for Teensy)
* **Hardware:** Teensy 4.0, Arduino Mega 2560

## Repository Structure
* `Simulink_Model/`: Contains the `.slx` files for the receiver and data processing.
* `Teensy_Firmware/`: C++ code for sensor acquisition and UART transmission.
* `Docs/`: Documentation and wiring diagrams.

## Results
The system was stress-tested by simulating transmission interruptions and noise. The implemented checksum algorithm successfully identified 100% of corrupted packets, ensuring that only valid telemetry data was plotted in the Simulink scope.

---
*Author: Lorenzo Tucci*
*Bachelor Thesis - University of Florence*
