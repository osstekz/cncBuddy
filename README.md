
###CNC 3 axis software suite
* cncBuddyUI: Windows G-Code parser/interpreting master control program. 
    - Fully configurable X,Y,Z,A Axis
    - Workspace / Tool Offsets
    - IPM Calibration
    - Jogging devices(Analog NESController,Analog Joystick,Keyboard)

* cncBuddyCAM: NetduinoPlus2 4 stepper driver and G-Code processor.

![cncBuddyUI](/images/cncBuddyUI.png)

If you would like to see additional functionality, feel free to post an enhancement/change request.

-----------------------
##Configuration
* General
    - Netduino IP address (default Port:80)
    - Feed Rates
    - G-Code Header/Footer files
* Axis Settings: X,Y,Z
    - Steps per Turn
    - Turns per Inch
    - Inverted signals
    - Slave A axis
* Netduino: X,Y,Z, A (slaved)
    - GPIO pins Step / Direction / Limit Switch
* 2D Simulator
    - Enable / Speed / Zoom Cut Diameter

-----------------------
##cncBuddyUI startup options 
 --resetcfg			Create new default configuration
-----------------------
##HOW TO RUN
 
-----------------------
##DEVELOPMENT
Development and testing use the .NET Micro Framework SDK v4.2.2

Contributions to this are absolutely welcome! Feel free to file issues.
 
-----------------------
##EXTENDED FEATURES