# 🎱 Ball Balancing System

![Project Status](https://img.shields.io/badge/Status-Completed-success)
![Platform](https://img.shields.io/badge/Platform-STM32-blue)
![Language](https://img.shields.io/badge/Language-C%20%7C%20Python-green)
![Library](https://img.shields.io/badge/Library-OpenCV-orange)

## 📖 Project Overview
[cite_start]The **Ball Balancing System** is an automated control project designed to stabilize a white ball on a specific setpoint on a plate[cite: 1, 212]. [cite_start]The system utilizes **Computer Vision** for real-time tracking and a **PID Controller** embedded in an **STM32** microcontroller to adjust the plate's angle via servo motors[cite: 209, 211, 213].

[cite_start]This project was developed by **Group 2 Team 12**[cite: 3].

## 👥 Team Members
| Name | Role |
|------|------|
| **Abdurakhmon Sobitkhanov** | [cite_start]Team Leader & Embedded Systems [cite: 12, 13] |
| **Nihad Hayani** | [cite_start]Control Systems [cite: 15] |
| **Ilyass Elmamouni** | [cite_start]Image Processing [cite: 16] |
| **Mohamed Osman** | [cite_start]Mechanic Design [cite: 17] |
| **Imed Tavil** | [cite_start]Mechanic Design [cite: 19] |
| **Talal Soufi** | [cite_start]Electrician [cite: 18] |

---

## ⚙️ System Architecture

### 1. Mechanical Design
[cite_start]The system uses a **Double Link Joint** mechanism to allow **Pitch & Roll** movements for the top plate[cite: 142, 150].
* [cite_start]**Design:** Symmetrical distribution of arms to ensure balanced movement[cite: 145].
* [cite_start]**Actuation:** Two Servo motors mounted on orthogonal axes[cite: 147].
* [cite_start]**Material:** 3D printed parts, manually adjusted for smooth joint movement[cite: 155, 157].



[Image of double link joint mechanism]


### 2. Electrical & Embedded System
* [cite_start]**Microcontroller:** STM32F103C8T6 (Blue Pill)[cite: 28, 31].
* [cite_start]**Actuators:** SG90 Small Servos [cite: 32] [cite_start](Torque: ~0.1766 Nm [cite: 165]).
* [cite_start]**PCB:** Custom designed board for signal distribution and power management[cite: 21, 22].
* [cite_start]**Communication:** UART Protocol to receive coordinates from the PC[cite: 213].



[Image of STM32 microcontroller pinout]


### 3. Image Processing (Vision System)
[cite_start]The vision system captures video in real-time using **OpenCV** to locate the ball[cite: 211].
* [cite_start]**Calibration:** Converts Pixel coordinates to Centimeters automatically using a reference black square (16x16 cm)[cite: 212, 216].
* [cite_start]**Tracking:** Isolates the white color, applies morphological filters to remove noise, and calculates the center[cite: 219].
* [cite_start]**Output:** Sends coordinates ($X, Y$) via Serial (UART) to the STM32 every 0.5 seconds[cite: 213, 229].

### 4. Control System (PID)
[cite_start]A **PID Controller** is implemented on the STM32 to calculate the required servo angles based on the error between the ball's current position and the setpoint (center)[cite: 127].
* [cite_start]**Mathematical Model:** Based on Lagrangian mechanics ($L = E_k - E_p$)[cite: 110].
* [cite_start]**Logic:** 1. Read Sensor Data (UART)[cite: 182].
    2. [cite_start]Check valid data[cite: 184].
    3. [cite_start]Calculate PID output ($u(t)$)[cite: 189].
    4. [cite_start]Actuate Servos[cite: 190].



[Image of PID controller block diagram]


---

## 🚀 How It Works
1.  [cite_start]**Detection:** The camera detects the white ball's position[cite: 218].
2.  [cite_start]**Processing:** Python script converts pixels to real-world coordinates ($cm$) relative to the center[cite: 221].
3.  [cite_start]**Communication:** Coordinates are sent to the STM32 via USB-TTL (UART)[cite: 229, 237].
4.  [cite_start]**Computation:** The STM32 computes the error and processes it through the PID algorithm ($K_p, K_i, K_d$)[cite: 203].
5.  [cite_start]**Action:** Servos adjust the plate angles to bring the ball back to the center (equilibrium)[cite: 149].

---

## 🛠️ Challenges & Solutions
* [cite_start]**Joint Placement:** The hinge location had to be redefined accurately to achieve stable balance[cite: 151, 152].
* [cite_start]**Servo Positioning:** Servos were repositioned relative to the center to allow better control over Pitch & Roll[cite: 153, 154].
* [cite_start]**3D Printing:** Tolerance issues required manual drilling and adjustments for smooth hinge operation[cite: 155, 157].

---

## 💻 Usage Commands (Vision System)
When running the Python vision script:
* [cite_start]Press **`r`**: Recalibrate the system (if camera position changes)[cite: 233].
* [cite_start]Press **`q`**: Quit the program safely[cite: 234].

---

## 📝 Mathematical Model
The system dynamics were derived using the Lagrangian equation:
[cite_start]$$L = \frac{6}{5}m\dot{x}^2 + mg \sin(\theta)$$ [cite: 117]
Where the equation of motion is derived as:
[cite_start]$$\frac{5}{3}m\ddot{x} - mg \sin(\theta) = 0$$ [cite: 120]

---
[cite_start]*University Project - Group 2 Team 12* [cite: 3]
