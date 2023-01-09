# My Creality CR-10S improvements

## The Board

[MKS-Robin-E3D-V1.0](https://github.com/makerbase-mks/MKS-Robin-E3-E3D)

## My personal touch, "The JackyTouch"

<img src="https://github.com/pierre-quelin/cr10s/blob/master/JackyTouch.png" width="300">

[README](JackyTouch/README.md)

## Another extruder fan

<img src="https://github.com/pierre-quelin/cr10s/blob/master/ExtruderFan.png" width="300">

[README](ExtruderFan/README.md)

## Power Loss Recovery

<img src="https://github.com/pierre-quelin/cr10s/blob/master/MKS_UPS12V_V1.0.png" width="300">

[README](MKS_UPS12V/README.md)

## My customised firmware (many thanks to [Marlin](https://marlinfw.org/) for their great job)

[MyCR10-S_2.1 Branch on github](https://github.com/pierre-quelin/Marlin)

## Unified bed leveling setup

[Marlin UBL Startup Guide](https://marlinfw.org/docs/features/unified_bed_leveling.html)

Setup and initial probing commands (Pronterface)

- Reset settings to configuration defaults... ([help](https://marlinfw.org/docs/gcode/M502.html))

```
M502
```
- ...and Save to EEPROM. Use this on a new install. ([help](https://marlinfw.org/docs/gcode/M500.html))

```
M500
```

- Read back in the saved EEPROM. ([help](https://marlinfw.org/docs/gcode/M501.html))

```
M501
```
- Wait for Bed Temperature 62°C. Helps accuracy ([help](https://marlinfw.org/docs/gcode/M190.html))

```
M190 S62
```

- Home XYZ. ([help](https://marlinfw.org/docs/gcode/G028.html))

```
G28
```

- Do automated probing of the bed. ([help](https://marlinfw.org/docs/gcode/G029-ubl.html))

```
G29 P1
```

- Do a ‘smart fill’ of missing mesh points.

```
G29 P3 T
```

- View the Z compensation values.

```
G29 T
```

- Save UBL mesh points to EEPROM slot 0.

```
G29 S0
```

- Set Fade Height for correction at 10.0 mm.

```
G29 F 10.0
```

- Activate the UBL System.

```
G29 A
```

- Save current setup. WARNING: UBL will be active at power up, before any G28.

```
M500
```


Do a test...

- Load the mesh stored in slot 0 (from G29 S0)

```
G29 L0
```

- Home XYZ.

```
G28
```

- Probe 3 points to find the plane of the bed

```
G29 J
```

- Print a pattern to test mesh accuracy.Prime Length of 10mm before print ([help](https://marlinfw.org/docs/gcode/G26.html))

```
G26 P10
```

## Slicer G-code

Start G-code

    G28 ;Home
    
    ; Unified Bed Leveling
    G29 A ; Activate the UBL System.
    G29 L0 ; Load UBL 0
    G29 J ; Probe 3 points to find the plane of the bed
    G29 F10.0 ; Fade to 10mm
    
    ;G1 Z0.2 ; Disable the touch sensor cf. Marlin TOUCH MI
    G1 Z15.0 F6000 ; Move the platform down 15mm
    G92 E0 ; Set extruder position to 0
    G1 F200 E4 ; Linear move, feedrate 200mm/min, extrusion length 4mm
    G92 E0 ; Set extruder position to 0

End G-Code

    G91 ;Relative positioning
    G1 E-2 F2700 ;Retract a bit
    G1 E-2 Z0.2 F2400 ;Retract and raise Z
    G1 X5 Y5 F3000 ;Wipe out
    G1 Z10 ;Raise Z more
    G90 ;Absolute positioning
    
    G1 X0 Y{machine_depth} ;Present print
    M106 S0 ;Turn-off fan
    M104 S0 ;Turn-off hotend
    M140 S0 ;Turn-off bed
    
    M84 X Y E ;Disable all steppers but Z
