# MiR 600 Integration Requirements for Hyperion Cell

## Overview

This document defines the technical requirements for integrating MiR 600 autonomous mobile robots into the Hyperion lights-out manufacturing cell. Integration encompasses communication protocols, safety systems, material flow coordination, and operational procedures for 24/7 automated operation.

## System Architecture

### Cell Control Integration
```
Siemens S7-1500F PLC
    ↕ OPC-UA Gateway (uaGate SI)
    ↕ Ethernet/WiFi
MiR Fleet Management Server
    ↕ REST API
MiR 600 Robot(s)
```

### Communication Requirements

#### Primary Integration: REST API → OPC-UA Gateway
- **MiR Fleet Server**: Centralized robot coordination and job management
- **Gateway Solution**: Softing uaGate SI or equivalent for protocol translation
- **PLC Integration**: OPC-UA client on Siemens S7-1500F (TIA Portal V16+)
- **Network**: Dedicated industrial WiFi (802.11ac) for robot mobility

#### Data Exchange Points
**From PLC to MiR Fleet:**
- Material requests (part numbers, quantities, destinations)
- Cell status (machine ready, pallet tower position)
- Safety zone status (area clear for robot entry)
- Emergency stop conditions

**From MiR Fleet to PLC:**
- Robot position and status
- Job completion confirmations
- Material delivery timestamps
- Battery and maintenance alerts

## Material Flow Integration

### Raw Stock Delivery Workflow

#### 1. Warehouse to Pallet Tower
**Trigger**: PLC detects low stock on pallet tower
**Process Flow:**
1. PLC sends material request to MiR Fleet via OPC-UA gateway
2. MiR Fleet assigns job to available robot
3. Robot navigates to warehouse staging area
4. ShelfLift module loads pallet/cart from designated pickup point
5. Robot transports to pallet tower drop-off zone
6. KUKA robot transfers material from cart to tower
7. Robot returns cart to warehouse staging area
8. Job completion confirmation sent to PLC

**Integration Points:**
- Warehouse management system interface for stock allocation
- Pallet tower position feedback for optimal drop-off location
- KUKA robot coordination for synchronized material transfer

#### 2. Tool Delivery from SmartCabinet
**Trigger**: Tool change request from machine tool or preventive schedule
**Process Flow:**
1. Machine tool or TMS system requests specific tools
2. PLC coordinates with Zoller SmartCabinet system
3. MiR Fleet receives tool delivery job
4. Robot with custom tool cart module navigates to SmartCabinet
5. SmartCabinet loads required tools onto robot cart
6. Robot delivers to machine tool vicinity
7. KUKA robot transfers tools to machine ATC
8. Robot returns empty cart to SmartCabinet

### Finished Parts Transport

#### 1. Cell to Shipping/Storage
**Trigger**: Part completion and quality approval
**Process Flow:**
1. ZEISS CMM completes measurement and approves part
2. PLC generates finished goods transport request
3. MiR Fleet assigns robot for pickup
4. Robot positions at cell output conveyor/staging area
5. KUKA robot loads finished parts onto robot platform
6. Robot transports to designated shipping/storage area
7. Parts unloaded at destination (manual or automated)
8. Robot returns to cell for next cycle

## Safety System Integration

### SICK Safety System Coordination

#### Perimeter Protection
- **microScan3 Core Scanners**: Monitor cell perimeter for human entry
- **Integration**: Safety scanner status communicated to MiR Fleet
- **Behavior**: Robot automatically reduces speed or stops when humans detected
- **Override**: Maintenance mode allows controlled human-robot collaboration

#### Collaborative Operation Zones
- **sBot Speed CIP**: Monitors KUKA robot speed and position
- **AMR Coordination**: MiR 600 receives robot position data
- **Dynamic Zones**: AMR adjusts path and speed based on KUKA arm position
- **Emergency Response**: Both systems respond to emergency stop activation

### AMR-Specific Safety Features

#### Built-in Safety Systems
- **360° Laser Scanners**: Continuous perimeter monitoring
- **3D Cameras**: Overhead obstacle detection (30-2000mm height)
- **Emergency Stops**: 4 physical stops + software emergency stop
- **Speed Monitoring**: Automatic speed reduction in congested areas

#### Safety Zone Configuration
```
Zone 1: High-Speed Transit (1.5-2.0 m/s)
Zone 2: Approach Areas (1.0 m/s)
Zone 3: Work Areas (0.5 m/s)
Zone 4: Human Interaction (0.3 m/s + stop)
```

## Infrastructure Requirements

### Network Infrastructure

#### WiFi Requirements
- **Standard**: 802.11ac (minimum), WiFi 6 preferred
- **Coverage**: Seamless throughout cell and transport routes
- **Bandwidth**: 10 Mbps minimum per robot
- **Latency**: <50ms to MiR Fleet server
- **Redundancy**: Dual access points for critical areas

#### Ethernet Backbone
- **MiR Fleet Server**: Dedicated server for robot coordination
- **Gateway Server**: OPC-UA to REST API translation
- **PLC Network**: Profinet for Siemens automation
- **Security**: Industrial firewall with VPN capability

### Physical Infrastructure

#### Charging Infrastructure
- **MiR Charge 48V Station**: Autonomous docking and charging
- **Location**: Accessible from main transport routes
- **Power**: 480V 3-phase, 15A circuit
- **Backup**: Secondary charging location for redundancy

#### Floor Requirements
- **Surface**: Smooth concrete, epoxy coating preferred
- **Tolerance**: ±5mm levelness across transport routes
- **Markings**: Optional VL-markers for high-precision docking
- **Obstacles**: Clear paths with 1.5m minimum width

## Integration with Existing Systems

### Siemens S7-1500F PLC Integration

#### OPC-UA Server Configuration
```
TIA Portal Configuration:
- OPC-UA Server enabled
- Security: Sign & Encrypt (recommended)
- User Authentication: Username/password
- Certificate Management: X.509 certificates
- Access Control: Read/write permissions per data block
```

#### Data Blocks for AMR Integration
```
DB_AMR_Control:
- Material_Request (BOOL array)
- Destination_Address (INT array)  
- Priority_Level (INT array)
- Cell_Status (WORD)

DB_AMR_Status:
- Robot_Position (REAL array)
- Job_Status (INT array)
- Battery_Level (REAL array)
- Error_Codes (WORD array)
```

### KUKA Robot Coordination

#### KR C5 Controller Integration
- **Safety Interface**: PROFIsafe for emergency stop coordination
- **Position Coordination**: Shared coordinate system with AMR
- **Handoff Protocols**: Defined sequences for material transfer
- **Collision Avoidance**: Dynamic path planning with AMR position data

#### Shared Work Envelope
```
Safe Zones:
- Robot Priority Zone: AMR stops/waits
- AMR Priority Zone: Robot retracts/holds
- Shared Zone: Speed monitoring active
- Handoff Zone: Coordinated material transfer
```

### Zoller SmartCabinet Integration

#### Tool Management Workflow
1. **TMS Request**: Tool required for upcoming job
2. **SmartCabinet Prep**: Tools prepared and loaded on cart
3. **AMR Dispatch**: MiR 600 with tool cart module deployed
4. **Automated Loading**: SmartCabinet automation loads tools
5. **Transport**: Robot delivers to machine tool
6. **Transfer**: KUKA robot moves tools to ATC magazine
7. **Return**: Empty cart returned to SmartCabinet

#### Integration Requirements
- **Communication**: Ethernet connection to SmartCabinet control system
- **Cart Design**: Custom tool cart compatible with MiR ShelfLift
- **RFID Integration**: Tool tracking through transport process
- **Safety**: Light curtains during automated loading/unloading

## Operational Procedures

### 24/7 Lights-Out Operation

#### Autonomous Operation Mode
- **Job Scheduling**: MiR Fleet manages job queue and robot assignment
- **Battery Management**: Automatic charging schedule optimization
- **Error Recovery**: Automated restart procedures for common issues
- **Monitoring**: Remote monitoring with alert escalation

#### Maintenance Procedures
- **Predictive**: Battery health, navigation sensor status
- **Scheduled**: Weekly inspection and cleaning routines
- **Emergency**: Procedures for robot recovery and bypass

### Human Interface Procedures

#### Operator Access
- **Safety Key**: Override for maintenance mode entry
- **Speed Reduction**: Automatic when humans detected
- **Manual Override**: Emergency stop and manual robot positioning
- **Status Display**: Robot status on SIMATIC HMI panels

#### Maintenance Access
- **Lockout/Tagout**: Integration with cell LOTO procedures
- **Diagnostic Mode**: Full sensor data and path visualization
- **Manual Control**: Direct robot positioning and testing
- **Calibration**: Navigation system and sensor calibration

## Performance Monitoring

### Key Performance Indicators

#### Operational Metrics
- **Availability**: Target >95% operational time
- **Throughput**: Material deliveries per hour
- **Efficiency**: Battery utilization and charging optimization
- **Safety**: Near-miss incidents and safety system activations

#### Integration Health
- **Communication**: Network latency and packet loss
- **Coordination**: Successful handoffs with KUKA robot
- **Reliability**: Job completion rate and error frequency
- **Maintenance**: Predictive indicators and service intervals

### Data Collection and Analytics

#### MiR Fleet Analytics
- Real-time robot status and performance
- Historical data for optimization
- Predictive maintenance alerts
- Fleet utilization reporting

#### Integration with Cell MES
- Production correlation with material flow
- Quality impact tracking
- Overall equipment effectiveness (OEE)
- Cost per transport analysis

## Security Considerations

### Cybersecurity Requirements
- **Network Segmentation**: Isolated AMR network segment
- **Authentication**: Strong passwords and certificate-based auth
- **Encryption**: All communications encrypted (TLS 1.2+)
- **Access Control**: Role-based permissions for different users
- **Monitoring**: Network traffic analysis and intrusion detection

### Physical Security
- **Robot Access**: Secured service panels and emergency stops
- **Charging Station**: Protected power connections
- **Infrastructure**: Secured network equipment and cabling

## Implementation Timeline

### Phase 1: Infrastructure (Weeks 1-4)
- Network infrastructure installation
- Charging station setup
- Floor preparation and marking
- Safety system integration testing

### Phase 2: Single Robot Deployment (Weeks 5-8)
- MiR 600 delivery and commissioning
- MiR Fleet server setup and configuration
- OPC-UA gateway installation and testing
- Basic material transport workflow validation

### Phase 3: Full Integration (Weeks 9-12)
- KUKA robot coordination programming
- SmartCabinet integration completion
- Safety system final validation
- Operator training and procedure finalization

### Phase 4: Optimization (Weeks 13-16)
- Performance tuning and optimization
- Advanced fleet features activation
- Predictive maintenance setup
- Full 24/7 operation validation

## Conclusion

The integration of MiR 600 AMRs into the Hyperion cell requires careful coordination of communication protocols, safety systems, and operational procedures. The modular approach allows for phased implementation while building toward full lights-out operation capability. Success depends on robust network infrastructure, comprehensive safety integration, and careful attention to human-robot interaction protocols.