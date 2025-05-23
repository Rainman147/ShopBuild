# Fastems FPT-630 Pallet Tower

| Spec                  | Value |
|-----------------------|-------|
| Function              | Automated pallet storage tower for 500-630mm pallets |
| Workspace / Reach     | 16 m² footprint, 2-4 level configurable storage |
| Payload / Pallet size | 500-630mm pallets, configurable heights |
| Interfaces            | MMS Manufacturing Management Software, Ethernet, OPC-UA compatible |
| Typical Price         | $185,000 - $250,000 FOB (estimate based on market positioning) |
| Lead Time             | 16 weeks |
| Notes                 | Lights-out capable, integrates with 90+ machine brands, compact footprint |

## Technical Specifications

### Performance
- **Storage capacity**: Up to 24 pallets in configurable 2-4 levels
- **Pallet sizes**: 500-630mm standard interfaces
- **Cycle time**: Fast automated pallet exchange (specific times TBD)
- **Load capacity**: Standard pallet + workpiece loads

### Physical
- **Footprint**: 16 m² (175 sq ft) for FPT-1000 model
- **Height**: Configurable 2-4 levels
- **Weight**: TBD - requires engineering consultation
- **Power requirements**: 400V 3-phase (typical European standard)
- **Air requirements**: Pneumatic systems for pallet clamping

### Automation Features
- **Pallet changer**: Automated loading/unloading with robot interface
- **Workpiece changer**: Compatible with 400x400mm, 500x500mm, and 630mm pallets
- **Probing**: Integration with machine tool probing systems
- **Safety**: Emergency stops, safety interlocks, light curtain integration

## Integration Notes

### Communication Protocols
- **Primary**: Manufacturing Management Software (MMS) with modern connectivity
- **Secondary**: Ethernet, fieldbus protocols, OPC-UA server capability
- **I/O**: 24V DC digital I/O for status and control signals

### Compatibility
- **Pallet system**: VERO-S compatible, Erowa compatible, System 3R compatible
- **Fixturing**: Standard zero-point clamping interfaces
- **Tooling**: Independent of tooling system - handles palletized workpieces

## Vendor Information

### Primary Contact
- **Company**: Fastems
- **Representative**: North American Sales Team
- **Phone**: Contact through distributors
- **Email**: sales@fastems.com

### Alternative Suppliers
- **Hartwig Inc.**: Authorized distributor, Missouri-based
- **Selway Tool**: Pacific Northwest distributor
- **Direct**: Factory direct for large installations

## Evaluation Criteria

### Strengths
- Compact 16m² footprint for high-capacity storage
- Compatible with 90+ machine tool brands
- 16-week delivery time is competitive
- MMS software provides advanced scheduling and tracking
- Lights-out operation capability
- Modular expansion possible

### Weaknesses
- Pricing not publicly available (requires quote)
- European origin may affect service support
- Limited to 630mm maximum pallet size
- Requires integration engineering for cell optimization

### Alternatives Considered
- **VERO-S Tower Systems**: More limited capacity, potentially lower cost
- **Erowa LoadMaster**: Higher capacity but larger footprint
- **Custom Tower**: Lower integration, higher engineering risk
- **Rationale**: Fastems offers best balance of capacity, footprint, and integration support for lights-out operation

## Integration Requirements for Hyperion Cell

### Robot Interface (KUKA KR 210 R3100)
- Standard pick/drop positions programmed in MMS
- Safety interlocks via Profisafe
- Collision avoidance through coordinated motion
- Gripper interface for various pallet types

### Machine Tool Interface (DN Solutions DVF 6500)
- Automatic pallet exchange coordination
- Workpiece present/absent signals
- Cycle complete notifications
- Error handling and recovery procedures

### Cell Control System (Siemens S7-1500)
- OPC-UA server for real-time status
- Production scheduling interface
- Alarm and diagnostic reporting
- Safety system integration

### Safety Integration
- Emergency stop circuits tied to cell E-stop
- Light curtain integration for access control
- Robot collision detection coordination
- Lockout/tagout procedures for maintenance