# Eylen Corporation (Configurations Da Vinci 1.0 Aio)

 ![](https://github.com/Eylen-Corporation/Da-Vinci-AIO-Configurations/blob/6c4ff30f4fdb1d9dd75bea045f1c44bfc464134c/eylen.jpg?raw=true) ![](https://github.com/Eylen-Corporation/Da-Vinci-AIO-Configurations/blob/6c4ff30f4fdb1d9dd75bea045f1c44bfc464134c/eylen.jpg?raw=true) ![](https://github.com/Eylen-Corporation/Da-Vinci-AIO-Configurations/blob/6c4ff30f4fdb1d9dd75bea045f1c44bfc464134c/eylen.jpg?raw=true) ![](https://github.com/Eylen-Corporation/Da-Vinci-AIO-Configurations/blob/6c4ff30f4fdb1d9dd75bea045f1c44bfc464134c/eylen.jpg?raw=true)


This page is intended for individuals with a 3D printer **"Da Vinci 1.0 AIO"** modified with the [Repetier-Firmware-0.92.10](https://github.com/luc-github/Repetier-Firmware-0.92/tree/devt).

## CAUTION: I will not be responsible for what you do with your printer. You may damage your machine and void the warranty, for the Da Vinci 1.0 AIO there is no return to the Official Firmware and the 3D Scanner is not supported at the moment (29/07 / 16). So be aware and aware of the risks you take.

![](https://images-na.ssl-images-amazon.com/images/I/61yCScw0nyL._SL1000_.jpg)

# Why did I change firmware?

After several tests with the official software I have forged a first-hand experience (secure and autonomous printer), but I wanted to increase the control of my machine to get a very detailed setting. I also noticed that my extruder, at the end of printing, had a big problem to return to its original position. Indeed it forced in Y- and did not move in X, so risk of breakage. This firmware corrected the problem with some Gcode changes at the end of the program.

The advantages of [Repetier-Firmware-0.92.10](https://github.com/luc-github/Repetier-Firmware-0.92/tree/devt): 
- A complete control of my machine (Speeds, Temperatures, layer heights, control software, etc ...).
- Filament chosen by me.
- A Gcode program that I configured to make my printings easier (Start) and (Fine).
- And I probably forget it.

To change Firmware I followed this very complete tutorial. "[Repetier-Firmware-0.92.10](https://github.com/luc-github/Repetier-Firmware-0.92/tree/devt)".

# Useful Files

[Modified EEPROM](https://github.com/Eylen-Corporation/Da-Vinci-AIO-Configurations/blob/6c4ff30f4fdb1d9dd75bea045f1c44bfc464134c/EEPRom-Eylen-CorporationV2.0.epr) "Improved probing points for Autoleveling (G32 S2)".

![](https://raw.githubusercontent.com/Eylen-Corporation/Da-Vinci-AIO-Configurations/6c4ff30f4fdb1d9dd75bea045f1c44bfc464134c/Tuto1.png)
![](https://raw.githubusercontent.com/Eylen-Corporation/Da-Vinci-AIO-Configurations/6c4ff30f4fdb1d9dd75bea045f1c44bfc464134c/Tuto2.png)

# Gcode for Slicer

## Start
```gcode
;*****************************************************************

;**                     EYLEN CORPORATION                       **

;**            3D Print Program by Eylen Corporation            **

;*****************************************************************

G28; Initial Position of XYZ Axes

G1 Z5 F5000; Clearance of the nozzle at 5mm from the board

G28; Initial Position of XYZ Axes

G32 S2; 3-point probing for Z0 tray update (automatic compensation for unevenness)

G1 F5000 X-3

G1 F5000 Y100

G1 F5000 X5
```

## End
```gcode
M104 S0; Disabling temperatures

M106 S255; Fan cooling

G90

G0 X-10

G0 Y100

M109 S40; Waiting for cooling

G28 X0; Initial position of the X axis

G28 Y0; Initial position of the Y axis

M106 S0; Fan disabled

M84; Deactivation of motors and end of program
```

# Details

For the beginning of the program one of the discoveries that really changed my way of adjusting the printer is the G32 S2.
Here is what the [Repetier Wiki](https://www.repetier.com/documentation/repetier-firmware/z-probing/)

## G32: Z probing and calculation of flatness

### Use

    - G32 
    - G32 Snnn

### Settings

    Snnn (Storage of the transformed matrix after probing) 


### Examples

    G32 
    G32 S2 (S2 => Storage of all data to EEPROM)


Scale the heated platen at 3 or more preset points (see M557) and update the die transformation for hot plate compensation.

RepRapFirmware executes the macro file `bed.g`

## Notes

    - S0 Default value. The calculated matrix is updated in the RAM but is not stored in the EEPROM.
     The height Z is not calculated.

    - S1 The calculated matrix is updated in the RAM but is not stored in the EEPROM. The printer
     immediately moves to its maximum Z position (Sensor Z max required), and calculates the new Z height.
     You must first use G28 to put the machine in the initial position before using
     G32 Snnn for it to work properly, or the Z height will be invalid.

    - S2 similar to S1, except the transformation of the matrix and the height Z are stored in the EEPROM.

    - S3 The transformed matrix is stored in the EEPROM. The height Z is not calculated.

## Slic3r Configuration for PLA ESUN Silver Gray

### Configuration files: [Slic3r_config_bundle.ini](https://github.com/Eylen-Corporation/Da-Vinci-AIO-Configurations/blob/6c4ff30f4fdb1d9dd75bea045f1c44bfc464134c/config.ini)

![](https://raw.githubusercontent.com/Eylen-Corporation/Da-Vinci-AIO-Configurations/6c4ff30f4fdb1d9dd75bea045f1c44bfc464134c/Tuto3.png)


