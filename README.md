I reflashed all my CR-10s (3 CR-10S and 1 CR-10 (with sanguino 1284p))

Afterwards I got the following error
E1 THERMAL RUNAWAY
PRINTER HALTED
Please reset

In order to autotune the PID for each printer I connected to the printer via serial port and did the following

```
M303 E0 S220 C10
```

This started the PID autotune for the main extruder at the temperature 220C and ran the test over 10 iterations

After the test was done it printed out something like the following:

```
...
...
READ:  T:222.14 /0.00 B:0.00 /0.00 @:17 B@:0
READ:  T:220.71 /0.00 B:0.00 /0.00 @:17 B@:0
READ:  bias: 144 d: 110 min: 215.78 max: 223.57 Ku: 35.96 Tu: 27.53
READ:  Classic PID 
READ:  Kp: 21.57 Ki: 1.57 Kd: 74.23
READ: PID Autotune finished! Put the last Kp, Ki and Kd constants from below into Configuration.h
READ: #define DEFAULT_Kp 21.57
READ: #define DEFAULT_Ki 1.57
READ: #define DEFAULT_Kd 74.23
READ: ok
```

I then took the values from this and wrote
```
M301 P21.57 I1.57 D74.23
M500
```
M301 updated the settings
M500 updated the EEPROM so that these settings would be persisted.

More info on gcode commands here: https://marlinfw.org/docs/gcode/M303.html

