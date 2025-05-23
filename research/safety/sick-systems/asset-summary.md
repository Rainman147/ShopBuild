# SICK Safety Systems - Asset Summary
## Hyperion Lights-Out Manufacturing Cell

### Executive Summary
SICK offers a comprehensive safety ecosystem specifically designed for automated manufacturing environments with minimal human intervention. Their integrated approach combines safety laser scanners, light curtains, and safety controllers to provide perimeter protection, machine access control, and collaborative robot safety functions ideal for lights-out operations.

---

## 1. Safety Laser Scanners

### microScan3 Series - Primary Perimeter Protection
**Model:** SICK microScan3 Core/Pro  
**Function:** Perimeter protection and area monitoring for robot cells  
**Safety Rating:** PLd, SIL2/SILCL2, Category 3, Type 3 (IEC EN 61496-3)

**Key Specifications:**
- **Scanning Performance:** 275° scanning angle, up to 9m protective range
- **Protective Fields:** Core: 8 configurable fields, Pro: 128 configurable fields
- **Simultaneous Monitoring:** Core: 4 fields, Pro: 8 fields
- **Technology:** safeHDDM™ scanning with 80,000+ pulses per scan
- **Environmental:** IP65 rated, resistant to dust/ambient light
- **Dimensions:** 112mm × 163.1mm × 111mm
- **Power:** 16.8-30Vdc (24Vdc nominal)
- **Communication:** PROFIsafe via PROFINET, CIP Safety via EtherNet/IP

**Applications for Hyperion Cell:**
- Robot perimeter protection during material handling operations
- Temporary zone reduction for pallet loading/unloading
- Area switching between setup, production, and maintenance modes
- Integration with KUKA robot safety systems

### nanoScan3 Series - Compact Safety Solution
**Model:** SICK nanoScan3 Core/Pro  
**Function:** Ultra-compact safety scanner for AGVs and mobile platforms  
**Safety Rating:** PLd, SIL2, Category 3, Type 3

**Key Specifications:**
- **Size:** 101mm × 101mm × 80mm (world's smallest safety scanner)
- **Range:** 3m protective field, 275° scanning angle
- **Fields:** Core: 8 configurable, Pro: 128 configurable
- **Technology:** safeHDDM™ scanning technology
- **Networking:** Safe EFI-Pro Ethernet-based networking

**Applications for Hyperion Cell:**
- AGV/mobile robot safety in material transport
- Collaborative robot workspace monitoring
- Access point protection for maintenance areas

### outdoorScan3 Series - Industrial Environment Protection
**Model:** SICK outdoorScan3  
**Function:** First IEC 62998 certified outdoor safety scanner  
**Safety Rating:** Certified for outdoor industrial applications

**Key Features:**
- All-weather operation capability
- Industrial environment certification
- AGV outdoor navigation support

---

## 2. Safety Light Curtains

### C4000 Series - Advanced Machine Access Protection
**Model:** SICK C4000 Advanced/Standard/Select  
**Function:** Machine access and hazardous point protection  
**Safety Rating:** PLe, SIL3, Type 4 (C4000 Advanced)

**Key Specifications:**
- **Height Range:** 300mm to 1,800mm
- **Resolution:** 14mm, 30mm options
- **Range:** Up to 20m depending on model
- **Features:** Integrated blanking, floating blanking, partial object detection
- **Integration:** Restart interlock (RES), External Device Monitoring (EDM)
- **Cascading:** Multiple system cascading capability

**Unique Advantages:**
- **No Muting Required:** C4000 eliminates need for traditional muting sensors/lamps
- **Material Flow Integration:** Allows defined objects while maintaining personnel protection
- **Flexible Configuration:** Blanking functions for cables, workpieces, fixtures

**Applications for Hyperion Cell:**
- Machine tool door protection
- Robot cell access points
- Conveyor integration points
- Maintenance area boundaries

### deTec4 Core Series - Point-of-Operation Protection
**Model:** SICK deTec4 Core  
**Function:** Slim profile point-of-operation protection  
**Safety Rating:** Type 4, SIL3, PLe

**Key Specifications:**
- **Height Range:** 300mm to 2,100mm
- **Resolution:** 14mm (7m range), 30mm (10m range)
- **Profile:** Ultra-slim design for close mounting
- **Integration:** Easy mounting and configuration

---

## 3. Safety Controllers and Systems

### Flexi Soft Safety Controller
**Model:** SICK Flexi Soft modular system  
**Function:** Programmable safety logic coordination  
**Safety Rating:** PLe, SIL3 capabilities

**Key Features:**
- Modular, scalable architecture
- Diagnostic interfaces for rapid commissioning
- Pre-configured robot integration packages
- Network communication capabilities

### Speed and Separation Monitoring (SSM)
**System:** sBot Speed CIP for KUKA robots  
**Function:** Collaborative robot speed and separation monitoring  
**Components:** microScan3 + Flexi Soft + EFI-pro gateway

**Zone Configuration:**
- **Green Zone:** Full speed operation (up to 2 m/s) when no personnel present
- **Orange Zone:** Speed reduction zone as detection/buffer area
- **Yellow Zone:** Safe speed monitoring zone with automatic stop if exceeded
- **Automatic Recovery:** System returns to full speed when zones clear

**Integration:** Pre-configured for KUKA KR C4 controllers via EtherNet/IP CIP Safety

---

## 4. Network and Communication

### Safe EFI-Pro Network
**Technology:** Ethernet-based safe networking  
**Capability:** General and safety-related data communications  
**Applications:** Control signals, safety shut-offs, diagnostics

### PROFIsafe Integration
**Compatibility:** Siemens S7-1500 F-CPU integration  
**Features:** Unified engineering via TIA Portal  
**Benefits:** Single controller for standard and safety functions

### CIP Safety via EtherNet/IP
**Applications:** Direct integration with Allen-Bradley and KUKA systems  
**Performance:** Real-time safety communication  
**Scalability:** Network-based safety architecture

---

## 5. Compliance and Standards

### Safety Standards Compliance
- **ISO 13849:** Performance Level d (PLd) and e (PLe)
- **IEC 61508:** Safety Integrity Level 2 and 3 (SIL2/SIL3)
- **IEC 62061:** Safety Category 3 and 4
- **EN 61496-3:** Type 3 and 4 safety devices
- **ISO TS15066:** Collaborative robot safety requirements
- **IEC 62998:** Outdoor safety device certification

### Lights-Out Operation Compliance
- Automated safety system reset capabilities
- Remote monitoring and diagnostics
- Predictive maintenance features
- Audit trail and safety logging

---

## 6. Integration Architecture for Hyperion Cell

### Primary Safety Network
**Backbone:** PROFIsafe via PROFINET to Siemens S7-1500F
**Backup:** CIP Safety via EtherNet/IP for KUKA robot integration
**Diagnostics:** Safe EFI-Pro for advanced monitoring

### Recommended Configuration
1. **Perimeter Protection:** 4× microScan3 Core scanners
2. **Machine Access:** 2× C4000 Advanced light curtains  
3. **Robot Integration:** 1× sBot Speed CIP system for KUKA
4. **Safety Logic:** 1× Flexi Soft controller system
5. **Emergency Systems:** Integrated with existing e-stop infrastructure

### Material Flow Integration
- **Pallet Handling:** C4000 material detection without muting
- **Conveyor Integration:** Blanking functions for automated material flow
- **Robot Workspace:** Dynamic area switching for operational modes

---

## 7. Competitive Advantages vs. Current BOM

### vs. Pilz PSENscan
**SICK Advantages:**
- Superior 9m range vs. Pilz 5.5m typical range
- 275° scanning vs. 190° typical
- Better integration with robot systems
- More flexible field configuration
- Superior environmental resistance

### vs. Banner EZ-SCREEN LS
**SICK Advantages:**
- C4000 eliminates muting complexity
- Better diagnostic capabilities
- Superior integration with safety PLCs
- Floating blanking for material flow
- Higher safety ratings available (PLe vs. PLd)

### Total System Integration
**SICK Benefits:**
- Single-source safety solution
- Pre-engineered robot integration packages
- Unified diagnostic and configuration tools
- Better technical support for complex applications
- Proven lights-out manufacturing experience

---

## 8. Cost Considerations

### Pricing Structure
**Note:** Specific pricing requires direct quotation based on configuration
**Typical Range Estimates:**
- microScan3 Core: $8,000-$12,000 per unit
- C4000 Advanced: $4,000-$6,000 per unit
- Flexi Soft controller: $3,000-$5,000 base system
- sBot Speed CIP: $15,000-$20,000 complete system

### ROI Factors
- Reduced downtime through better diagnostics
- Faster commissioning with pre-configured packages
- Lower maintenance costs
- Improved productivity through automated reset
- Compliance assurance for audits

### Implementation Costs
- Engineering/configuration: 10-15% of equipment cost
- Installation and commissioning: 15-20% of equipment cost
- Training and documentation: 5% of equipment cost

---

## 9. Recommendations

### Phase 1 - Core Safety Infrastructure
1. Replace Pilz PSENscan with SICK microScan3 Core (4 units)
2. Replace Banner EZ-SCREEN with SICK C4000 Advanced (2 units)
3. Implement Flexi Soft safety controller for centralized logic

### Phase 2 - Robot Integration
1. Implement sBot Speed CIP for KUKA robot collaboration
2. Configure dynamic area switching for operational modes
3. Integrate with Siemens S7-1500F via PROFIsafe

### Phase 3 - Advanced Features
1. Add nanoScan3 for mobile platform safety
2. Implement predictive maintenance features
3. Configure remote monitoring capabilities

### Critical Success Factors
- Early engagement with SICK applications engineering
- Comprehensive safety risk assessment
- Integration testing with all major systems
- Operator training on diagnostic capabilities
- Maintenance procedures for lights-out operation

---

**Status:** Recommended for implementation  
**Next Steps:** Obtain detailed quotation for Phase 1 components  
**Engineering Contact:** SICK Applications Engineering team  
**Timeline:** 8-12 weeks for delivery, 4-6 weeks for commissioning