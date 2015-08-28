
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

Contributions always welcome!
 <form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top">
<input type="hidden" name="cmd" value="_s-xclick">
<input type="hidden" name="encrypted" value="-----BEGIN PKCS7-----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-----END PKCS7-----
">
<input type="image" src="https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!">
<img alt="" border="0" src="https://www.paypalobjects.com/en_US/i/scr/pixel.gif" width="1" height="1">
</form>
-----------------------
####Requested Features
    - AndroidUI Controller