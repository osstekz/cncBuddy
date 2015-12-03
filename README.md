
###CNC 3 Axis software suite
* CncBuddyUI: Windows G-Code parser/interpreting master control program. 
  - Fully configurable 4 stepper motor (X,Y,Z,A)
  - Netduino+2 network(IP/Port) discovery
  - Workspace / Tool Offsets
  - InchesPerMinute Calibration
  - 3D Path Viewer
  - Jogging devices(Analog NESController,Analog Joystick,Keyboard)
  - Audible speech command responses
  - Binary file transfers
  - Color coded response messages (Red=Errors, Yellow=Warnings, Green=Info)

* cncBuddyCAM: Netduino+2 controller
  - GPIO control up to 4 stepper motors
  - UDP broadcast IPAddress/Port for discovery
  - G-Code processor
  - SDCard job caching
  - X,Y,Z axis JogMode
    - Analog devices: NESControl or Joystick 
    - PC keyboard 

![CncBuddyUI](/images/cncBuddyUI.png)

If you would like to see additional functionality, feel free to post an enhancement/change request.

-----------------------
####Configuration
* General
  - Netduino+2 IP address & Port (default Port:80)
  - Feed Rates
  - G-Code Header/Footer files
* Axis Settings: X,Y,Z
  - Steps per Turn
  - Turns per Inch
  - Inverted signals
  - Slave A axis
* Netduino+2: X,Y,Z, A (slaved)
  - GPIO pins: Step / Direction / Limit Switch
* 3D Path Viewer
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
- \bin\CncBuddyUI.exe is a Windows ready-to-run program on the .Net4.0 framework
 
-----------------------
####Getting started
- cncBuddyCAM:
  - Blue LED 5 rapid flashes means waiting for a network connection to CncBuddyUI.
    - The ONBOARD_SW1 button (typically used for rebooting) is re-configured for use as an "ESTOP" button (Safety1st).
    - At start up, software always defaults to an "ESTOP" condition (Safety1st)!
- CncBuddyUI:
  - Set all operating parameters in menu "Machine->Configuration Settings". Clicking the "Save" button:
    1. settings are sent to cncBuddyCAM for re-configuration
    2. "RPTSTATUS" response is always returned for verification
    3. settings are stored locally on your hard drive to be used during next startup.
  - At start up, we always produce an "ESTOP" condition! Any/All errors must be resolved before you can Reset/Clear an "ESTOP" (Safety1st).
  - Audible beeps are used during "ESTOP" conditions and error detection.
  - Command line options (prefixed by "-","--", or "/"):
~~~~
CncBuddyUI.exe [/help|/?] [/reset] [/discover] [/install:[axisA=X|Y][,port=9999][,limitsw=true|false]] 

/help|/?    Show this help/usage information
/reset      Create new default software configuration
/discover   Listen for cncBuddyCAM broadcasting IPAddress & Port (timeout 30 secs)
/install    Install hardware specific settings on Netduino+2 SDCard. Overrides software configuration values
   port     Network port number (default=80)
   axisA    Slave axisA motor signals to X or Y axis
   limitsw  Limit switches are installed and active on X,Y,Z axis

Example: CncBuddyUI.exe /install:"axisA=X,port=4512,limitsw=true"
~~~~

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
I've built a couple CNC machines which rely heavily on this project for their day to day use.
I'm dedicated to growing it's base whether applying bug fixes, performance tuning, or adding features.

Feel free to file issues and change requests.

Development and testing use the .NET Micro Framework SDK v4.2.2

If you find this software useful, want to say thanks and encourage development, please consider a donation.
[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=ZMMCYGL8QD8BW&lc=US&item_name=cncBuddy%20XProject&item_number=cncBuddy&currency_code=USD&bn=PP%2dDonationsBF%3abtn_donateCC_LG%2egif%3aNonHosted)
-----------------------
####Requested Features
    - AndroidUI Controller