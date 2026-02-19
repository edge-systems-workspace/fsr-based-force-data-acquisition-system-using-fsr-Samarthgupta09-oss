# 🧲 FSR-Based Force Data Acquisition System

![License](https://img.shields.io/badge/license-MIT-blue)
![Platform](https://img.shields.io/badge/platform-Arduino-orange)
![Language](https://img.shields.io/badge/language-C++-blue)
![Microcontroller](https://img.shields.io/badge/Microcontroller-Arduino%20Uno%20R4-brightgreen)

An embedded force sensing and data acquisition system using a Force Sensitive Resistor (FSR) for real-time pressure measurement and structured serial monitoring.

---

## 📑 Table of Contents

- [Author Information](#author-information)
- [Project Framework & Environment](#project-framework--environment)
- [Hardware Requirements](#hardware-requirements)
- [Software Requirements](#software-requirements)
- [Libraries in Code](#libraries-in-code)
- [Code Functions Documentation](#code-functions-documentation)
- [Sensor & Pin Configuration](#sensor--pin-configuration)
- [Wiring Connections](#wiring-connections)
- [Sensor Working Principle](#sensor-working-principle)
- [Project Overview](#project-overview)
- [Future Improvements](#future-improvements)
- [License](#license)

---

## 👨‍💻 Author Information

| Attribute | Details |
|-----------|---------|
| **@author** | Samarth Gupta |
| **@date** | February 19, 2026 |
| **@time** | Project Completion Phase |
| **@file** | src/main.cpp |
| **@framework** | Arduino Framework (PlatformIO) |
| **@purpose** | FSR-based force data acquisition and real-time sensor monitoring |
| **@brief** | Real-time analog force measurement system using Force Sensitive Resistor with serial data transmission |

---

## 🏗️ Project Framework & Environment

### **Framework**
- **Name:** Arduino Framework
- **Platform:** PlatformIO (Platform.io)
- **Description:** Open-source development environment for embedded systems with Arduino compatibility

### **Microcontroller**
- **Model:** Arduino Uno R4 WiFi (Renesas RA4M1)
- **Processor:** Renesas RA MCU
- **Memory:** 32 KB RAM, 256 KB Flash
- **Analog Inputs:** 14 (A0-A13)
- **Operating Voltage:** 5V

### **IDE (Integrated Development Environment)**
- **IDE Name:** Arduino IDE / PlatformIO IDE
- **Version:** Latest (Compatible with PlatformIO v6.x)
- **Build System:** PlatformIO Build System
- **Upload Protocol:** Serial (9600 baud)

### **Configuration File**
The project uses `platformio.ini` for configuration:
```ini
[env:uno_r4_wifi]
platform = renesas-ra
board = uno_r4_wifi
framework = arduino
```

---

## 🔧 Hardware Requirements

| Component | Quantity | Description |
|-----------|----------|-------------|
| Arduino Uno R4 WiFi | 1 | Main microcontroller board |
| Force Sensitive Resistor (FSR 402) | 1 | Pressure/force sensor |
| 10kΩ Resistor | 1 | Voltage divider resistor |
| Breadboard | 1 | Prototyping board |
| Jumper Wires | 4-5 | Connecting components |
| USB Type-C Cable | 1 | For programming and power |

---

## 💻 Software Requirements

| Software | Version | Purpose |
|----------|---------|---------|
| Arduino IDE | Latest | Code development and compilation |
| PlatformIO | v6.x+ | Build and upload framework |
| Git | Latest | Version control |
| GitHub Account | - | Repository hosting |

---

## 📚 Libraries in Code

### **Arduino Core Libraries Used:**

| Library | Header | Purpose |
|---------|--------|---------|
| Arduino Core | `<Arduino.h>` | Core Arduino functions including Serial communication, GPIO control, and analog-to-digital conversion (ADC) |

### **Built-in Functions Used (Arduino.h):**
- `Serial.begin(9600)` - Initialize serial communication at 9600 baud rate
- `pinMode(A0, INPUT)` - Configure pin mode for analog input
- `analogRead(A0)` - Read analog value from pin A0 (0-1023)
- `Serial.println()` - Print data with newline to serial monitor
- `delay()` - Delay execution for specified milliseconds

---

## 🧠 Code Functions Documentation

### **1. void setup()**

```cpp
void setup() {
    Serial.begin(9600);
    pinMode(A0, INPUT);
}
```

**Purpose:** Initialize the system once at startup.

**Function Details:**
- **Serial.begin(9600):** Initializes serial communication with a baud rate of 9600 bits per second. This allows the Arduino to send data to the Serial Monitor on the connected computer.
  - Baud rate: 9600 (standard for Arduino projects)
  - Enables bidirectional communication
  - Required before any Serial.print() or Serial.println() calls

- **pinMode(A0, INPUT):** Configures analog pin A0 as an input pin.
  - Pin mode: INPUT (sets the pin to read analog voltage)
  - Pin reference: A0 (Analog Pin 0)
  - Allows the Arduino ADC to sample the voltage from the FSR sensor

**Execution:** Runs once when the microcontroller boots up or after reset.

---

### **2. void loop()**

```cpp
void loop() {
    value = analogRead(A0);
    Serial.println(value);
    delay(500);
}
```

**Purpose:** Continuously acquire force data and transmit it to the host.

**Function Details:**

1. **value = analogRead(A0):**
   - Reads the analog voltage from pin A0
   - Converts analog voltage (0-5V) to digital value (0-1023) using 10-bit ADC
   - Stores the result in the global variable `value`
   - ADC Resolution: 10-bit (0-1023)
   - Conversion time: ~100 microseconds

2. **Serial.println(value):**
   - Transmits the sensor reading to the Serial Monitor
   - Appends a newline character after each value
   - Allows real-time monitoring of force data
   - Output format: Raw ADC value (0-1023)

3. **delay(500):**
   - Pauses execution for 500 milliseconds (0.5 seconds)
   - Sampling rate: 2 Hz (2 readings per second)
   - Prevents overwhelming the serial port
   - Allows time for human observation of sensor changes

**Execution:** Repeats continuously after setup() completes.

**Data Flow:** Sensor → ADC → Serial Transmission → Serial Monitor

---

## 📍 Sensor & Pin Configuration

### **FSR Sensor Details**
- **Type:** Force Sensitive Resistor (FSR 402)
- **Sensor Principle:** Resistive pressure sensor
- **Force Range:** 0 - 10 kg (approximately)
- **Resistance Range:** 100MΩ (no force) → 1kΩ (maximum force)
- **Operating Temperature:** -20°C to +60°C

### **Pin Assignment**

| Pin | Type | Function | Connection |
|-----|------|----------|-----------|
| A0 | Analog Input | Force sensor data acquisition | FSR sensor output (via voltage divider) |
| 5V | Power | Supply voltage | FSR sensor positive pin |
| GND | Ground | Reference voltage | Voltage divider and circuit ground |

### **Analog Input Characteristics**
- **Pin:** A0 (Arduino Uno R4)
- **Voltage Range:** 0-5V
- **ADC Resolution:** 10-bit (0-1023 counts)
- **Conversion Resolution:** ~4.9 mV per bit (5V / 1024)

---

## 🔌 Wiring Connections (Voltage Divider Setup)

### **Circuit Configuration:**

```
5V ─────┬─────────┐
        │         │
       FSR      10kΩ Resistor
        │         │
        └────┬────┘
             │
            A0 (Analog Input)
             │
            GND
```

### **Pin Connection Table**

| Arduino Pin | Component | Description |
|-------------|-----------|-------------|
| 5V | FSR Pin 1 | Supply voltage for sensor |
| A0 | FSR Pin 2 & 10kΩ junction | Analog voltage measurement point |
| GND | 10kΩ Resistor Pin 2 | Ground reference |

### **Voltage Divider Formula**
```
V_out = V_in × (R2 / (R1 + R2))
Where:
  - V_in = 5V (supply voltage)
  - R1 = FSR resistance (variable)
  - R2 = 10kΩ (fixed)
  - V_out = Voltage measured at A0
```

⚠️ **Important:** FSR must be connected using a voltage divider configuration to convert resistance changes into voltage changes that the ADC can measure.

---

## ⚙️ Sensor Working Principle

### **How FSR Works:**

1. **Resistance Change with Force:**
   - FSR resistance **decreases** when force/pressure increases
   - No force: ~100 MΩ (very high resistance)
   - Maximum force: ~1 kΩ (low resistance)

2. **Voltage Divider Effect:**
   - As FSR resistance changes, the voltage at point A0 changes
   - Higher force → Lower FSR resistance → Higher voltage at A0
   - Lower force → Higher FSR resistance → Lower voltage at A0

3. **ADC Conversion:**
   - Arduino ADC samples the voltage at A0 (0-5V)
   - Converts analog voltage to digital value: **0-1023**
   - 10-bit resolution: ~4.9 mV per step

4. **Data Output:**
   - Raw ADC value is printed to Serial Monitor every 500ms
   - Value ranges from 0 (no force) to 1023 (maximum force)
   - Real-time force measurement displayed continuously

### **Signal Flow:**
```
Mechanical Force
       ↓
FSR Resistance Change
       ↓
Voltage Divider (0-5V)
       ↓
Arduino ADC Conversion (0-1023)
       ↓
Serial Transmission
       ↓
Serial Monitor Display
```

---

## 🚀 Project Overview

This project demonstrates **force measurement** and **data acquisition** using an FSR sensor connected to an Arduino Uno R4.

### **System Capabilities:**
- ✅ Real-time analog force sensing
- ✅ ADC conversion (0-1023 digital values)
- ✅ Serial data transmission at 9600 baud
- ✅ Sampling rate: 2 Hz (readings every 500ms)
- ✅ Continuous monitoring via Serial Monitor

### **Learning Objectives:**
- Understand analog sensor interfacing
- Learn ADC (Analog-to-Digital Conversion) principles
- Implement data acquisition systems
- Develop embedded system firmware
- Practice serial communication protocols

### **Applications:**
- Force measurement systems
- Pressure sensing
- Touch detection
- Robotic gripper control
- Load cell simulation

---

## 🔮 Future Improvements

- [ ] Convert ADC value to estimated force in Newtons (N)
- [ ] Implement data logging to SD card
- [ ] Add LCD display for local readings
- [ ] Real-time data plotting with Python/MATLAB
- [ ] Integrate with robotic gripper system
- [ ] Add calibration routine for accurate force estimation
- [ ] Implement threshold-based alerts
- [ ] Add wireless data transmission (WiFi/Bluetooth)
- [ ] Create mobile app for remote monitoring
- [ ] Implement machine learning for force prediction

---

## 📜 License

This project is licensed under the **MIT License**.

You are free to use, modify, and distribute this project for personal and commercial purposes.
