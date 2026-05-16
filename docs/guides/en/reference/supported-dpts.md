# Supported Datapoint Types (DPTs)

SharKNX supports KNX Datapoint Types in two contexts:

- **Decoding** — values decoded and displayed when receiving telegrams in the Monitor. Applies to all DPTs in this document.
- **Sending** — DPTs available for selection when composing a command. A subset of the decodable DPTs. Marked with ✅ in the table below.

If a telegram arrives for a group address whose DPT is unknown or not yet supported, the raw hex payload is shown instead of a decoded value.

---

## Overview

| DPT | Name | Size | Send |
|-----|------|------|------|
| **1** | 1-bit Boolean | 1 bit | ✅ |
| **2** | 1-bit Controlled | 2 bits | ✅ |
| **3** | 3-bit Controlled (Step) | 4 bits | ✅ |
| **4** | Character | 1 byte | ✅ |
| **5** | 8-bit Unsigned Value | 1 byte | ✅ |
| **6** | 8-bit Signed Value | 1 byte | ✅ |
| **7** | 2-byte Unsigned Value | 2 bytes | ✅ |
| **8** | 2-byte Signed Value | 2 bytes | ✅ |
| **9** | 2-byte Float | 2 bytes | ✅ |
| **10** | Time of Day | 3 bytes | ✅ |
| **11** | Date | 3 bytes | ✅ |
| **12** | 4-byte Unsigned Value | 4 bytes | ✅ |
| **13** | 4-byte Signed Value | 4 bytes | ✅ |
| **14** | 4-byte IEEE 754 Float | 4 bytes | ✅ |
| **15** | Entrance Access | 4 bytes | — |
| **16** | 14-Character String | 14 bytes | ✅ |
| **17** | Scene Number | 1 byte | ✅ |
| **18** | Scene Control | 1 byte | ✅ |
| **19** | Date & Time | 8 bytes | ✅ |
| **20** | 1-byte Enum | 1 byte | ✅ |
| **21** | 8-bit Status / Flags | 1 byte | ✅ |
| **22** | 16-bit Status / Flags | 2 bytes | ✅ |
| **23** | 2-bit Set | 1 byte | — |
| **24** | Variable String (ISO 8859-1) | variable | — |
| **25** | Double Nibble | 1 byte | — |
| **26** | Scene Info | 1 byte | — |
| **27** | 32-bit Combined Info | 4 bytes | — |
| **28** | Variable String (UTF-8) | variable | ✅ |
| **29** | 8-byte Signed Value | 8 bytes | ✅ |
| **30** | Channel Activation (24 ch) | 3 bytes | — |
| **206** | Time Delay + HVAC Mode | 3 bytes | — |
| **217** | Version | 2 bytes | — |
| **219** | Alarm Info | 6 bytes | — |
| **222** | Temperature Setpoints (×3) | 6 bytes | — |
| **225** | Scaling Step Time | 4 bytes | — |
| **229** | Metering Value | 6 bytes | — |
| **232** | RGB Colour | 3 bytes | ✅ |
| **234** | Language Code | 2 bytes | — |
| **235** | Tariff Active Energy | 6 bytes | — |
| **240** | Combined Position (blinds) | 3 bytes | — |
| **241** | Shutter Actuator Status | 4 bytes | — |
| **242** | CIE xyY Colour | 6 bytes | ✅ |
| **243** | xyY Colour Transition | 8 bytes | — |
| **249** | Brightness & CCT Transition | 6 bytes | ✅ |
| **250** | Brightness & CCT Control (relative) | 3 bytes | ✅ |
| **251** | RGBW Colour | 6 bytes | ✅ |
| **252** | Relative Control RGBW | 5 bytes | ✅ |
| **253** | Relative Control xyY | 4 bytes | — |
| **254** | Relative Control RGB | 3 bytes | ✅ |
| **275** | Four 2-byte Floats | 8 bytes | — |

---

## Subtypes

The following sections list the subtypes selectable when **sending** commands, grouped by main type. DPTs with a single subtype or no send support are omitted.

### DPT 1 — 1-bit Boolean

| Subtype | Description |
|---------|-------------|
| 1.001 | Switch (Off / On) |
| 1.002 | Boolean |
| 1.003 | Enable |
| 1.004 | Ramp |
| 1.005 | Alarm |
| 1.006 | Binary Value |
| 1.007 | Step |
| 1.008 | Up / Down |
| 1.009 | Open / Close |
| 1.010 | Start / Stop |
| 1.011 | State |
| 1.012 | Invert |
| 1.013 | Dim Send Style |
| 1.014 | Input Source |
| 1.015 | Reset |
| 1.016 | Acknowledge |
| 1.017 | Trigger |
| 1.018 | Occupancy |
| 1.019 | Window / Door |
| 1.021 | Logical Function |
| 1.022 | Scene A/B |
| 1.023 | Shutter / Blinds Mode |
| 1.100 | Cooling / Heating |

### DPT 2 — 1-bit Controlled

| Subtype | Description |
|---------|-------------|
| 2.001 | Switch Control |
| 2.002 | Boolean Control |
| 2.003 | Enable Control |
| 2.004 | Ramp Control |
| 2.005 | Alarm Control |
| 2.006 | Binary Value Control |
| 2.007 | Step Control |
| 2.008 | Direction Control 1 |
| 2.009 | Direction Control 2 |
| 2.010 | Start Control |
| 2.011 | State Control |
| 2.012 | Invert Control |

### DPT 3 — 3-bit Controlled

| Subtype | Description |
|---------|-------------|
| 3.007 | Dimming Control |
| 3.008 | Blind Control |

### DPT 4 — Character

| Subtype | Description |
|---------|-------------|
| 4.001 | Character (ASCII) |
| 4.002 | Character (ISO 8859-1) |

### DPT 5 — 8-bit Unsigned

| Subtype | Description | Range | Unit |
|---------|-------------|-------|------|
| 5.001 | Scaling / Percentage | 0–100 | % |
| 5.003 | Angle | 0–360 | ° |
| 5.004 | Percentage | 0–255 | % |
| 5.005 | Ratio | 0–255 | — |
| 5.006 | Tariff | 0–255 | — |
| 5.010 | Counter Pulses | 0–255 | — |

### DPT 6 — 8-bit Signed

| Subtype | Description | Range | Unit |
|---------|-------------|-------|------|
| 6.001 | Percentage | −128–127 | % |
| 6.010 | Counter Pulses | −128–127 | — |

### DPT 7 — 2-byte Unsigned

| Subtype | Description | Unit |
|---------|-------------|------|
| 7.001 | Pulses | — |
| 7.002 | Time Period | ms |
| 7.003 | Time Period | 10 ms |
| 7.004 | Time Period | 100 ms |
| 7.005 | Time Period | s |
| 7.006 | Time Period | min |
| 7.007 | Time Period | h |
| 7.011 | Length | mm |
| 7.012 | Current | mA |
| 7.013 | Brightness | lux |
| 7.600 | Colour Temperature | K |

### DPT 8 — 2-byte Signed

| Subtype | Description | Unit |
|---------|-------------|------|
| 8.001 | Pulses Difference | — |
| 8.002 | Time Lag | ms |
| 8.003 | Time Lag | 10 ms |
| 8.004 | Time Lag | 100 ms |
| 8.005 | Time Lag | s |
| 8.006 | Time Lag | min |
| 8.007 | Time Lag | h |
| 8.010 | Percentage Difference | % |
| 8.011 | Rotation Angle | ° |

### DPT 9 — 2-byte Float

| Subtype | Description | Unit |
|---------|-------------|------|
| 9.001 | Temperature | °C |
| 9.002 | Temperature Difference | K |
| 9.003 | Temperature Change | K/h |
| 9.004 | Illuminance | lux |
| 9.005 | Wind Speed | m/s |
| 9.006 | Pressure | Pa |
| 9.007 | Humidity | % |
| 9.008 | Air Quality (CO₂) | ppm |
| 9.009 | Air Flow | m³/h |
| 9.010 | Time | s |
| 9.011 | Time | ms |
| 9.020 | Voltage | mV |
| 9.021 | Current | mA |
| 9.022 | Power Density | W/m² |
| 9.023 | Kelvin per Percent | K/% |
| 9.024 | Power | kW |
| 9.025 | Volume Flow | l/h |
| 9.026 | Rain Amount | l/m² |
| 9.027 | Temperature | °F |
| 9.028 | Wind Speed | km/h |

### DPT 13 — 4-byte Signed

| Subtype | Description | Unit |
|---------|-------------|------|
| 13.001 | Counter Pulses | — |
| 13.002 | Flow Rate | m³/h |
| 13.010 | Active Energy | Wh |
| 13.011 | Apparent Energy | VAh |
| 13.012 | Reactive Energy | VARh |
| 13.013 | Active Energy | kWh |
| 13.014 | Apparent Energy | kVAh |
| 13.015 | Reactive Energy | kVARh |
| 13.100 | Time Lag | s |

### DPT 14 — 4-byte IEEE Float (selected subtypes)

Only a subset of DPT 14's 80 subtypes are available in the send UI. All subtypes are decoded in the monitor.

| Subtype | Description | Unit |
|---------|-------------|------|
| 14.007 | Angle | ° |
| 14.019 | Electric Current | A |
| 14.027 | Electric Potential | V |
| 14.033 | Frequency | Hz |
| 14.056 | Power | W |
| 14.065 | Speed | m/s |
| 14.068 | Temperature | °C |
| 14.069 | Temperature Absolute | K |
| 14.070 | Temperature Difference | K |

### DPT 16 — 14-Character String

| Subtype | Description |
|---------|-------------|
| 16.000 | ASCII |
| 16.001 | ISO 8859-1 |

### DPT 20 — 1-byte Enum

| Subtype | Description |
|---------|-------------|
| 20.002 | Building Mode |
| 20.003 | Occupied Mode |
| 20.004 | Priority |
| 20.005 | Light Application Mode |
| 20.006 | Light Application Area |
| 20.007 | Alarm Class Type |
| 20.008 | PSU Mode |
| 20.013 | Time Delay |
| 20.014 | Wind Force (Beaufort) |
| 20.100 | Fuel Type |
| 20.101 | Burner Type |
| 20.102 | HVAC Mode |
| 20.103 | DHW Mode |
| 20.104 | Load Priority |
| 20.105 | HVAC Control Mode |
| 20.106 | HVAC Emergency Mode |
| 20.107 | Changeover Mode |
| 20.108 | Valve Mode |
| 20.109 | Damper Mode |
| 20.110 | Heater Mode |
| 20.111 | Fan Mode |
| 20.112 | Master / Slave Mode |
| 20.113 | Status Room Setpoint |

> **Note:** Display of enum labels for most DPT 20 subtypes falls back to the raw mode number. Named labels (e.g. "Comfort", "Standby") are shown for 20.102 (HVAC Mode) and a few others.

### DPT 21 — 8-bit Status Flags

| Subtype | Description |
|---------|-------------|
| 21.001 | General Status |
| 21.002 | Device Control |
| 21.100 | Forcing Signal |
| 21.102 | Room Heating Controller Status |
| 21.103 | Solar DHW Controller Status |
| 21.105 | Room Cooling Controller Status |
| 21.106 | Ventilation Controller Status |

### DPT 22 — 16-bit Status Flags

| Subtype | Description |
|---------|-------------|
| 22.100 | DHW Controller Status |
| 22.101 | RHCC Status |

### DPT 29 — 8-byte Signed (64-bit Energy)

| Subtype | Description | Unit |
|---------|-------------|------|
| 29.010 | Active Energy | Wh |
| 29.011 | Apparent Energy | VAh |
| 29.012 | Reactive Energy | VARh |

### DPT 232 / 242 / 249 / 250 / 251 / 252 / 254 — Colour & Lighting

| DPT | Description | Size |
|-----|-------------|------|
| 232.600 | RGB Colour | 3 bytes |
| 242.600 | CIE xyY Colour | 6 bytes |
| 249.600 | Brightness & Colour Temperature Transition | 6 bytes |
| 250.600 | Brightness & Colour Temperature Control (relative) | 3 bytes |
| 251.600 | RGBW Colour | 6 bytes |
| 252.600 | Relative Control RGBW | 5 bytes |
| 254.600 | Relative Control RGB | 3 bytes |

---

## Decode-only DPTs

The following DPTs are decoded in the monitor when the ETS project provides the DPT assignment, but are not available for manual command composition in the send UI.

| DPT | Description |
|-----|-------------|
| 15.000 | Entrance Access (access code) |
| 23.x | 2-bit Action Set (on/off, up/down, alarm) |
| 24.x | Variable-length String (ISO 8859-1) |
| 25.x | Double Nibble |
| 26.001 | Scene Info |
| 27.001 | Bit-combined Info On/Off |
| 30.1010 | Channel Activation (24 channels) |
| 206.x | Time Delay + HVAC/DHW/Occupancy/Building Mode |
| 217.001 | DPT Version |
| 219.001 | Alarm Info |
| 222.x | Room Temperature Setpoints (×3) |
| 225.x | Scaling Step Time |
| 229.001 | Metering Value |
| 234.001 | Language Code (ISO 639-1) |
| 235.001 | Tariff Active Energy |
| 240.800 | Combined Position (blinds/shutter) |
| 241.800 | Shutter Actuator Status |
| 243.x | xyY Colour Transition |
| 253.x | Relative Control xyY |
| 275.x | Four 2-byte Floats |
