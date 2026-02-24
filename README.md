# H-Bridge Motor Driver PCB - URC 2026

A high-performance 2-layer H-Bridge motor driver PCB designed for University Rover Challenge 2026, featuring the Texas Instruments DRV8701 smart gate driver and CSD18532Q5B NexFET power MOSFETs.

![PCB Top Layer](docs/pcb_top.png)
*PCB Layout - Component Side*

---

## 📋 Table of Contents

- [Overview](#overview)
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

`[TO BE ADDED: Describe the specific motor/actuator this driver controls in your URC rover - e.g., wheel motors, robotic arm joints, etc.]`

---

## ✨ Features

### Motor Control
- ✅ Bidirectional DC motor control
- ✅ PWM speed control input
- ✅ Direction control input
- ✅ Configurable current limiting (up to 20A)
- ✅ Fault detection and reporting

### Protection Features
- ✅ Overcurrent protection (OCP)
- ✅ Thermal shutdown
- ✅ Undervoltage lockout (UVLO)
- ✅ Short circuit protection
- ✅ Sleep mode for low power consumption

### Design Features
- ✅ 2-layer PCB for cost-effective manufacturing
- ✅ XT60 connectors for robust power connections
- ✅ Compact form factor: `[TO BE ADDED: Board dimensions]`
- ✅ Optimized thermal management
- ✅ Easy-to-use control interface

---

## 📊 Specifications

### Electrical Specifications

| Parameter | Min | Typ | Max | Unit |
|-----------|-----|-----|-----|------|
| **Input Voltage (VM)** | 6.5 | 24 | 47 | V |
| **Logic Supply (DVDD)** | - | 5 | 5.5 | V |
| **Continuous Output Current** | - | 15 | 20 | A |
| **Peak Output Current** | - | - | `[TO BE ADDED]` | A |
| **PWM Frequency** | - | - | `[TO BE ADDED]` | kHz |
| **Current Sense Range** | - | 20 | - | A |
| **Operating Temperature** | -40 | 25 | 125 | °C |

### Motor Specifications

| Parameter | Value |
|-----------|-------|
| **Motor Type** | Brushed DC |
| **Rated Voltage** | `[TO BE ADDED]` V |
| **Rated Current** | `[TO BE ADDED]` A |
| **Stall Current** | `[TO BE ADDED]` A |

### Mechanical Specifications

| Parameter | Value |
|-----------|-------|
| **PCB Dimensions** | `[TO BE ADDED]` mm × `[TO BE ADDED]` mm |
| **PCB Thickness** | 1.6 mm (standard) |
| **Number of Layers** | 2 |
| **Mounting Holes** | `[TO BE ADDED]` |
| **Weight** | `[TO BE ADDED]` g |

---

## 🔧 Hardware Components

### Bill of Materials (BOM)

| Ref | Qty | Value | Part Number | Description | Package |
|-----|-----|-------|-------------|-------------|---------|
| U1 | 1 | DRV8701ERGET | DRV8701ERGET | 47V H-bridge smart gate driver | VQFN-25 |
| U2, U3, U4, U5 | 4 | CSD18532Q5B | CSD18532Q5B | 60V N-channel NexFET MOSFET | SON-5mm×6mm |
| C7, C10 | 2 | 470µF/35V | `[TO BE ADDED]` | Bulk capacitor | Radial |
| C4, C6 | 2 | 1µF | CC0805MKX7R6BB105 | Ceramic capacitor 10V X7R | 0805 |
| C1, C2, C3, C5, C8, C9 | 6 | 10µF | ECHU1C473JX5 | Ceramic capacitor 16VDC 12% | 1206 |
| R2, R3, R4 | 3 | 10kΩ | - | Chip resistor ±1% 0.25W | 0805 |
| R1 | 1 | 33kΩ | - | Chip resistor ±1% 0.25W | 0805 |
| P1 | 1 | - | MTSW-106-09-T-S-540 | 0.025" SQ post header, 5-pin | Through-hole |
| J1, J2 | 2 | XT60-M | XT60-M | DC power connector | - |

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
    PWM ────────────────►│                 │
    DIR ────────────────►│   DRV8701      │
  FAULT ◄────────────────│   Gate Driver  │
  SLEEP ────────────────►│                 │
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

### Power Supply Section

The driver accepts input voltage (VM) from **6.5V to 47V** through robust XT60 connectors (J1). Bulk capacitors C7 and C10 (470µF/35V) provide energy storage and filtering for the motor power supply.

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

### Current Sensing

The DRV8701 includes integrated current sensing:

**Current Limit Calculation**:
```
VREF = (Ichop × Rsense × 20) + 0.05
```

For **Ichop = 20A**:
- VREF is set via resistor divider R2, R3, R4
- VREF = 4.8V (calculated for 20A current limit)
- The 20× gain of internal current sense amplifier scales the sense voltage

### Control Interface

5-pin header (P1) provides:
1. **+5V**: Logic power supply input
2. **PWM**: Motor speed control (0-100% duty cycle)
3. **DIR**: Direction control (HIGH/LOW)
4. **FAULT**: Active-low fault output
5. **GND**: Ground reference

---

## 🖥️ PCB Design

### Design Details

- **Layer Count**: 2 layers
- **Layer Stack**: 
  - **L1 (Top)**: Signal, components, and power routing
  - **L2 (Bottom)**: Ground plane with power routing
- **Copper Weight**: `[TO BE ADDED: e.g., 1 oz or 2 oz]`
- **Trace Width**: 
  - Power traces (VM): `[TO BE ADDED]` mm
  - Signal traces: `[TO BE ADDED]` mm
- **Clearance**: `[TO BE ADDED]` mm

### Layout Considerations

1. **Power Distribution**:
   - Wide traces for high-current paths (VM, OUT1, OUT2)
   - Star-ground configuration for minimizing ground loops
   - Bulk capacitors placed close to XT60 input connector

2. **Thermal Management**:
   - MOSFETs positioned for optimal heat dissipation
   - Thermal vias under high-power components
   - `[TO BE ADDED: Heatsink mounting provisions, if any]`

3. **Signal Integrity**:
   - Gate drive traces kept short to minimize inductance
   - Proper gate resistors (R2, R3, R4) for controlled switching
   - Decoupling capacitors placed close to IC power pins

4. **EMI Mitigation**:
   - Solid ground plane on bottom layer
   - Minimized loop areas in switching paths
   - `[TO BE ADDED: Additional EMI measures]`

### Manufacturing Files

The `gerbers/` directory contains all files needed for PCB fabrication:
- `[TO BE ADDED: List of Gerber files]`

Recommended PCB specifications for ordering:
- **Material**: FR-4
- **Thickness**: 1.6mm
- **Surface Finish**: `[TO BE ADDED: e.g., HASL, ENIG]`
- **Solder Mask**: `[TO BE ADDED: color]`
- **Silkscreen**: `[TO BE ADDED: color]`

---

## 🔬 Simulation

### TINA-TI Simulation

The design has been validated using **Texas Instruments TINA-TI** simulation software. The simulation file `slvmb82.TSC` contains the complete circuit model.

### Simulation Results

`[TO BE ADDED: Add key simulation results such as:]`
- Switching waveforms
- Current limiting behavior
- Thermal performance
- Efficiency curves
- PWM response

### Running Simulations

1. Download and install **TINA-TI** from [TI's website](https://www.ti.com/tool/TINA-TI)
2. Open the simulation file: `simulation/slvmb82.TSC`
3. Run transient analysis to verify:
   - Gate drive timing
   - Current sense accuracy
   - Fault protection triggers
   - `[TO BE ADDED: Other parameters]`

**Simulation Parameters**:
```
[TO BE ADDED: Key simulation parameters like:
- Input voltage: XX V
- Load resistance: XX Ω
- PWM frequency: XX kHz
- Duty cycle range: XX%
]
```

---

## 🔨 Assembly Instructions

### Prerequisites

- Soldering iron (temperature-controlled recommended)
- Solder paste (for SMD components)
- Hot air rework station or reflow oven
- Tweezers and fine-tip tools
- Multimeter
- `[TO BE ADDED: Other tools]`

### Assembly Sequence

1. **SMD Components First**:
   - Start with smallest components (resistors, small capacitors)
   - Apply solder paste to pads
   - Place components using tweezers
   - Reflow using hot air or oven

2. **Gate Driver IC (U1)**:
   - Carefully align DRV8701ERGET on pads
   - Use hot air or reflow to solder
   - Inspect with magnification for solder bridges

3. **MOSFETs (U2-U5)**:
   - Align CSD18532Q5B MOSFETs ensuring correct orientation
   - Reflow solder
   - Check thermal pad connection

4. **Through-Hole Components**:
   - Solder bulk capacitors C7, C10
   - Install XT60 connectors (J1, J2)
   - Install control header (P1)

5. **Inspection**:
   - Visual inspection for solder bridges
   - Continuity testing for power rails
   - Verify no shorts between VM and GND

### Assembly Tips

- Use thermal relief for ground connections on large pads
- Ensure proper polarity for electrolytic capacitors C7, C10
- MOSFETs are directional - verify pinout before soldering
- Add thermal paste if using heatsinks

---

## 📖 Usage

### Initial Setup

1. **Visual Inspection**: Verify all components are properly soldered
2. **Continuity Check**: Ensure no shorts between power rails
3. **Power Supply Check**: Verify 5V logic supply is stable

### Connections

```
Control Header (P1):
├─ Pin 1: +5V  ──────► Connect to 5V logic supply
├─ Pin 2: PWM  ──────► Connect to MCU PWM output
├─ Pin 3: DIR  ──────► Connect to MCU GPIO
├─ Pin 4: FAULT ─────► Connect to MCU GPIO input (with pull-up)
└─ Pin 5: GND  ──────► Connect to common ground

Power Input (J1 - XT60):
├─ Positive (+) ─────► Connect to battery/PSU positive
└─ Negative (-) ─────► Connect to battery/PSU ground

Motor Output (J2 - XT60):
├─ OUT1 ────────────► Motor terminal 1
└─ OUT2 ────────────► Motor terminal 2
```

### Operating Modes

#### Forward Direction
- DIR = HIGH
- PWM = Variable duty cycle (0-100%)
- Current flows: OUT1 → Motor → OUT2

#### Reverse Direction
- DIR = LOW
- PWM = Variable duty cycle (0-100%)
- Current flows: OUT2 → Motor → OUT1

#### Brake Mode
- PWM = 0% (LOW)
- Both outputs shorted to ground through low-side FETs

#### Sleep Mode
`[TO BE ADDED: Sleep mode control if implemented]`

### Control Example (Arduino)

```cpp
// Pin definitions
#define PWM_PIN 9
#define DIR_PIN 8
#define FAULT_PIN 7

void setup() {
  pinMode(PWM_PIN, OUTPUT);
  pinMode(DIR_PIN, OUTPUT);
  pinMode(FAULT_PIN, INPUT_PULLUP);
  
  // Set PWM frequency (adjust for your motor)
  // [TO BE ADDED: Specific PWM frequency setting]
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

### Fault Handling

The FAULT pin goes LOW when:
- Overcurrent condition detected
- Thermal shutdown triggered
- Undervoltage on VM or DVDD
- `[TO BE ADDED: Other fault conditions]`

**Recommended fault recovery**:
1. Read FAULT pin state
2. If LOW, disable PWM output
3. Wait for fault to clear
4. Check fault cause (temperature, current, voltage)
5. Resume operation only after fault is resolved

---

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

| Parameter | Expected | Measured | Status |
|-----------|----------|----------|--------|
| Quiescent Current (no load) | < 50 mA | `____` mA | ☐ |
| Maximum Continuous Current | 20 A | `____` A | ☐ |
| Switching Frequency | XX kHz | `____` kHz | ☐ |
| Efficiency @ 50% load | > 95% | `____` % | ☐ |
| Rise Time (10-90%) | < X µs | `____` µs | ☐ |
| Fall Time (90-10%) | < X µs | `____` µs | ☐ |
| Temperature Rise @ Full Load | < 40°C | `____` °C | ☐ |

### Test Equipment Required

- Programmable power supply (6.5-47V, >25A capability)
- Electronic load or test motor
- Oscilloscope (for waveform analysis)
- Multimeter
- Infrared thermometer or thermal camera
- `[TO BE ADDED: Other equipment]`

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

`[TO BE ADDED: Contribution guidelines if this is a team project]`

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/improvement`)
5. Open a Pull Request

---

## 📄 License

`[TO BE ADDED: Choose and add appropriate license]`

This project is licensed under the `______` License - see the [LICENSE](LICENSE) file for details.

Recommended licenses for hardware projects:
- MIT License (permissive)
- CERN Open Hardware Licence v2 (hardware-specific)
- Creative Commons (for documentation)

---

## 📧 Contact

**Project Team**: `[TO BE ADDED]`

**University**: `[TO BE ADDED]`

**URC 2026 Team**: `[TO BE ADDED]`

**Maintainer**: `[TO BE ADDED: Your name]`
- Email: `[TO BE ADDED]`
- GitHub: `[TO BE ADDED]`

---

## 🙏 Acknowledgments

- Texas Instruments for DRV8701 reference design and TINA-TI simulation software
- University Rover Challenge organizers
- `[TO BE ADDED: Team members, advisors, sponsors]`

---

## 📚 References

1. [DRV8701 Datasheet](https://www.ti.com/product/DRV8701)
2. [CSD18532Q5B Datasheet](https://www.ti.com/product/CSD18532Q5B)
3. [TINA-TI Simulation Software](https://www.ti.com/tool/TINA-TI)
4. [DRV8701 Reference Design](https://www.ti.com/lit/pdf/slvmb82) - SLVMB82
5. `[TO BE ADDED: Additional references]`

---

## ⚠️ Safety Notes

- **High Current**: This driver can deliver 20A+ - ensure proper fusing and wire gauge
- **Reverse Polarity**: Incorrect polarity on VM can damage components
- **Heat Dissipation**: MOSFETs may require heatsinks at high current
- **Inductive Load**: Motors generate back-EMF - this driver includes protection
- **ESD Sensitive**: Use anti-static precautions during assembly

---

**Last Updated**: `[TO BE ADDED: Date]`

**Board Revision**: Rev 1.0

**Status**: `[TO BE ADDED: e.g., Prototype, Tested, Production]`

---

*Made with ⚡ for URC 2026*
