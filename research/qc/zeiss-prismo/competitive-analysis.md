# CMM Competitive Analysis for Hyperion Lights-Out Cell

## Executive Summary

Analysis of ZEISS PRISMO vs current Hexagon Global Classic selection for automated quality control in the Hyperion lights-out manufacturing cell. Focus on 200×200×150mm part envelope with robot loading automation.

## Detailed Comparison

### ZEISS PRISMO Navigator vs Hexagon Global Classic 7.10.7

| Criteria | ZEISS PRISMO | Hexagon Global Classic | Winner |
|----------|--------------|----------------------|--------|
| **Measuring Volume** | 900×1000×600mm | 700×1000×700mm | ZEISS |
| **Accuracy** | 0.9 + L/350 µm | 2.2 + 3L/1000 µm | ZEISS |
| **Scanning Speed** | 300 mm/s | ~50 mm/s | ZEISS |
| **Automation** | MultiLoad (16 pallets) | TEMPO system | ZEISS |
| **Software** | CALYPSO + automation | PC-DMIS | Tie |
| **Price** | $380-450k | $220k | Hexagon |
| **Total Ownership** | Higher (software modules) | Lower initial, higher annual | ZEISS |
| **Robot Integration** | Proven (Mini-SiPos) | Available (I/O Flow) | Tie |

### Alternative: Mitutoyo CRYSTA-Apex V

| Criteria | ZEISS PRISMO | Mitutoyo CRYSTA-Apex V | Winner |
|----------|--------------|----------------------|--------|
| **Measuring Volume** | 900×1000×600mm | 900×1000×600mm | Tie |
| **Accuracy** | 0.9 + L/350 µm | 1.7 + 3L/1000 µm | ZEISS |
| **Automation** | MultiLoad system | Limited options | ZEISS |
| **Software Costs** | Modular licensing | One-time purchase | Mitutoyo |
| **Scanning Performance** | Industry leading | Good | ZEISS |
| **Price** | $380-450k | $280-350k | Mitutoyo |

## Key Findings

### ZEISS Advantages
1. **Superior Accuracy**: 0.9 + L/350 µm vs 2.2 + 3L/1000 µm (Hexagon)
2. **Scanning Performance**: 300 mm/s vs ~50 mm/s typical competitors
3. **Automation Maturity**: MultiLoad system proven for lights-out operation
4. **Computer-Aided Accuracy**: Dynamic error correction during high-speed scanning
5. **Energy Efficiency**: 64% power reduction with new C99m controller

### ZEISS Disadvantages
1. **Higher Initial Cost**: $160-230k premium over Hexagon
2. **Software Licensing**: Modular CALYPSO pricing vs bundled competitors
3. **Complexity**: Steeper learning curve for operators
4. **Service Costs**: Higher long-term maintenance costs reported

### Hexagon Advantages
1. **Lower Initial Cost**: $220k vs $380k+ for ZEISS
2. **Software Bundle**: PC-DMIS included (though annual renewals expensive)
3. **Market Share**: Larger installed base and service network
4. **Integration Experience**: Established automation partnerships

### Mitutoyo Advantages
1. **Software Economics**: One-time MCOSMOS purchase, no annual fees
2. **Ease of Use**: Simpler programming and operation
3. **Reliability**: Strong reputation for consistent performance
4. **Value Proposition**: Good accuracy at moderate price

## Automation Assessment

### ZEISS MultiLoad System
- **Capacity**: 16 pallet positions with 4 CMM simultaneous operation
- **Footprint**: Compact tower design
- **Integration**: OPC-UA, FACS job management, robot communication protocols
- **Proven**: Deployed in multiple lights-out installations

### Hexagon TEMPO/I/O Flow
- **Capacity**: Variable pallet configurations
- **Integration**: Available but less mature than ZEISS
- **Cost**: Additional system cost on top of CMM

### Robot Interface Requirements
All systems support industrial robot integration with:
- Safety interlocks (light curtains, area scanners)
- Part present sensors and fixture control
- Program selection and result feedback
- Statistical process control data output

## Recommendation

**Replace Hexagon Global Classic with ZEISS PRISMO Navigator** in BOM based on:

1. **Critical Accuracy Requirements**: ZEISS 0.9 + L/350 µm vs Hexagon 2.2 + 3L/1000 µm
2. **Lights-Out Operation**: Proven MultiLoad automation vs developmental TEMPO
3. **Scanning Performance**: 6x faster scanning enables higher throughput
4. **Future-Proofing**: Advanced automation features support cell expansion

**Cost Impact**: +$160-230k initial investment justified by:
- Superior measurement capability for precision parts
- Proven automation reducing operator intervention
- Faster cycle times enabling higher cell throughput
- Better integration with KUKA robot systems

**Alternative Option**: Mitutoyo CRYSTA-Apex V for cost-conscious implementation
- Good accuracy and reliability
- Lower total cost of ownership
- Limited automation capabilities require manual oversight

## Implementation Notes

### Integration with KUKA KR 210 R3100
- ZEISS Mini-SiPos safety protocol compatible with KUKA SafetyBus
- OPC-UA communication standard for both systems
- Proven integration examples in automotive applications

### Software Automation
- CALYPSO Dynamic Planning for adaptive measurement strategies
- FACS job management for production coordination
- Integration with Siemens S7-1500 PLC via OPC-UA

### Training Requirements
- 2-week CALYPSO programming course for operators
- 1-week automation integration training
- Ongoing support through ZEISS service network