# SICK Safety Systems - Integration Requirements
## Hyperion Lights-Out Manufacturing Cell

### Executive Summary
This document defines the technical integration requirements for implementing SICK safety systems within the Hyperion lights-out manufacturing cell. The integration encompasses safety laser scanners, light curtains, safety controllers, and their communication with existing automation infrastructure including Siemens S7-1500 PLC, KUKA robots, and DN Solutions machine tools.

---

## 1. Network Architecture Integration

### Primary Safety Network - PROFIsafe
**Protocol:** PROFIsafe over PROFINET  
**Primary Controller:** Siemens S7-1500F F-CPU  
**Topology:** Star configuration with managed switches

**Network Requirements:**
- Dedicated PROFINET safety network (isolated from standard I/O)
- Managed switches with PROFIsafe support (Siemens SCALANCE X-200)
- Maximum cable length: 100m per segment
- Update time: ≤10ms for safety functions
- Network redundancy: Ring topology with MRP support

**Device Configuration:**
```
Safety Network Map:
├── Siemens S7-1500F (Safety PLC)
├── SICK microScan3 #1 (Perimeter North)
├── SICK microScan3 #2 (Perimeter East) 
├── SICK microScan3 #3 (Perimeter South)
├── SICK microScan3 #4 (Perimeter West)
├── SICK C4000 #1 (Machine Access)
├── SICK C4000 #2 (Robot Cell Access)
└── SICK Flexi Soft (Safety Controller)
```

### Secondary Safety Network - CIP Safety
**Protocol:** CIP Safety over EtherNet/IP  
**Primary Integration:** KUKA KR C5 robot controller  
**Application:** Speed and separation monitoring

**Network Requirements:**
- Dedicated EtherNet/IP safety network
- Managed switches with CIP Safety support
- RPI (Requested Packet Interval): ≤8ms
- Connection timeout: 100ms maximum

---

## 2. Siemens S7-1500 Integration

### Hardware Requirements
**CPU:** S7-1500F F-CPU (existing - confirmed compatible)  
**Safety I/O:** ET-200SP F-modules for discrete safety inputs  
**Communication:** CM 1542-5 PROFINET interface (safety capable)

### Safety Program Structure
```
Safety Program Organization:
├── Safety FB1: Perimeter Monitoring
│   ├── microScan3 Scanner Array Processing
│   ├── Zone Configuration Management  
│   └── Operational Mode Switching
├── Safety FB2: Access Point Control
│   ├── C4000 Light Curtain Logic
│   ├── Material Flow Detection
│   └── Muting Logic (if required)
├── Safety FB3: Robot Integration
│   ├── Safe Stop Commands
│   ├── Speed Monitoring Interface
│   └── Collaboration Zone Management
└── Safety FB4: Emergency Systems
    ├── E-Stop Processing
    ├── Safety Door Monitoring
    └── System Reset Logic
```

### Configuration Requirements
**TIA Portal Version:** V17 or higher with Safety Advanced  
**Library Requirements:** SICK safety function blocks  
**Safety Integrity:** SIL2/PLd minimum for all safety functions

**Safety Tags Allocation:**
```yaml
Safety Inputs:
  - Scanner_Zone_1_Clear: BOOL
  - Scanner_Zone_2_Clear: BOOL  
  - Scanner_Zone_3_Clear: BOOL
  - Scanner_Zone_4_Clear: BOOL
  - LightCurtain_1_Clear: BOOL
  - LightCurtain_2_Clear: BOOL
  - Emergency_Stop_OK: BOOL
  - Safety_Doors_Closed: BOOL

Safety Outputs:
  - Robot_Safe_Stop: BOOL
  - Machine_Safe_Stop: BOOL
  - Conveyor_Safe_Stop: BOOL
  - Safety_Relay_Enable: BOOL
```

---

## 3. KUKA Robot Integration

### KR C5 Controller Configuration
**Software Requirements:**
- KUKA.SafeOperation technology package
- KUKA.SafeRangeMonitoring option
- PROFIsafe interface card for KR C5

### Speed and Separation Monitoring
**sBot Speed CIP Integration:**
- Direct connection via EtherNet/IP CIP Safety
- Pre-configured KUKA safety functions
- Automatic speed scaling based on human presence

**Safety Zones Configuration:**
```yaml
Safety Zones:
  Green_Zone:
    description: "No person detected"
    max_speed: 2000  # mm/s
    safety_function: "Normal operation"
    
  Orange_Zone: 
    description: "Person approaching (detection zone)"
    max_speed: 1000  # mm/s
    safety_function: "Speed reduction buffer"
    
  Yellow_Zone:
    description: "Person in collaboration area" 
    max_speed: 250   # mm/s (ISO TS15066 compliant)
    safety_function: "Collaborative speed monitoring"
    
  Red_Zone:
    description: "Safety violation"
    max_speed: 0     # mm/s
    safety_function: "Safety Stop 1"
```

### Robot Safety Functions
**Integration Points:**
- Safe stop inputs from safety scanners
- Workspace monitoring feedback
- Automatic restart after zone clearance
- Speed override for manual mode

---

## 4. DN Solutions DVF 6500 Integration

### Machine Tool Safety Interface
**Safety Functions Required:**
- Spindle safe stop
- Axis safe stop  
- Door interlock monitoring
- Coolant system safe stop

**Interface Method:**
- Safety relay outputs from SICK Flexi Soft
- Hardwired to machine safety inputs
- Monitoring of machine ready signals

**Safety Logic:**
```
Machine Safety Interlocks:
├── Perimeter Clear AND
├── Access Points Clear AND  
├── Robot Safe State AND
├── Manual Enable (if in manual mode)
└── → Machine Enable Output
```

---

## 5. Material Handling Integration

### Fastems FPT-630 Pallet Tower
**Safety Requirements:**
- Pallet transport path monitoring
- Load/unload position safety
- Material flow through protected areas

**C4000 Light Curtain Configuration:**
- Blanking functions for pallet profiles
- Floating blanking for variable load heights
- No muting required (SICK C4000 advantage)

### Conveyor System Integration
**Safety Functions:**
- Emergency stop of all conveyors
- Safe speed monitoring during loading
- Material jam detection safety

---

## 6. Emergency Stop System Integration

### Distributed E-Stop Architecture
**Components:**
- Existing emergency stop stations (maintain)
- Safety relay system integration
- Central safety logic in S7-1500F

**Integration Requirements:**
- E-stop status monitoring in all SICK devices
- Automatic reset capability for lights-out operation
- Manual reset requirement for personnel access modes

### Reset Logic
```yaml
Automatic Reset Conditions:
  - All safety zones clear for >5 seconds
  - No active alarms
  - System in automatic mode
  - No maintenance mode active

Manual Reset Required:
  - Personnel access detected
  - Safety door opened
  - Manual mode selected
  - After any safety stop category 0
```

---

## 7. Operational Mode Management

### Mode Selection Interface
**Modes Required:**
1. **Lights-Out Production**
   - Full automatic operation
   - Maximum speed settings
   - Automatic reset enabled
   - Remote monitoring only

2. **Setup/Programming**
   - Reduced robot speeds
   - Personnel access allowed
   - Enhanced monitoring zones
   - Manual reset required

3. **Maintenance**
   - All motion systems stopped
   - Safety systems bypassed (with key)
   - Full access permissions
   - Detailed audit logging

### Mode Switching Logic
**Safety Requirements:**
- Mode changes require safety clearance
- Automatic return to production mode after setup timeout
- Mode status visible on all HMIs
- Mode change logging for audit trail

---

## 8. Diagnostic and Monitoring Integration

### SICK Safety System Diagnostics
**Data Points:**
- Scanner contamination levels
- Light curtain beam interruption counts
- Safety controller health status
- Communication status for all devices

**Integration with Siemens:**
- Diagnostic data via PROFINET diagnostics
- Predictive maintenance alerts
- Automatic maintenance scheduling

### Remote Monitoring Capabilities
**Requirements:**
- VPN access for SICK service technicians
- Remote diagnostic capabilities
- Performance trending data
- Automatic alert generation

---

## 9. Installation and Commissioning

### Physical Installation Requirements
**Scanner Mounting:**
- Height: 300-400mm above floor level
- Protection: IP65 rated enclosures
- Vibration isolation from machine tools
- Clear line-of-sight for all zones

**Light Curtain Installation:**
- Mounting brackets for machine doors
- Alignment tools required
- Cable routing through machine conduits
- Integration with existing door switches

### Commissioning Sequence
1. **Phase 1: Individual Device Testing**
   - Scanner range and angle verification
   - Light curtain alignment and function
   - Safety controller I/O testing

2. **Phase 2: Network Integration Testing**
   - PROFIsafe communication verification
   - Safety function response time testing
   - Diagnostic data flow confirmation

3. **Phase 3: System Integration Testing**
   - Robot safety function verification
   - Machine tool safety integration
   - Emergency stop system testing

4. **Phase 4: Operational Testing**
   - Lights-out mode verification
   - Mode switching functionality
   - Automatic reset testing

### Validation and Documentation
**Required Documentation:**
- Safety validation report (per IEC 62061)
- Risk assessment updates
- Operating procedures
- Maintenance procedures
- Training documentation

---

## 10. Performance Requirements

### Safety Response Times
**Maximum Allowable:**
- Scanner detection to stop: 200ms
- Light curtain interrupt to stop: 150ms
- Emergency stop to full stop: 500ms
- Network communication cycle: 10ms

### Availability Requirements
**Target Metrics:**
- Safety system availability: 99.9%
- Mean time between failures: >10,000 hours
- Mean time to repair: <2 hours
- Lights-out operation capability: 16+ hours continuous

### Environmental Specifications
**Operating Conditions:**
- Temperature: 0°C to +50°C
- Humidity: 90% non-condensing
- Vibration resistance per IEC 60068-2-6
- EMC compliance per EN 61000-6-2

---

## 11. Maintenance and Support

### Preventive Maintenance Schedule
**Weekly:**
- Scanner lens cleaning verification
- Light curtain alignment check
- System diagnostic review

**Monthly:**
- Safety function testing
- Communication status verification
- Performance data analysis

**Annually:**
- Complete safety validation
- Risk assessment review
- System software updates

### Support Infrastructure
**SICK Service Agreement:**
- 24/7 remote diagnostic access
- Guaranteed response times
- Preventive maintenance services
- Software update management

---

## 12. Project Timeline and Dependencies

### Critical Path Items
**Week 1-2:** Safety system design finalization
**Week 3-4:** Equipment procurement and delivery
**Week 5-6:** Installation and physical integration
**Week 7-8:** Software configuration and testing
**Week 9-10:** System validation and documentation

### Dependencies
- Siemens S7-1500F safety programming completion
- KUKA robot safety option installation
- Machine tool safety interface preparation
- Network infrastructure preparation

### Risk Mitigation
**Technical Risks:**
- Communication protocol compatibility testing
- Safety function validation complexity
- Integration with existing systems

**Schedule Risks:**
- Equipment delivery delays
- Commissioning complexity
- Certification and validation time

---

**Document Status:** Draft for review  
**Next Review:** System design approval meeting  
**Approval Required:** Safety engineer, automation engineer, project manager