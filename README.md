[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/VO8hr3MM)
# 🧲 Embedded Force Measurement System – FSR

![License](https://img.shields.io/badge/license-MIT-blue)
![Platform](https://img.shields.io/badge/platform-Arduino-orange)
![Language](https://img.shields.io/badge/language-C++-blue)


An embedded force sensing and data acquisition system using a Force Sensitive Resistor (FSR) for real-time pressure measurement and structured serial monitoring.

---

## 📑 Table of Contents

- Project Overview
- Hardware Requirements
- Software Requirements
- Wiring Connections
- Sensor Working Principle
- Code Structure
- Documentation Requirement
- Submission Requirements
- Future Improvements
- License

---

## 🚀 Project Overview

This project demonstrates force measurement using an FSR sensor and Arduino (Uno R4 recommended).

The system:

- Reads analog force data
- Converts raw ADC values
- Displays structured output
- Implements input validation
- Follows Doxygen documentation standards
- Enforces Git-based development discipline

This project introduces:

- Analog sensor interfacing
- ADC (Analog-to-Digital Conversion)
- Data acquisition systems
- Embedded system structuring

---

## 🔧 Hardware Requirements

- Arduino Uno R4
- Force Sensitive Resistor (FSR)
- 10kΩ Resistor (Voltage Divider)
- Breadboard
- Jumper wires
- USB cable

---

## 💻 Software Requirements

- Arduino IDE
- Git
- GitHub Account

---

## 🔌 Wiring Connections (Voltage Divider Setup)

| Component | Connection |
|------------|------------|
| FSR One Pin | 5V |
| FSR Other Pin | Analog Pin A0 |
| 10kΩ Resistor | Between A0 and GND |

⚠ FSR must be connected using a voltage divider configuration.

---

## ⚙ Sensor Working Principle

- FSR resistance decreases when force increases.
- Analog voltage changes.
- Arduino ADC converts voltage to digital value (0–1023).
- Force estimation is derived from ADC value.

---

## 🧠 Code Structure

The system:

1. Initializes Serial communication
2. Reads analog value from A0
3. Converts raw ADC reading
4. Prints formatted force data
5. Applies threshold detection

---

## 📚 Documentation Requirement

Students must include:

- File-level Doxygen block
- Documentation for:
  - `setup()`
  - `loop()`
- Required tags:
  - `@file`
  - `@brief`
  - `@author`
  - `@date`

---

## 📊 Submission Requirements

- Minimum 5 meaningful commits
- Proper commit message format
- TODO tasks completed
- Doxygen documentation included
- Code must compile successfully

---

## 🔮 Future Improvements

- Convert ADC value to estimated force (Newton)
- Add LCD display
- Add data logging
- Add real-time plotting
- Integrate with robotic gripper system

---

## 📜 License

This project is licensed under the MIT License.
