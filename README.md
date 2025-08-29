# ARM EXOSKELETON REQUIREMENTS DOCUMENT

**Project:** "Iron Arm" - Single DOF Elbow Assist Exoskeleton

**Version:** 1.0

**Purpose:** For fun, learning, and demonstration


---


## 1. FUNCTIONAL REQUIREMENTS


### Primary Function

- **FR-01**: System SHALL provide assistive force to elbow flexion/extension motion

- **FR-02**: System SHALL amplify user input force by a configurable factor (1.5x to 3x)

- **FR-03**: System SHALL operate transparently when user is not applying force

- **FR-04**: System SHALL provide smooth, responsive assistance with <100ms delay


### Control Requirements

- **FR-05**: System SHALL detect user intent through force sensing

- **FR-06**: System SHALL provide variable assist levels (low/medium/high)

- **FR-07**: System SHALL include emergency stop functionality

- **FR-08**: System SHALL have power on/off control


### Range of Motion

- **FR-09**: System SHALL allow natural elbow motion from 0° to 120° flexion

- **FR-10**: System SHALL NOT restrict normal arm movement when unpowered

- **FR-11**: System SHALL accommodate shoulder motion without interference


---


## 2. PERFORMANCE REQUIREMENTS


### Mechanical Performance

- **PR-01**: Maximum assist force: 150N at forearm cuff

- **PR-02**: System backlash: <5° of joint angle

- **PR-03**: Mechanical efficiency: >70%

- **PR-04**: Operating noise level: <60dB at 1m distance


### Electrical Performance

- **PR-05**: Battery life: Minimum 2 hours continuous operation

- **PR-06**: Control loop frequency: 100Hz minimum

- **PR-07**: System response time: <100ms from force input to assist output

- **PR-08**: Power consumption: <50W average, <100W peak


### Dynamic Performance

- **PR-09**: System SHALL track user motion up to 180°/sec angular velocity

- **PR-10**: Force tracking accuracy: ±10N

- **PR-11**: Stable operation across full temperature range: 0°C to 40°C


---


## 3. SAFETY REQUIREMENTS


### Mechanical Safety

- **SF-01**: System SHALL include mechanical stops to prevent overextension

- **SF-02**: All user contact surfaces SHALL be padded and smooth

- **SF-03**: System SHALL fail to safe (unpowered) state on any fault

- **SF-04**: Maximum force output SHALL be software and hardware limited


### Electrical Safety

- **SF-05**: System SHALL include emergency stop accessible during operation

- **SF-06**: Battery SHALL include overcharge/overdischarge protection

- **SF-07**: All electrical components SHALL be protected from user contact

- **SF-08**: System SHALL shut down if overheating detected


### Control Safety

- **SF-09**: Force amplification SHALL have maximum limit (3x)

- **SF-10**: System SHALL timeout and stop if no user input for 30 seconds

- **SF-11**: System SHALL include watchdog timer for control system

- **SF-12**: All sensor failures SHALL result in safe shutdown


---


## 4. PHYSICAL REQUIREMENTS


### Size and Weight

- **PH-01**: Total system weight: <2.5kg

- **PH-02**: System SHALL fit users with arm length 55-75cm

- **PH-03**: Cuffs SHALL accommodate arm circumference 20-40cm

- **PH-04**: Maximum system width: <15cm from arm centerline


### Ergonomics

- **PH-05**: System SHALL be donnable/doffable by user in <2 minutes

- **PH-06**: No pressure points or discomfort during 30-minute wear test

- **PH-07**: System weight distribution SHALL not cause user fatigue

- **PH-08**: All controls SHALL be accessible while wearing system


### Durability

- **PH-09**: System SHALL withstand 1000 flex cycles without degradation

- **PH-10**: System SHALL survive 1m drop test when not worn

- **PH-11**: Water resistance: IP32 (protected against spraying water)


---


## 5. INTERFACE REQUIREMENTS


### User Interface

- **UI-01**: Power indicator (LED)

- **UI-02**: Battery level indicator (3-state LED or display)

- **UI-03**: Assist level indicator

- **UI-04**: Emergency stop button (red, prominent)

- **UI-05**: Mode selection (assist level adjustment)


### Connectivity

- **UI-06**: USB-C charging port

- **UI-07**: Optional: Bluetooth connectivity for smartphone app

- **UI-08**: Optional: Data logging capability


---


## 6. MANUFACTURING REQUIREMENTS


### Materials

- **MF-01**: Frame components: 3D printable (PLA+/PETG)

- **MF-02**: Structural elements: Standard aluminum extrusion (20x20mm)

- **MF-03**: All fasteners: Stainless steel or aluminum

- **MF-04**: User contact materials: Soft, washable, hypoallergenic


### Assembly

- **MF-05**: System SHALL be assemblable with common tools

- **MF-06**: No specialized manufacturing equipment required

- **MF-07**: All custom parts SHALL be 3D printable on 200x200mm bed

- **MF-08**: Assembly time: <8 hours for experienced maker


### Cost

- **MF-09**: Target bill of materials cost: <$300

- **MF-10**: All components SHALL be available from standard suppliers


---


## 7. TESTING REQUIREMENTS


### Functional Testing

- **TS-01**: Force amplification accuracy test

- **TS-02**: Response time measurement

- **TS-03**: Battery life test

- **TS-04**: Range of motion verification


### Safety Testing

- **TS-05**: Emergency stop function test

- **TS-06**: Maximum force limit test

- **TS-07**: Fault condition response test

- **TS-08**: Overload protection test


### User Testing

- **TS-09**: Comfort test (30-minute wear)

- **TS-10**: Ease of use test (don/doff time)

- **TS-11**: User satisfaction survey


---


## 8. SUCCESS CRITERIA


### Minimum Viable Product (MVP)

- ✓ Provides noticeable force assistance

- ✓ Safe for operator use

- ✓ Operates for minimum battery life

- ✓ Meets basic ergonomic requirements


### Stretch Goals

- ✓ Smartphone connectivity and control

- ✓ Data logging and analysis

- ✓ Multiple user profiles

- ✓ Advanced control algorithms (impedance control)


---


## 9. CONSTRAINTS AND ASSUMPTIONS


### Constraints

- **Budget**: Maximum $300 for materials

- **Timeline**: 3-6 months for complete build

- **Tools**: Standard maker tools (3D printer, basic electronics)

- **Experience**: Single builder with robotics background


### Assumptions

- User has normal arm mobility and strength

- Indoor use environment

- Occasional use (not daily medical device)

- User can follow safety procedures


---


## 10. ACCEPTANCE CRITERIA


The system will be considered complete when:

1. All functional requirements are met

2. All safety requirements are verified

3. User can safely don/doff and operate the system

4. System provides measurable force assistance

5. Documentation and user manual are complete


**Sign-off**: Ready for detailed design phase upon requirements approval.


There's our comprehensive requirements document! This gives us a solid foundation to work from and helps prevent scope creep.


**Key highlights:**

- **150N assist force** - enough to really feel the difference

- **2-hour battery life** - reasonable for demo/experimentation

- **<100ms response time** - fast enough to feel natural

- **<2.5kg total weight** - won't exhaust you wearing it

- **$300 budget** - achievable for a hobbyist project


**Critical requirements to focus on:**

1. **Safety first** - Emergency stops, force limits, fail-safe behavior

2. **User comfort** - If it's uncomfortable, you won't want to use it

3. **Responsive control** - The magic is in making it feel intuitive


**Requirements that drive major design decisions:**

- The 150N force requirement determines our motor sizing

- The 100Hz control loop sets our microcontroller needs

- The 2-hour battery life drives our power budget

- The donning time requirement affects our cuff/harness design


This spec also gives us clear test criteria - we'll know we're done when we can check off all these boxes.


Any requirements you'd like to modify or add? We could adjust the assist force levels, battery life, or add requirements for things like wireless connectivity or data logging. 
