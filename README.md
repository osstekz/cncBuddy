
###CNC 3 Axis software suite
* cncBuddyUI: Windows G-Code parser/interpreting master control program. 
  - Fully configurable X,Y,Z,A Axis
  - Workspace / Tool Offsets
  - InchesPerMinute Calibration
  - Jogging devices(Analog NESController,Analog Joystick,Keyboard)
  - Audible speech command responses
  - Color coded response messages (Red=Errors, Yellow=Warnings, Green=Info)

* cncBuddyCAM: Netduino+2 controller
  - GPIO control up to 4 stepper motors
  - G-Code processor
  - SDCard job caching
  - X,Y,Z axis JogMode
    - Analog devices: NESControl or Joystick 
    - PC keyboard 

![cncBuddyUI](/images/cncBuddyUI.png)

If you would like to see additional functionality, feel free to post an enhancement/change request.

-----------------------
####Configuration
* General
  - Netduino+2 IP address (default Port:80)
  - Feed Rates
  - G-Code Header/Footer files
* Axis Settings: X,Y,Z
  - Steps per Turn
  - Turns per Inch
  - Inverted signals
  - Slave A axis
* Netduino+2: X,Y,Z, A (slaved)
  - GPIO pins: Step / Direction / Limit Switch
* 2D Simulator
  - Enable / Speed / Zoom / Cut Diameter

-----------------------
####Installation
- Download the zip archive and unpack or git-clone the project. The \bin folder contains the application files.
- \bin\cncBuddyCAM.hex is a Netduino+2 image for .NET Micro Framework SDK v4.2.2.  You must run MFDeploy.exe to load the hex image onto your Netduino+2. Once the cncBuddyCAM.hex image is loaded...
  - Make sure the device is responding: 
    - Optional: You may have to restart TinyClr from the menu "Plug-In->Debug->Reboot CLR".
    - Select Device type = "USB" and name "NetduinoPlus2_Netduino".
    - Click "PING" button should display message "Pinging... TinyCLR".
  - Set your network configuration parameters "Target->Configuration->Network".
    - Optional: You may have to restart TinyClr from the menu "Plug-In->Debug->Reboot CLR".
- \bin\cncBuddyUI.exe is a Windows ready-to-run program on the .Net4.0 framework
 
-----------------------
####Getting started
- cncBuddyCAM:
  - Blue LED 5 rapid flashes means waiting for a network connection to cncBuddyUI.
    - The ONSWITCH1 (typically for rebooting) is redesigned for use as an "ESTOP" button (Safety1st).
    - At start up, software always defaults to an "ESTOP" condition (Safety1st)!
- cncBuddyUI:
  - Set all operating parameters in menu "Machine->Configuration Settings". Clicking the "Save" button:
    1. settings are sent to cncBuddyCAM for re-configuration
    2. "RPTSTATUS" response is always returned for verification
    3. settings are stored locally on your hard drive to be used during next startup.
  - At start up, we always produce an "ESTOP" condition! Any/All errors must be resolved before you can Reset/Clear an "ESTOP" (Safety1st).
  - Audible beeps are used during "ESTOP" conditions and error detection.
  - Command line options:
      '--resetcfg'			Create new default configuration

-----------------------
####ESTOP
ESTOP conditions are stored internally as Motion Interrupt Flags(MIC). The MIC value can be any combination:

	| ## |                         Description                           |
	| -- | ------------------------------------------------------------- |
	| 01 | PAUSE button                                                  |
	| 02 | ESTOP button                                                  |
	| 04 | OVERTRAVEL - limit switch detected                            |
	| 08 | CLIENTSOCKETNOTREADY - network connection not ready/available |
	| 16 | CONFIGERROR - configuration error                             |

-----------------------
####Development
I've built a couple of CNC machines, so I rely heavily on this project for their day to day use.
Whether applying bug fixes, performance tuning, or adding features, I'm dedicated to growing it's base.
Feel free to file issues and change requests.

Development and testing use the .NET Micro Framework SDK v4.2.2

Contributions always welcome!
 
-----------------------
####Requested Features
    - AndroidUI Controller