# EE_bachelor_thesis-En(Mar 2024 – Jun 2024)

&nbsp;

## 🧠 Robotic Arm Control Using Deep Learning-Based Electrooculogram

&nbsp;

## 🔗 References & License

1. **A Method of EOG Signal Processing to Detect the Direction of Eye Movements**  
   - Manuel Merino, Octavio Rivera, Isabel Gómez, Alberto Molina, Enrique Dorronzoro  
   - Electronic Technology Department, University of Seville, Spain  
   - https://ieeexplore.ieee.org/document/5632116

2. **ArduinoTensorFlowLiteTutorials / GestureToEmoji**  
   - https://github.com/arduino/ArduinoTensorFlowLiteTutorials/tree/master/GestureToEmoji

3. **AUTODESK Instructables - 3D Printed Robot Arm by Beaconsfield**  
   - https://www.instructables.com/3D-Printed-Robot-Arm

&nbsp;

## 📑 Table of Contents

1. [📌 Project Overview](#1--project-overview)  
2. [🔧 Components](#2--components)  
3. [💻 Technologies Used](#3--technologies-used)  
4. [🧭 System Workflow](#4--system-workflow)  
5. [💻 How to Run Code](#5--how-to-run-code)  
6. [📷 Demonstration Videos & Images](#6--demonstration-videos--images)  
7. [🌟 Expected Impact / Limitations & Improvements](#7--expected-impact--limitations--improvements)

&nbsp;

## 1. 📌 Project Overview

As aging populations increase, there is growing difficulty in caring for elderly individuals.  
For people with impaired arm mobility, even basic daily activities can be a challenge.  
This project aims to develop an **eye-movement-based robotic arm control system using EOG sensors**  
to allow users to pick up food using only eye movements—without using their arms.

- When the user wears the EOG sensor, real-time signals corresponding to eye direction and intensity are collected  
- Data is sent to an Arduino board, processed through a deep learning model to classify gaze direction  
- The predicted gaze direction is then used to **control a 3D-printed robotic arm** to grab food

&nbsp;

### 🎯 Objectives

- Develop a user-friendly interface to improve **independence for elderly and mobility-impaired individuals**
- Enable desired actions with **simple eye movements (left/right/blink)**  
- Example: left/right gaze → arm moves, **strong blink** → grab object

> Most recent EOG studies focus on signal processing and gaze tracking.  
> **Real-time hardware integration is limited**.  
> This project integrates **EOG signal processing + AI model training + real robot control**, making it highly significant.

&nbsp;

### 🏭 Existing Technology & Expandability

- Integrated **EOG + Arduino + deep learning model** to create a low-cost, efficient system  
- Used **TensorFlow Lite** to run lightweight models on embedded systems in real time  
- Designed and 3D-printed a robotic arm for **customizable user applications**

Future applications can be extended to **collaborative robots (Cobots)** for:  
- Rehabilitation and assistive devices  
- **Touchless smart-home control systems** and industrial automation

[🔝 Back to Top](#-table-of-contents)

&nbsp;

## 2. 🔧 Components

| Component            | Description                                                                 | Image |
|---------------------|-----------------------------------------------------------------------------|-------|
| **Arduino Nano 33 BLE Sense** | Receives EOG sensor signals, classifies gaze direction using a deep learning model, and controls the robotic arm. | <img width="300" src="https://github.com/user-attachments/assets/5a5c921e-9021-4990-8892-2aa33eaebafc" /> |
| **PSL-iEOG2 EOG Sensor** | Detects eye potential (EOG) and outputs analog signals representing left/right gaze and blinks. | <img width="300" src="https://github.com/user-attachments/assets/dc2073be-53a0-4884-b0e6-b9ad2de862f3" /> |
| **Servo Motors (SG90 / MG995)** | Drive the robotic arm joints. MG995 is used for high-torque joints, SG90 for lightweight parts. | <img width="300" src="https://github.com/user-attachments/assets/97048b8f-518e-4930-895a-cad75dea3428" /> |
| **3D-Printed Robotic Arm** | Physical arm structure, 3D printed for customizable and functional use. | <img width="300" src="https://github.com/user-attachments/assets/2814adce-4669-40f8-b355-288e6d7c45f6" /> |

> **Component Cost Breakdown:**  
> - PSL-iEOG2 : ₩168,960  
> - Arduino Nano 33 BLE : ₩59,900  
> - MG995 Motors ×4 : ₩26,000  
> - SG90 Motors ×2 : ₩2,800  
> - Battery Packs, AA batteries, breadboards, jumpers, etc. (various)

[🔝 Back to Top](#-table-of-contents)

&nbsp;

## 3. 💻 Technologies Used

| Technology | Description |
|-----------|-------------|
| 💻 **Windows, C++** |
| **PSL-iEOG2 EOG Sensor** | Captures eye movement potentials and outputs analog signals for left/right gaze and blinking detection. |
| **Arduino Nano 33 BLE Sense** | Processes EOG data in real time, classifies gaze direction with TensorFlow Lite, and sends commands to the robotic arm. |
| **Servo Motors (SG90 / MG995)** | Drive the arm joints to perform movements according to gaze direction. |
| **3D-Printed Robotic Arm** | Custom-designed to pick up real objects, fabricated using 3D printing. |

[🔝 Back to Top](#-table-of-contents)

&nbsp;

## 4. 🧭 System Workflow

<img width="652" height="473" alt="image" src="https://github.com/user-attachments/assets/340626b4-d98d-4b9c-bfdc-103f4d0fc735" />

### 📡 EOG Data Collection

Electrooculography (EOG) measures the potential difference between the cornea and retina to record eye movements.  
PSL EOG sensors were used to measure eye potential, connected to Arduino Nano, and monitored via Arduino IDE Serial Monitor.

- Electrodes placed near left/right eyes and center of forehead → measure differential voltages  
- Analog channel used (750 V/V gain)  
- Built-in 60 Hz notch filter, 0.05 Hz HPF, 10 Hz LPF  
- Output voltage range: 0–3.3 V

### 🔀 Slope-Based Feature Extraction

Only the **initial slope change** right after eye movement showed distinct differences between left/right.  
Therefore, **5-second post-gaze EOG windows were differentiated** to create a new dataset.

### 🤖 Model Training & Selection

- CNN: Accuracy 80.7%  
- SVM: Accuracy 88.8%  
- **LSTM: Accuracy 92.5% → Selected final model**

Model was converted to **TensorFlow Lite** and deployed on Arduino Nano for real-time inference.

### 🛠️ 3D-Printed Arm Design & Assembly

- Designed a 6-DOF robotic arm capable of precise movements  
- MG995 motors for base/shoulder/elbow joints, SG90 for wrist/gripper

### 🔌 Circuit & Control

- Motor wires extended and connected to Arduino pins  
- Powered with 5 V power supply for stable torque  
- Servo control implemented via Arduino C++ code

### 🔁 State Machine Logic

- Gaze direction classified as left, right, or center  
- Finite State Machine (FSM) controls arm movement according to classification results

[🔝 Back to Top](#-table-of-contents)

&nbsp;

## ✅ Results

<img width="857" height="341" alt="image" src="https://github.com/user-attachments/assets/3a3af50d-4ca5-4de7-8538-c315d31d9a54" />

- Robotic arm successfully performed direction switching and grabbing using **only the user’s eye movements**  
- Demonstrated feasibility of integrating LSTM-based EOG classification with real-time robotic control

[🔝 Back to Top](#-table-of-contents)

&nbsp;

## 5. 💻 How to Run Code

### 🤖 EogDeepLearning-Robot

- Code: [`eog_deeplearning`](./Arduino/Arduino/eog_deeplearning/eog_deeplearning-DESKTOP-O965BML.ino)

[🔝 Back to Top](#-table-of-contents)

&nbsp;

## 6. 📷 Demonstration Videos / Images

### Kyung Hee University Graduation Thesis Presentation
<img width="670" height="481" alt="image" src="https://github.com/user-attachments/assets/ee818f96-756f-4eaf-9bdc-710e653cd323" />

### Kyung Hee University Capstone Design Competition – Grand Prize 🏆
![Capstone Design Group Photo](https://github.com/user-attachments/assets/d9fc142f-a1ec-436a-888b-d0d8fbc1dbe4)
![Capstone Design Grand Prize](https://github.com/user-attachments/assets/9c34a8d0-3c7f-4ca7-8bd4-0bce211a80c4)

### Demo Video
> https://youtu.be/b7gsw20pOGk?si=eo5Fte_9hxvChOGH  

### System Test Video
> https://youtu.be/0Lg0ZxRh0jA

[🔝 Back to Top](#-table-of-contents)

&nbsp;

## 7. 🌟 Expected Impact / Limitations & Improvements

EOG sensors provide **fast response**, enabling immediate reflection of user intent and **real-time robotic control**.  
The skin-attached, non-invasive method allows safe and convenient use, even for mobility-impaired individuals.  

> This technology can be extended to **medical, industrial, and service applications** for a wide range of users.

### 🛠️ Potential Applications

- **Assistive Devices:** Daily activity support for individuals with limited mobility  
- **Rehabilitation Therapy:** Encourage active participation and track progress  
- **Industrial Automation:** Precision control in manufacturing environments  
- **Service Robots:** Contactless serving systems in cafes, restaurants, etc.

### 🔍 Conclusion & Suggestions

This project demonstrates that **EOG-based robotic control** enables precise and rapid actions via bio-signals.  
The system guarantees **safety and accessibility** while being adaptable to various tasks and environments.  

> With further research and user-centered design, this technology has the potential to **enrich human life**  
> and drive **innovation** in assistive robotics.

[🔝 Back to Top](#-table-of-contents)

&nbsp;

## 🙌 Team Members

- Hayun Yoon  
- Seoyoon Jung  
- Byungho An
