# JackyTouch - My personal touch

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

TODO

## Firmware updates (Marlin)
[MyCR10-S Branch on github][mygithub]

TODO

## Sensor wiring

* Pinout module

VCC: Module power supply.
GND: Ground.
D0: Digital signal of the output pulses.
A0: Analog signal of the output pulses (not used).

- Remove the old Z limit switch connector from the board.

- Connect the new sensor. **Be careful !!!**

Connect the VCC wire first, then the GND wire.
If the power indicator led is off, you made a mistake. Reconnect the GND wire correctly.
To avoid a short circuit, connect the D0 wire only if the sensor is powered correctly.

## Z-offset setting

TODO

## gcode updates (ex. Cura)

Machine settings -> Start G-code

```
G28 ; Home (Enable device)
G29 ; Auto bed leveling
G1 Z0.2 ; Down (Disable device)
G4 P1000 ; Wait 1s to cut the filament
```

[mygithub]: <https://github.com/pierre-quelin/Marlin/tree/MyCR10-S>