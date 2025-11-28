# 🎱 Ball Balancing System

![Project Status](https://img.shields.io/badge/Status-Completed-success)
![Platform](https://img.shields.io/badge/Platform-STM32-blue)
![Language](https://img.shields.io/badge/Language-C%20%7C%20Python-green)
![Library](https://img.shields.io/badge/Library-OpenCV-orange)

## 📖 Project Overview
The **Ball Balancing System** is an automated control project designed to stabilize a white ball on a specific setpoint on a plate. The system utilizes **Computer Vision** for real-time tracking and a **PID Controller** embedded in an **STM32** microcontroller to adjust the plate's angle via servo motors.

This project was developed by **Group 2 Team 12**.

## 👥 Team Members
| Name | Role |
|------|------|
| **Abdurakhmon Sobitkhanov** | Embedded Systems |
| **Nihad Hayani** | Control Systems |
| **Ilyass Elmamouni** | Image Processing |
| **Mohamed Osman** | Mechanic Design |
| **Imed Tavil** | Mechanic Design |
| **Talal Soufi** | Electrician |

---

## ⚙️ System Architecture

### 1. Mechanical Design
The system uses a **Double Link Joint** mechanism to allow **Pitch & Roll** movements for the top plate.
* **Design:** Symmetrical distribution of arms to ensure balanced movement.
* **Actuation:** Two Servo motors mounted on orthogonal axes.
* **Material:** 3D printed parts, manually adjusted for smooth joint movement.

### 2. Electrical & Embedded System
* **Microcontroller:** STM32F103C8T6 (Blue Pill).
* **Actuators:** SG90 Small Servos (Torque: ~0.1766 Nm).
* **PCB:** Custom designed board for signal distribution and power management.
* **Communication:** UART Protocol to receive coordinates from the PC.

### 3. Image Processing (Vision System)
The vision system captures video in real-time using **OpenCV** to locate the ball.
* **Calibration:** Converts Pixel coordinates to Centimeters automatically using a reference black square (16x16 cm).
* **Tracking:** Isolates the white color, applies morphological filters to remove noise, and calculates the center.
* **Output:** Sends coordinates (X, Y) via Serial (UART) to the STM32 every 0.5 seconds.

### 4. Control System (PID)
A **PID Controller** is implemented on the STM32 to calculate the required servo angles based on the error between the ball's current position and the setpoint (center).
* **Mathematical Model:** Based on Lagrangian mechanics.
* **Logic:**
    1. Read Sensor Data (UART).
    2. Check valid data.
    3. Calculate PID output.
    4. Actuate Servos.

---

## 🚀 How It Works
1.  **Detection:** The camera detects the white ball's position.
2.  **Processing:** Python script converts pixels to real-world coordinates (cm) relative to the center.
3.  **Communication:** Coordinates are sent to the STM32 via USB-TTL (UART).
4.  **Computation:** The STM32 computes the error and processes it through the PID algorithm.
5.  **Action:** Servos adjust the plate angles to bring the ball back to the center (equilibrium).

---

## 🛠️ Challenges & Solutions
* **Joint Placement:** The hinge location had to be redefined accurately to achieve stable balance.
* **Servo Positioning:** Servos were repositioned relative to the center to allow better control over Pitch & Roll.
* **3D Printing:** Tolerance issues required manual drilling and adjustments for smooth hinge operation.

---

## 💻 Usage Commands (Vision System)
When running the Python vision script:
* Press **`r`**: Recalibrate the system (if camera position changes).
* Press **`q`**: Quit the program safely.

---

## 📝 Mathematical Model
The system dynamics were derived using the Lagrangian equation:

$$L = E_K - E_P$$

Where the equation of motion is derived as:

$$\frac{5}{3}m\ddot{x} - mg \sin(\theta) = 0$$

---
*University Project - Group 2 Team 12*
