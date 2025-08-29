# Iron Arm - DIY Arm Exoskeleton

![Project Status](https://img.shields.io/badge/Status-In%20Development-yellow)
![Build Difficulty](https://img.shields.io/badge/Difficulty-Intermediate-orange)
![Estimated Cost](https://img.shields.io/badge/Cost-$284-green)
![Build Time](https://img.shields.io/badge/Build%20Time-40--60%20hours-blue)

A single degree-of-freedom arm exoskeleton that provides force amplification for elbow flexion/extension. Built for fun, learning, and demonstration of human augmentation concepts.

## 🎯 Project Overview

**Iron Arm** is an open-source arm exoskeleton designed to:
- Amplify user force input by 1.5x to 3x
- Provide smooth, responsive assistance with <100ms latency
- Demonstrate practical human-machine interface concepts
- Serve as a platform for robotics and control systems learning

### Key Features
- ⚡ **Real-time force amplification** - Detects your effort and multiplies it
- 🔋 **2+ hour battery life** - Portable and practical for demonstrations
- 📱 **Bluetooth connectivity** - Control and monitoring via smartphone
- 🛡️ **Safety systems** - Emergency stops and force limiting
- 🔧 **Modular design** - Easy to modify and upgrade
- 📊 **Data logging** - Track performance and usage patterns

## 🚀 Quick Start

### Prerequisites
- 3D printer (200x200x200mm minimum build volume)
- Basic electronics tools (soldering iron, multimeter)
- Arduino IDE or PlatformIO
- CAD software (Fusion 360, SolidWorks, or FreeCAD)

### Build Phases
1. **Mechanical Assembly** (15-20 hours)
2. **Electronics Integration** (10-15 hours) 
3. **Software Development** (10-15 hours)
4. **Testing & Tuning** (5-10 hours)

## 📋 Bill of Materials

| Category | Items | Cost |
|----------|-------|------|
| Actuators & Drives | 5 items | $89 |
| Sensors & Feedback | 4 items | $42 |
| Control Electronics | 5 items | $45 |
| Power System | 5 items | $38 |
| Mechanical Components | 6 items | $52 |
| Comfort & Interface | 3 items | $25 |
| Miscellaneous | 3 items | $15 |
| **TOTAL** | **31 items** | **$284** |

*See detailed BOM in `/docs/bill-of-materials.md`*

## 🔧 Hardware Architecture

### Mechanical System
- **Frame**: 20x20mm aluminum extrusion with 3D printed brackets
- **Actuation**: High-torque servo with cable drive system
- **Joints**: Ball bearing pivots with mechanical stops
- **Interface**: Padded cuffs with velcro attachment

### Electronics
- **Controller**: Arduino Nano 33 BLE (ARM Cortex-M4)
- **Motor Driver**: PCA9685 servo controller
- **Sensors**: Load cell (force), IMU (orientation), encoder (position)
- **Power**: 12V Li-ion battery with USB-C charging

### Control Architecture
```
User Input → Force Sensor → Controller → Motor Driver → Servo Motor
     ↑                            ↓
   Feedback ←── Position Encoder ←┘
```

## 🖥️ Software Stack

### Core Control Loop (100Hz)
1. **Sensor Reading** - Force, position, orientation
2. **Intent Detection** - Determine user desired motion
3. **Assist Calculation** - Compute required motor output
4. **Safety Checks** - Validate within limits
5. **Motor Command** - Output PWM to servo

### Control Modes
- **Force Amplification** - Multiply user input force
- **Gravity Compensation** - Counter arm weight
- **Impedance Control** - Variable stiffness/damping
- **Manual Mode** - Direct motor control via app

## 📁 Project Structure

```
iron-arm/
├── README.md                 # This file
├── docs/                     # Documentation
│   ├── assembly-guide.md     # Step-by-step build instructions
│   ├── bill-of-materials.md  # Detailed BOM with suppliers
│   ├── safety-manual.md      # Safety procedures and warnings
│   └── troubleshooting.md    # Common issues and solutions
├── hardware/                 # Physical design files
│   ├── cad/                  # 3D CAD files (Fusion 360)
│   ├── stl/                  # Ready-to-print STL files
│   ├── drawings/             # Technical drawings (PDF)
│   └── electronics/          # PCB designs and schematics
├── software/                 # All code
│   ├── arduino/              # Main controller code
│   ├── calibration/          # Sensor calibration utilities
│   ├── testing/              # Test and validation code
│   └── mobile-app/           # Optional smartphone app
├── simulations/              # Analysis and modeling
│   ├── mechanical/           # FEA and kinematic models
│   └── control/              # Control system modeling
└── testing/                  # Test data and reports
    ├── bench-tests/          # Component validation
    ├── integration/          # System-level tests
    └── user-studies/         # Human factors testing
```

## 🛠️ Build Instructions

### Phase 1: Mechanical Assembly

#### 1.1 Frame Construction
```bash
# Cut aluminum extrusion to lengths:
# - Upper arm: 300mm
# - Forearm: 280mm  
# - Cross braces: 2x 150mm
```

#### 1.2 3D Printing
Print all components in this order (total ~8 hours print time):
1. **Upper Arm Cuff Bracket** - Use PETG, 0.2mm layers, 100% infill
2. **Forearm Cuff Bracket** - Use PETG, 0.2mm layers, 100% infill  
3. **Elbow Joint Housing** - Use PETG, 0.15mm layers, 100% infill
4. **Motor Mount** - Use PLA+, 0.2mm layers, 80% infill
5. **Control Box** - Use PLA+, 0.2mm layers, 50% infill

#### 1.3 Assembly Steps
1. Install bearings in elbow joint housing
2. Mount servo motor to bracket
3. Route cables through housing system
4. Attach cuffs with padding
5. Install cable tensioning system

### Phase 2: Electronics Integration

#### 2.1 Circuit Assembly
- Solder prototype PCB following schematic in `/hardware/electronics/`
- Wire power distribution system with proper fusing
- Install emergency stop in accessible location
- Connect all sensor modules

#### 2.2 Sensor Calibration
```arduino
// Run calibration routine
void calibrateSensors() {
    calibrateLoadCell();    // Zero and span calibration
    calibrateIMU();         // Magnetometer and gyro offsets
    calibrateEncoder();     // Set zero position
}
```

### Phase 3: Software Development

#### 3.1 Control Algorithm
Core control loop implements force amplification:

```arduino
void controlLoop() {
    // Read sensors (100Hz)
    float userForce = readLoadCell();
    float armAngle = readEncoder();
    Vector3 armOrientation = readIMU();
    
    // Compute assist force
    float assistForce = userForce * amplificationFactor;
    assistForce = constrain(assistForce, -maxForce, maxForce);
    
    // Safety checks
    if (emergencyStop || outOfRange(armAngle)) {
        assistForce = 0;
    }
    
    // Output to motor
    setMotorTorque(assistForce);
    
    // Log data
    logData(userForce, assistForce, armAngle);
}
```

#### 3.2 Safety Systems
- **Watchdog Timer** - Resets system if code hangs
- **Force Limiting** - Software and hardware limits
- **Range Checking** - Prevents mechanical damage
- **Emergency Stop** - Immediate motor disable

## ⚡ Performance Specifications

| Parameter | Target | Measured |
|-----------|--------|----------|
| Max Assist Force | 150N | TBD |
| Response Time | <100ms | TBD |
| Battery Life | 2+ hours | TBD |
| System Weight | <2.5kg | TBD |
| Operating Range | 0-120° elbow | TBD |
| Force Accuracy | ±10N | TBD |

## 🔬 Testing Protocol

### Bench Tests
1. **Motor Performance** - Torque curves, speed tests
2. **Sensor Accuracy** - Calibration verification
3. **Battery Life** - Discharge curves under load
4. **Control Response** - Step response, frequency response

### Integration Tests  
1. **Force Amplification** - Measure actual vs commanded force
2. **Safety Systems** - Emergency stop, limit testing
3. **Ergonomics** - Comfort during extended wear
4. **Reliability** - 100-cycle endurance test

### User Acceptance Tests
1. **Ease of Use** - Don/doff time, control intuitiveness  
2. **Performance** - Perceived assistance, user satisfaction
3. **Safety** - Real-world usage scenarios

## 🛡️ Safety Considerations

### ⚠️ WARNINGS
- **Never bypass emergency stop** - Always accessible during operation
- **Respect force limits** - System can generate significant forces
- **Proper fitting required** - Loose cuffs can cause injury
- **Battery safety** - Follow Li-ion handling procedures
- **Regular inspection** - Check for wear, loose fasteners

### Safety Features
- Emergency stop button (hardware interrupt)
- Software force limiting (max 150N)
- Mechanical stops prevent overextension  
- Battery protection circuits
- Timeout shutdown (30 seconds no input)

## 🔧 Maintenance

### Daily Checks
- [ ] Battery charge level
- [ ] Emergency stop function
- [ ] Cuff padding condition
- [ ] No loose fasteners

### Weekly Maintenance
- [ ] Cable tension adjustment
- [ ] Sensor calibration check
- [ ] Lubricate moving parts
- [ ] Inspect electrical connections

### Monthly Service
- [ ] Deep clean all components
- [ ] Re-torque critical fasteners
- [ ] Battery capacity test
- [ ] Software backup and update

## 🚀 Future Enhancements

### Phase 2 Additions (v2.0)
- **Shoulder DOF** - Add shoulder flexion/extension
- **Force Feedback** - Haptic feedback for virtual interactions
- **Advanced Control** - Machine learning for user adaptation
- **Wireless Power** - Inductive charging system

### Phase 3 Additions (v3.0)
- **Full Arm** - Include wrist and hand assistance
- **Bilateral System** - Two-arm exoskeleton
- **Medical Integration** - Rehabilitation therapy modes
- **AR Interface** - Augmented reality control and feedback

## 📱 Mobile App Features

### Core Functions
- Real-time force and battery monitoring
- Assist level adjustment (1.5x to 3x)
- Data visualization and logging
- Safety system status

### Advanced Features  
- Custom force profiles
- Exercise mode with rep counting
- Performance analytics
- Remote diagnostics

## 🤝 Contributing

This is an open-source project! Contributions welcome:

### How to Contribute
1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Areas Needing Help
- [ ] Control algorithm optimization
- [ ] Mobile app development  
- [ ] Additional sensor integration
- [ ] Documentation and tutorials
- [ ] Safety testing and validation

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- OpenExo community for inspiration and reference designs
- Arduino and maker communities for extensive documentation
- All contributors and testers who helped make this possible

## 📞 Support

### Getting Help
- **Issues**: Use GitHub Issues for bugs and feature requests
- **Discussions**: Use GitHub Discussions for questions
- **Email**: [your-email] for safety-critical issues
- **Discord**: Join the maker community server

### Troubleshooting
Common issues and solutions in `/docs/troubleshooting.md`

---

## 🔥 Ready to Build?

1. **Order components** from BOM
2. **Print mechanical parts** (8 hours print time)
3. **Follow assembly guide** in `/docs/assembly-guide.md`
4. **Flash software** from `/software/arduino/`
5. **Calibrate sensors** using built-in routines
6. **Start lifting things!** 💪

**Estimated build time**: 40-60 hours over 2-3 months

**Skill level required**: Intermediate (basic electronics, 3D printing, programming)

---

*⚠️ Always prioritize safety. This is experimental equipment - use at your own risk and follow all safety procedures.*