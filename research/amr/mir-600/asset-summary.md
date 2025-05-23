# MiR 600 Autonomous Mobile Robot

| Spec                  | Value |
|-----------------------|-------|
| Function              | Autonomous material transport - 600kg payload |
| Workspace / Reach     | 1,304 × 864 mm load surface |
| Payload / Capacity    | 600 kg (1,322.8 lbs) |
| Interfaces            | REST API, OPC-UA (via gateway), Profinet, WiFi |
| Typical Price         | $150,000-180,000 FOB (robot + charging station) |
| Lead Time             | 12-16 weeks |
| Notes                 | IP52 rated, 24/7 operation, fleet management capable |

## Technical Specifications

### Performance
- **Maximum Speed**: 2.0 m/s (7.2 km/h / 4.4 mph)
- **Positioning Accuracy**: ±2mm (X), ±3mm (Y), ±0.25° (yaw) with VL-marker
- **Navigation**: SLAM + natural navigation, no infrastructure required
- **Operating Time**: Up to 11 hours active operation
- **Charging Ratio**: 1:12 (10 min charging = 2 hours runtime at max payload)

### Physical
- **Footprint**: 1,350 × 910 × 322 mm (L × W × H)
- **Weight**: 240 kg (529.1 lbs) including battery
- **Load Surface**: 1,304 × 864 mm (51.3 × 34 in)
- **Ground Clearance**: 27 mm (1.06 in)
- **Environmental Rating**: IP52 (dust and water resistant)

### Automation Features
- **Navigation**: 360° laser scanners, 3D cameras (30-2000mm detection)
- **Safety**: 12 safety functions per ISO 13849-1, 4 emergency stops
- **Fleet Management**: MiR Fleet Enterprise software for multi-robot coordination
- **Charging**: Autonomous docking with MiR Charge 48V station
- **Battery**: Removable lithium-ion, hot-swappable capability

## Integration Notes

### Communication Protocols
- **Primary**: REST API for ERP/MES/WMS integration
- **Fleet Management**: Event-driven architecture for 100+ robot fleets
- **OPC-UA**: Via third-party gateway (uaGate SI or similar)
- **Network**: WiFi 802.11ac, Ethernet for charging station

### Compatibility
- **Top Modules**: ShelfLift, Pallet Lift, Cart Carrier, custom modules
- **Pallet System**: Compatible with VERO-S, Erowa pallets via ShelfLift
- **Material Handling**: Integrates with conveyors, warehouse systems
- **Safety**: Collaborative operation with KUKA robots via speed monitoring

## Top Module Options

### MiR ShelfLift
- **Function**: Automated lifting and transport of shelves/carts
- **Capacity**: Up to 600kg including robot payload
- **Integration**: Tool cart transport from Zoller SmartCabinet
- **Operation**: Docks underneath, lifts off ground, transports

### Custom Modules Available
- **Pallet Lift**: For standard pallet handling
- **Cart Carrier**: Towing mechanism for wheeled carts
- **Conveyor Interface**: Direct loading/unloading automation

## Vendor Information

### Primary Contact
- **Company**: Mobile Industrial Robots (MiR)
- **Distributor**: Multiple authorized dealers in North America
- **Support**: 24/7 technical support, global service network
- **Training**: Comprehensive operator and maintenance training

### Alternative Suppliers
- **OTTO Motors**: $120,000-160,000, Rockwell integration
- **Zebra/Fetch**: $100,000-140,000, warehouse-focused
- **Locus Robotics**: $80,000-120,000, picking optimization

## Evaluation Criteria

### Strengths
- **Proven 24/7 Operation**: Over 5 million hours field experience
- **Infrastructure-Free**: No wires, magnets, or QR codes required
- **Fleet Scalability**: Proven systems with 100+ robots
- **Safety Certification**: ISO 13849-1 compliant, collaborative operation
- **Modular Design**: Extensive top module ecosystem
- **Industry 4.0 Ready**: Full API integration capabilities

### Weaknesses
- **Premium Pricing**: Higher cost than AGV alternatives
- **WiFi Dependency**: Requires robust wireless infrastructure
- **OPC-UA Integration**: Requires gateway for direct PLC communication
- **Load Height**: Limited to floor-level material handling

### Alternatives Considered
- **OTTO Motors KMP 600**: Higher payload (1,900kg), Rockwell native integration, $160,000
- **Zebra/Fetch AMR**: Warehouse optimization focus, lower manufacturing capability, $140,000
- **Traditional AGV**: Lower cost ($50,000-80,000), requires infrastructure, limited flexibility

### Integration with Hyperion Cell

#### Material Flow Applications
1. **Raw Stock Delivery**: Transport raw materials from warehouse to pallet tower
2. **Finished Parts Transport**: Move completed parts from cell to shipping/storage
3. **Tool Management**: Integrate with Zoller SmartCabinet for tool delivery
4. **Consumables Delivery**: Transport cutting fluids, tooling, maintenance supplies

#### Safety Integration
- **SICK Safety System**: Compatible with microScan3 Core perimeter monitoring
- **KUKA Collaboration**: Speed separation monitoring via sBot Speed CIP
- **Emergency Systems**: Integration with distributed emergency stop network

#### Control System Integration
- **Siemens S7-1500F**: REST API to OPC-UA gateway for PLC communication
- **MiR Fleet**: Centralized control and coordination with cell automation
- **HMI Integration**: Status monitoring on SIMATIC Comfort Panels

#### ROI Analysis
- **Manual Transport Cost**: $65,000/year (operator @ $25/hr + benefits)
- **AMR System Cost**: $180,000 initial + $15,000/year maintenance
- **Break-Even**: 2.8 years
- **Additional Benefits**: 24/7 operation, consistency, safety improvement
- **Scalability**: Add second robot for redundancy and capacity

## Rationale for Selection

The MiR 600 with ShelfLift represents the optimal balance of capability, reliability, and integration potential for the Hyperion lights-out cell. While premium-priced, the system's proven 24/7 operation, infrastructure-free deployment, and extensive API integration capabilities align perfectly with lights-out manufacturing requirements. The collaborative safety features and fleet management software provide the foundation for future expansion and optimization.