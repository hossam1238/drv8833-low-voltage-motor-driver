# Design notes — Low-Voltage DC Motor Driver Board

## Assumptions

The datasheet specifies 1.5 A RMS/DC per bridge under stated conditions, but this design does not claim a safe continuous current. Final current must be derated from package, copper area, ambient temperature, motor duty cycle and measured thermal rise.

Component selection uses manufacturer datasheets linked in the root README. MPN availability should be rechecked at purchasing time. No continuous-current guarantee is made without a thermal calculation and measurement.

## Review gates

- Confirm every symbol pin number against the manufacturer datasheet.
- Confirm package land patterns against the latest recommended land pattern.
- Confirm creepage, clearance, copper widths and connector ratings.
- Run KiCad ERC/DRC after assigning project-specific rules.
- Export fresh Gerbers from the reviewed KiCad PCB rather than relying on the preliminary files.
