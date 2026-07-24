# Potentiometer-Based Position Controller

A bare-metal C implementation for an STM32F103 microcontroller that performs position control using analog feedback. The system samples input voltage from a potentiometer via an ADC and translates it into a PWM duty cycle for motor or servo actuation.

---

## Overview

In position control applications, continuous mapping between sensor feedback and dynamic signal output is crucial. This project implements a deterministic linear translation pipeline on the STM32 architecture using Peripheral Hardware Timers and Analog-to-Digital Converters.

* **Sensor Interface:** Samples 12-bit analog feedback via ADC1 Channel 0 (`PA0`).
* **Actuation Output:** Drives PWM signal generation on TIM2 Channel 2 (`PA1`).
* **Deterministic Logic:** Maps raw 12-bit readings directly to dynamic timer compare registers.

---

## Mathematical Translation Logic

The system reads raw input levels ranging from $0$ to $4095$ ($2^{12} - 1$) and maps them to a PWM duty compare range between $1000$ and $2000$ microseconds:

$$\text{PWM Duty} = 1000 + \left( \frac{\text{ADC Value} \times 1000}{4095} \right)$$

---

## Hardware Architecture & Peripheral Mapping

| Peripheral | Pin | Configuration Mode | Description |
| :--- | :--- | :--- | :--- |
| **ADC1_IN0** | `PA0` | Analog Mode | Potentiometer Feedback Input (12-bit Resolution) |
| **TIM2_CH2** | `PA1` | PWM Generation Mode | PWM Control Output |

### Pinout Assignment
<img width="1918" height="1026" alt="Pinout" src="https://github.com/user-attachments/assets/95684fc9-ef52-4a37-9f31-11706ea7969b" />

### System Clock Tree
<img width="1920" height="1026" alt="Clock_Config" src="https://github.com/user-attachments/assets/79154ac5-728a-4200-b6c2-8bdf22473c55" />

---

## Build and Project Layout

### Directory Structure
```text
.
├── Core/
│   ├── Inc/           # Application Header Files
│   └── Src/           # C Source Files (main.c, peripheral setup)
├── FinalProject.ioc   # STM32CubeMX Project Configuration
└── FinalProject.hex   # Compiled Binary Executable
```
---

## Build Instructions

1. **Clone the repository:**
```bash
git clone [https://github.com/mohizmni/Position-Control-Using-Potentiometer.git]
```
2. **Import the Project workspace into STM32CubeIDE.**
  
3. **Build the target(Ctrl + B)to compile source binaries.**
