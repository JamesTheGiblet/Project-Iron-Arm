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

## 🚀 Quick Start

### Prerequisites
- **Development Tools**: Text-to-CAD and PI Planner (build these first!)
- **Hardware**: 3D printer (200x200x200mm minimum build volume)  
- **Skills**: Basic electronics, 3D printing, Arduino/Python programming
- **Optional**: Raspberry Pi for advanced features

### Recommended Build Sequence
```
Week 1-2: 🛠️  Build Text-to-CAD → Design all mechanical parts
Week 3-4: 🔧  Phase 1 Build → Print and assemble mechanics  
Week 5:   📱  Build PI Planner → Plan electronics integration
Week 6-7: ⚡  Phase 2 Build → Wire and program electronics
Week 8:   🎯  Testing & Tuning → Optimize performance
```

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

## 🔗 Project Ecosystem

**Iron Arm** is part of a connected suite of development tools designed to streamline the entire exoskeleton development process:

### Related Projects
- **[Text to CAD Generator](../text-to-cad/)** - Generate 3D models from natural language for rapid prototyping of brackets and housings
- **[Project PI Planner](../pi-planner/)** - Visual GPIO planning tool for organizing sensor and actuator connections
- **Iron Arm** (this project) - The complete arm exoskeleton system

### Development Workflow
```
1. Plan Electronics → Project PI Planner → GPIO allocation
2. Design Components → Text to CAD → 3D printed parts  
3. Build System → Iron Arm → Complete exoskeleton
```

## 🏗️ Development Strategy

**Iron Arm** follows a tool-driven development approach, building supporting applications first to accelerate the main build:

### Development Phases
```
Phase 0: Tool Development (Weeks 1-5)
├── Week 1-2: Text to CAD Generator → Design all mechanical components  
├── Week 3-4: Phase 1 Build → Complete mechanical assembly
└── Week 5: PI Planner → Plan electronics integration

Phase 1: Electronics & Software (Weeks 6-8)  
├── Week 6-7: Electronics Integration → Wire and test systems
└── Week 8: Software Development → Control algorithms and tuning
```

### Tool Integration Benefits
- **Design Iteration** - Rapidly prototype components with Text-to-CAD
- **Validated Mechanics** - Prove physical design before electronics complexity
- **Planned Electronics** - Systematic GPIO allocation prevents wiring conflicts
- **Code Generation** - Jump-start software with PI Planner templates

```
iron-arm/
├── README.md                 # This file
├── docs/                     # Documentation
│   ├── assembly-guide.md     # Step-by-step build instructions
│   ├── bill-of-materials.md  # Detailed BOM with suppliers
│   ├── safety-manual.md      # Safety procedures and warnings
│   ├── gpio-planning.md      # Integration with PI Planner
│   └── troubleshooting.md    # Common issues and solutions
├── hardware/                 # Physical design files
│   ├── cad/                  # 3D CAD files (Fusion 360)
│   ├── stl/                  # Ready-to-print STL files
│   ├── drawings/             # Technical drawings (PDF)
│   ├── text-to-cad/         # Natural language CAD commands
│   └── electronics/          # PCB designs and schematics
├── software/                 # All code
│   ├── arduino/              # Main controller code
│   ├── pi-integration/       # Raspberry Pi GPIO code
│   ├── calibration/          # Sensor calibration utilities
│   ├── testing/              # Test and validation code
│   └── mobile-app/           # Optional smartphone app
├── simulations/              # Analysis and modeling
│   ├── mechanical/           # FEA and kinematic models
│   └── control/              # Control system modeling
├── tools/                    # Development utilities
│   ├── text-to-cad/         # CAD generation scripts
│   └── gpio-planner/        # Pin planning utilities
└── testing/                  # Test data and reports
    ├── bench-tests/          # Component validation
    ├── integration/          # System-level tests
    └── user-studies/         # Human factors testing
```

## 🛠️ Build Instructions

### Phase 0: Tool Development & Mechanical Build

#### Step 1: Text-to-CAD Development (Week 1-2)
**🔗 Priority: Build [Text to CAD Generator](../text-to-cad/) first**

1. **Set up Text-to-CAD environment**
2. **Design Iron Arm components using natural language:**
   ```
   Create upper arm cuff bracket: gray box with width 12, height 4, depth 2
   Make elbow joint housing: black cylinder with radius 3.5 and height 2.8  
   Generate motor mount: gray bracket with width 4.5, height 6, depth 3
   Create control box: blue enclosure with width 8, height 5, depth 3
   ```
3. **Refine designs** through iterative text commands
4. **Export STL files** for all mechanical components
5. **Document successful commands** for future use

#### Step 2: Mechanical Assembly (Week 3-4)
**Prerequisites: Completed Text-to-CAD development with exported STLs**

##### 2.1 Frame Construction
```bash
# Cut aluminum extrusion to lengths:
# - Upper arm: 300mm  
# - Forearm: 280mm
# - Cross braces: 2x 150mm
```

##### 2.2 3D Printing
Print components designed in Step 1 (~8 hours total print time):
1. **Upper Arm Cuff Bracket** - Use PETG, 0.2mm layers, 100% infill
2. **Forearm Cuff Bracket** - Use PETG, 0.2mm layers, 100% infill
3. **Elbow Joint Housing** - Use PETG, 0.15mm layers, 100% infill  
4. **Motor Mount** - Use PLA+, 0.2mm layers, 80% infill
5. **Control Box** - Use PLA+, 0.2mm layers, 50% infill

##### 2.3 Assembly Steps
1. Install bearings in elbow joint housing (Text-to-CAD designed)
2. Mount servo motor to bracket (custom generated mount)
3. Route cables through housing system
4. Attach cuffs with padding to custom brackets
5. Install cable tensioning system
6. **Validate mechanical function** - Test full range of motion

#### Step 3: PI Planner Development (Week 5)
**🔗 Build [Project PI Planner](../pi-planner/) for electronics integration**

1. **Develop GPIO planning interface**
2. **Configure Iron Arm sensor suite:**
   - Load Cell + HX711 amplifier
   - MPU9250 IMU
   - Emergency stop button
   - Status LEDs  
   - Servo motor control
   - Rotary encoder
3. **Generate pin allocation** avoiding conflicts
4. **Export Python code templates** with Iron Arm integration
5. **Create wiring diagrams** for assembly reference

### Phase 1: Electronics Integration (Week 6-7)

#### Electronics Assembly  
**Prerequisites: Completed PI Planner with validated GPIO plan**

1. **Follow PI Planner GPIO allocation** exactly
2. **Wire according to generated diagrams**
3. **Install emergency stop** in accessible location  
4. **Mount sensors in Text-to-CAD housings**
5. **Test each subsystem** before integration

### Phase 2: Software Development (Week 8)

#### Control System Implementation
**Prerequisites: Mechanical assembly complete, electronics wired per PI Planner**

1. **Flash PI Planner generated code** as starting framework
2. **Implement control algorithms** for force amplification
3. **Add safety systems** with emergency stop integration
4. **Tune performance** and optimize response

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
