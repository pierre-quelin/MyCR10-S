# My personal touch, "The JackyTouch"

## Expected performances

Number of probes : 50

```
G28
M48 P50 V2
...
Mean: -0.004780 Min: -0.008 Max: -0.002 Range: 0.006
Standard Deviation: 0.001467
ok P15 B0
```

## Hardware

- 1 x Optocoupler module LM393 comparator Slot-Type 3.3V-5V for arduino based
- 2 x N52 super strong cylinder magnets 6mm x 3mm rare earth neodymium Mmgnets
- 1 x Steel rode d=4 l=50
- 1 x A mouse wire

## Assembly

## Firmware (Marlin)

Configure a TOUCHMI probe that uses the same operating principle.

[MyCR10-S_2.1 Branch on github](https://github.com/pierre-quelin/Marlin)

## Sensor wiring

### Original Creality board pinout

[CR10S-V2.1](https://github.com/pierre-quelin/cr10s/blob/master/JackyTouch/CR10S-V2.1.png)

### MKS-Robin-E3D pinout

[MKS-Robin-E3D-V1.0](https://github.com/pierre-quelin/cr10s/blob/master/JackyTouch/MKS-Robin-E3D-V1.0.jpg)

### LM393 pinout

[LM393](https://github.com/pierre-quelin/cr10s/blob/master/JackyTouch/LM393.pinout.jpg)
   
- VCC: Module power supply.
- GND: Ground.
- D0: Digital signal of the output pulses.
- A0: Analog signal of the output pulses (not used).

### Wiring

- Remove the old Z limit switch connector from the board.

- Connect the new sensor to the board. **Be careful !!!**

Connect the VCC wire first, then the GND wire.

If the power indicator led is off, you made a mistake. Reconnect the GND wire correctly.

To avoid a short circuit, connect the D0 wire only if the sensor is powered correctly.

## Calibrating Z-offset (Pronterface)

- Enable the probe (Press the button to lower the probe)
- Launch Pronterface
- Do Homing and read current Z-offset

```
...
echo:Z-Probe Offset (mm):
echo:  M851 Z-6.43
...
```

- Reset current offset ([help](https://marlinfw.org/docs/gcode/M851.html))

```
M851 Z0
```

- Store offset to EEPROM ([help](https://marlinfw.org/docs/gcode/M500.html))

```
M500
```

- Set EEPROM as active parameters ([help](https://marlinfw.org/docs/gcode/M501.html))

```
M501
```

- Display current active settings ([help](https://marlinfw.org/docs/gcode/M503.html))

```
M503
```

- Home Z axis only ([help](https://marlinfw.org/docs/gcode/G028.html))

```
G28 Z0
```

- Move nozzle to 0.0 Z offset ([help](https://marlinfw.org/docs/gcode/G000-G001.html))

```
G1 F60 Z0
```

- Switches off soft endstops ([help](https://marlinfw.org/docs/gcode/M211.html))

```
M211 S0
```

- Manually slide a pice of paper (0.1mm) under the nozzle and slowly move the nozzle downwoards until the paper can barely move due to the friction of the nozzle and the bed.

- Look at the Z-offset value at the printer screen and take a note about it

```
-6.3 mm
```

- Set Z-offset (add the paper thickness to the previous value) 

```
M851 Z-6.4
```

- Switch on soft endstops

```
M211 S1
```

- Store current settings to EEPROM

```
M500
```

- Set EEPROM as active parameters

```
M501
```

- Display current active settings

```
M503
```

- Do homing
- Move to 0 and check again with the paper

```
G1 F60 Z0
```

## gcode updates (Cura)

Machine settings -> Start G-code

```
G28 ; Home (Enable device)
G29 ; Auto bed leveling
G1 Z0.2 ; Down to 0.2mm (Disable device)
```

[mygithub]: <https://github.com/pierre-quelin/Marlin/tree/MyCR10-S_2.0.x>
