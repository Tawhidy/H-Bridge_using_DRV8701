# H-Bridge Motor Driver PCB - URC 2026

A high-performance 2-layer H-Bridge motor driver PCB designed for University Rover Challenge 2026, featuring the Texas Instruments DRV8701 smart gate driver and CSD18532Q5B NexFET power MOSFETs.

![PCB 3D](https://github.com/Tawhidy/H-Bridge_using_DRV8701/blob/main/images/ISO_3D.png)
![PCB Back](https://github.com/Tawhidy/H-Bridge_using_DRV8701/blob/main/images/Back_3D.png)
*PCB - Component Side*

---

## 📋 Table of Contents

- [Overview](#🎯overview)
- [Features](#features)
- [Specifications](#specifications)
- [Hardware Components](#hardware-components)
- [Circuit Description](#circuit-description)
- [PCB Design](#pcb-design)
- [Simulation](#simulation)
- [Assembly Instructions](#assembly-instructions)
- [Usage](#usage)
- [Testing and Validation](#testing-and-validation)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## 🎯 Overview

This H-Bridge motor driver is designed specifically for the **URC 2026** (University Rover Challenge) robotic system. The design leverages Texas Instruments' advanced motor control components to deliver reliable, high-current motor control with integrated protection features.

### Key Highlights

- **Smart Gate Driver**: DRV8701ERGET with integrated deadtime control and protection
- **High-Performance MOSFETs**: CSD18532Q5B NexFET (60V, ultra-low RDS(on))
- **Current Sensing**: Configurable current limiting up to 20A
- **Compact Design**: 2-layer PCB optimized for manufacturability
- **Simulation Verified**: Validated using TINA-TI simulation software

### Application

- **(6-24)V Brushed DC Motor**
---

## ✨ Features

### Motor Control
- ✅ Bidirectional DC motor control
- ✅ PWM speed & direction control input

### Protection Features
- ✅ Overcurrent protection (OCP)
- ✅ Thermal shutdown
- ✅ Undervoltage lockout (UVLO)
- ✅ Short circuit protection
- ✅ Sleep mode for low power consumption

### Design Features
- ✅ 2-layer (1 0z) PCB for cost-effective manufacturing
- ✅ 30A Continuous & 100A Peak
- ✅ Screw terminal connectors for easy connection
- ✅ Compact form factor: 65 X 45 mm
- ✅ Heatsink added for Optimized thermal management
- ✅ Easy-to-use control interface

---

## 📊 Specifications

### Electrical Specifications

| Parameter                     | Min | Typ | Max | Unit |
| ----------------------------- | --- | --- | --- | ---- |
| **Input Voltage (VM)**        | 6.5 | 18  | 24  | V    |
| **Logic Supply (DVDD)**       | 2.7 | 3.3 | 5.5 | V    |
| **Continuous Output Current** | -   | 30  | 100 | A    |
| **PWM Frequency**             | -   | 25  | 100 | kHz  |
| **Operating Temperature**     | -40 | 25  | 150 | °C   |

### Motor Specifications
(My use case)

| Parameter         | Value      |
| ----------------- | ---------- |
| **Motor Type**    | Brushed DC |
| **Rated Voltage** | 12V, 18V   |
| **Rated Current** | 5A         |
| **Stall Current** | 8A         |

### Mechanical Specifications

| Parameter               | Value             |
| ----------------------- | ----------------- |
| **PCB Dimensions**      | 65 mm × 45 mm     |
| **PCB Thickness**       | 1.6 mm (standard) |
| **Number of Layers**    | 2                 |
| **Mounting Holes**      | 4 (plated - GND)  |
| **Mounting Dimensions** | 60mm × 40mm       |


---

## 🔧 Hardware Components

### Bill of Materials (BOM)

| Ref                | Qty | Value                       | Part Number     | Description                                    | Package               |
| ------------------ | --- | --------------------------- | --------------- | ---------------------------------------------- | --------------------- |
| U1                 | 1   | DRV8701ERGET                | DRV8701ERGET    | 47V H-bridge smart gate driver                 | VQFN-25               |
| U2, U3, U4, U5     | 4   | CSD18532Q5B                 | CSD18532Q5B     | 60V N-channel  MOSFET                          | SON-5mm×6mm           |
| C7, C10            | 2   | 470µF/35V                   | `[TO BE ADDED]` | Electrolytic Cap                               | Radial (through hole) |
| C1, C2, C3, C8, C9 | 5   | 1µF                         | `[TO BE ADDED]` | MLCC X7R                                       | 1206                  |
| C4, C6, C11        | 3   | 100nF                       | `[TO BE ADDED]` |                                                | 0805                  |
| C5                 | 1   | 10µF                        | `[TO BE ADDED]` | MLCC X7R                                       | 1206                  |
| R2, R3, R4, R8, R9 | 5   | 10kΩ                        | `[TO BE ADDED]` | Chip resistor                                  | 0805                  |
| R5, R6, R7         | 3   | 1kΩ                         |                 | chip resistor                                  | 0805                  |
| R1                 | 1   | 500kΩ                       | `[TO BE ADDED]` | Rdrive resistor                                | 1206                  |
| Q1, Q2             | 2   | Transistor                  | 2N3904          | DC power connector                             | Through-hole          |
| J1, J2             | 2   | 5.08mm Pitch Screw Terminal |                 | 2.54mm - 6 pin connector (male),<br>single row | Through-hole          |
| J3                 | 1   | JST-XH                      | JST-XH          | 4Pin - 2.50P connector                         | Through-hole          |

### Component Notes

**DRV8701ERGET** - Key Features:
- Integrated gate driver with adjustable drive strength
- Configurable dead time control
- Built-in current sensing amplifier
- Sleep mode for power saving
- Fault reporting with diagnostic output

**CSD18532Q5B NexFET** - Key Features:
- 60V drain-source voltage rating
- Ultra-low RDS(on) for efficiency
- Optimized for motor drive applications
- Excellent thermal performance in SON package

---

## 🔌 Circuit Description

### Block Diagram

```
                         ┌─────────────────┐
   PWM1 ────────────────►│                 │
   PWM2 ────────────────►│   DRV8701       │
    GND ────────────────►│   Gate Driver   │
    VCC ────────────────►│                 │
                         └────┬──────┬─────┘
                              │      │
                         GH1,GL1  GH2,GL2
                              │      │
                         ┌────▼──────▼─────┐
        ┌───────────────►│  H-Bridge FETs  │◄──────────────┐
        │                │  (CSD18532Q5B)  │               │
     VM(+) ──────────────┤  Q1  Q2  Q3  Q4 ├──────────── VM(+)
                         └────┬──────┬─────┘
                              │      │
                            OUT1   OUT2
                              │      │
                         ┌────▼──────▼─────┐
                         │                 │
                         │   DC MOTOR      │
                         │                 │
                         └─────────────────┘
```

### Schematics
Find a PDF of the Schematics in Docs Folder

![PCB Back](https://github.com/Tawhidy/H-Bridge_using_DRV8701/blob/main/images/Schematic.png)
### Power Supply Section

The driver accepts input voltage (VM) from **6.5V to 47V** through robust Terminal connectors (J1). Bulk capacitors C7 and C10 (470µF/35V) provide energy storage and filtering for the motor power supply.

A regulated **5V logic supply (DVDD)** powers the control circuitry and DRV8701 logic. Decoupling capacitors (C1-C6, C8, C9) ensure clean power delivery to both the gate driver and logic sections.

### Gate Driver Section

The **DRV8701ERGET** provides intelligent gate drive for all four MOSFETs in the H-bridge configuration:

- **Charge pump (VCP)**: Generated from VM to provide gate drive voltage above VM for high-side FETs
- **Dead-time control**: Prevents shoot-through by ensuring both high-side and low-side FETs are never on simultaneously
- **Drive strength control**: Resistor R1 (33kΩ) sets the gate drive current (IDRIVE)

### H-Bridge Power Stage

Four **CSD18532Q5B NexFET** MOSFETs form the H-bridge:
- **U2, U3**: High-side switches
- **U4, U5**: Low-side switches

This configuration enables bidirectional current flow through the motor with low conduction losses.
### Control Interface

5-pin header (P1) provides:
1. **+5V**: Logic power supply input
2. **IN1**: Motor speed control (0-100% duty cycle)
3. **IN2**: Direction control (HIGH/LOW)
4. **GND**: Ground reference

---

## 🖥️ PCB Design

### Design Details

- **Layer Count**: 2 layers
- **Layer Stack**: 
  - **L1 (Top)**: Signal, components, and power routing
  - **L2 (Bottom)**: Ground plane with power routing
- **Copper Weight**: 1 oz
- **Trace Width**: 
  - Power traces (VM): copper pour
  - Signal traces: 0.3 mm
- **Clearance**: 0.2 mm

### Layout Considerations

1. **Power Distribution**:
   - Wide traces for high-current paths (VM, OUT1, OUT2)
   - Star-ground configuration for minimizing ground loops
   - Bulk capacitors placed close to XT60 input connector

2. **Thermal Management**:
   - MOSFETs positioned for optimal heat dissipation
   - Thermal vias under high-power components

3. **Signal Integrity**:
   - Gate drive traces kept short to minimize inductance
   - Proper gate resistors (R2, R3, R4) for controlled switching
   - Decoupling capacitors placed close to IC power pins

4. **EMI Mitigation**:
   - Solid ground plane on bottom layer
   - Minimized loop areas in switching paths

### Manufacturing Files

The `gerbers/` directory contains all files needed for PCB fabrication:
- Project Output Files Folder

Recommended PCB specifications for ordering:
- **Material**: FR-4
- **Thickness**: 1.6mm
- **copper**: 1oz

---

## 🔬 Simulation

### TINA-TI Simulation

The design has been validated using **Texas Instruments TINA-TI** simulation software. The simulation file `slvmb82.TSC` contains the complete circuit model.

### Running Simulations

1. Download and install **TINA-TI** from [TI's website](https://www.ti.com/tool/TINA-TI)
2. Open the simulation file: `simulation/slvmb82.TSC`
3. Run transient analysis to verify:
   - Gate drive timing
   - Current sense accuracy
   - Fault protection triggers
   
---
## 📖 Usage

### Initial Setup

1. **Visual Inspection**: Verify all components are properly soldered. **Optimized for Hand Soldering**
2. **Continuity Check**: Ensure no shorts between power rails
3. **Power Supply Check**: Verify 5V logic supply is stable

### Heatsink Mounting
Same Process as you would do in Putting a heatsink on a M.2 SSD
1. Buy a m.2 SSD Heatsink, Preferably copper
2. Follow the dimension guideline in the File and Drill 2xM3 holes.
3. Cut the excess part.
   
![Heatsink Dimensions](https://github.com/Tawhidy/H-Bridge_using_DRV8701/blob/main/Heatsink/Drawing.png)
```
Control Header (J3):
├─ Pin 1: VCC  ──────► Connect to 5V logic supply
├─ Pin 2: IN1  ──────► Connect to MCU PWM output
├─ Pin 3: IN2  ──────► Connect to MCU GPIO
└─ Pin 5: GND  ──────► Connect to common ground

Power Input (J1):
├─ Positive (+) ─────► Connect to battery/PSU positive
└─ Negative (-) ─────► Connect to battery/PSU ground

Motor Output (J2):
├─ OUT1 ────────────► Motor terminal 1
└─ OUT2 ────────────► Motor terminal 2
```

### Operating Modes

#### Forward Direction
- IN1 = Variable duty cycle (0-100%)
- IN2 = 0% (LOW)
- Current flows: OUT1 → Motor → OUT2

#### Reverse Direction
- IN1 = 0% (LOW)
- IN2 = Variable duty cycle (0-100%)
- Current flows: OUT2 → Motor → OUT1

#### Brake Mode
- IN1 = 100% (HIGH)
- IN2 = 100% (HIGH)
- Low side slow decay

#### Coast Mode
- IN1 = 0% (LOW)
- IN2 = 0% (LOW)

### Control Example (Arduino)

```
cpp
// Pin definitions
#define IN1 9
#define IN2 8
#define FAULT_PIN 7

void setup() {
  pinMode(PWM_PIN, OUTPUT);
  pinMode(DIR_PIN, OUTPUT);
  pinMode(FAULT_PIN, INPUT_PULLUP);
  
  // Set PWM frequency (adjust for your motor)
}

void setMotorSpeed(int speed) {
  // speed: -255 (full reverse) to +255 (full forward)
  
  if (speed > 0) {
    digitalWrite(DIR_PIN, HIGH);
    analogWrite(PWM_PIN, speed);
  } else if (speed < 0) {
    digitalWrite(DIR_PIN, LOW);
    analogWrite(PWM_PIN, -speed);
  } else {
    analogWrite(PWM_PIN, 0); // Brake
  }
  
  // Check for faults
  if (digitalRead(FAULT_PIN) == LOW) {
    // Handle fault condition
    Serial.println("Motor driver fault detected!");
  }
}

void loop() {
  // Example: Ramp up forward, then reverse
  for (int speed = 0; speed <= 255; speed++) {
    setMotorSpeed(speed);
    delay(10);
  }
  delay(1000);
  
  for (int speed = 255; speed >= -255; speed--) {
    setMotorSpeed(speed);
    delay(10);
  }
  delay(1000);
}
```


## ✅ Testing and Validation

### Functional Tests

#### 1. Power-On Test
- [ ] Apply 5V to DVDD (Pin 1 of P1)
- [ ] Measure VM voltage at test points
- [ ] Verify no overcurrent on power supply
- [ ] Check LED indicators (if present)

#### 2. No-Load Test
- [ ] Connect motor to J2
- [ ] Apply low PWM duty cycle (10-20%)
- [ ] Verify motor rotates in both directions
- [ ] Measure quiescent current: `[TO BE ADDED]` mA

#### 3. Load Test
- [ ] Apply rated load to motor
- [ ] Gradually increase PWM to 100%
- [ ] Monitor motor current
- [ ] Verify current limiting at ~20A
- [ ] Check for thermal issues

#### 4. Fault Protection Test
- [ ] Overcurrent: `[TO BE ADDED: Test method]`
- [ ] Thermal shutdown: `[TO BE ADDED: Test method]`
- [ ] Undervoltage: `[TO BE ADDED: Test method]`

### Performance Measurements

`[TO BE ADDED: Add actual measured values]`

| Parameter                    | Expected | Measured   | Status |
| ---------------------------- | -------- | ---------- | ------ |
| Quiescent Current (no load)  | < 50 mA  | `____` mA  | ☐      |
| Maximum Continuous Current   | 30 A     | `____` A   | ☐      |
| Switching Frequency          | XX kHz   | `____` kHz | ☐      |
| Efficiency @ 50% load        | > 95%    | `____` %   | ☐      |
| Rise Time (10-90%)           | < X µs   | `____` µs  | ☐      |
| Fall Time (90-10%)           | < X µs   | `____` µs  | ☐      |
| Temperature Rise @ Full Load | < 40°C   | `____` °C  | ☐      |

---

## 📁 Project Structure

```
h-bridge-motor-driver/
├── README.md                    # This file
├── docs/                        # Documentation
│   ├── schematic.pdf           # Circuit schematic
│   ├── pcb_top.pdf            # PCB top layer
│   ├── pcb_bottom.pdf         # PCB bottom layer
│   └── assembly_guide.pdf     # [TO BE ADDED]
├── hardware/                    # Hardware design files
│   ├── schematic/
│   │   └── H_Bridge1.SchDoc   # Altium schematic file
│   ├── pcb/
│   │   └── H_Bridge_pcb.PcbDoc # Altium PCB file
│   └── gerbers/               # Manufacturing files
│       └── [TO BE ADDED]
├── simulation/                  # TINA-TI simulation files
│   ├── slvmb82.TSC            # Main simulation file
│   └── results/               # [TO BE ADDED]
├── firmware/                    # Example control code
│   └── [TO BE ADDED]
├── bom/                        # Bill of materials
│   └── H_Bridge_BOM.xlsx      # [TO BE ADDED]
└── LICENSE                     # [TO BE ADDED]
```

---

## 🤝 Contributing

Contribution guidelines if this is a team project

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/improvement`)
5. Open a Pull Request

---

## 📄 License

- MIT License (permissive)
---

## 📧 Contact

**Project Team**: Project Altair
**University**: ISLAMIC UNIVERSITY OF TECHNOLOGY (IUT), Gazipur, Dhaka.
**Maintainer**: Tawhid Alam
- Email: tawhidalam2001@gmail.com

---

## 🙏 Acknowledgments

- Texas Instruments for DRV8701 reference design and TINA-TI simulation software
- University Rover Challenge organizers
---

## 📚 References

1. [DRV8701 Datasheet](https://www.ti.com/product/DRV8701)
2. [CSD18532Q5B Datasheet](https://www.ti.com/product/CSD18532Q5B)
3. [TINA-TI Simulation Software](https://www.ti.com/tool/TINA-TI)
4. [DRV8701 Reference Design](https://www.ti.com/lit/pdf/slvmb82) - SLVMB82

---

## ⚠️ Safety Notes

- **High Current**: This driver can deliver 30A+ - ensure proper fusing and wire gauge
- **Reverse Polarity**: **No Reverse Polarity Protection**. Incorrect polarity on VM can damage components
- **Heat Dissipation**: Heatsink Added.
- **Inductive Load**: Motors generate back-EMF - this driver includes protection
- **ESD Sensitive**: **Use anti-static precautions during assembly

---

**Last Updated**: 17 Mar 2026

**Board Revision**: Rev 1.0

**Status**: Prototype Design

---

*Made with Altium Designer-23 for URC 2026*
