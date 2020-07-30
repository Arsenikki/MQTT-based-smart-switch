# General
The goal of this project is to  a ESP8266 based smart switch from cloud control to local control using MQTT. This ensures low latency and that data stays in the home network. 

> WARNING! Disassembling the smart switch will probably void the warranty and never keep it connected to live voltage without enclosure. 

# Requirements
## Hardware:
- Sonoff S26 Smart Switch 
- FTDI USB to Serial programmer (Mine is based on CH340 board) 
## Software
- Visual Studio Code
- PlatformIO extension for VS Code
- CH340 drivers
# Preparations for flashing
1. Clone newest version of Tasmota from official repository: https://github.com/arendst/Sonoff-Tasmota
2. Start PlatformIO in VS Code and click open project. Select Tasmota folder, which was downloaded in previous step
3. Navigate to ``Sonoff-Tasmota-master\sonoff`` and open ``my_user_config.h``
4. Fill in Wifi SSID and password, everything else can be set easily afterwards.
```
#define STA_SSID1              "ExampleSSID"                // [Ssid1] Wifi SSID
#define STA_PASS1              "ExamplePassword"            // [Password1] Wifi password
```
## Hardware preparation
1. Disassemble the smart switch
2. Soldering the pins is not mandatory, but recommended. I decided to not solder and just pressed the pins against 4 PCB contacts.
(Extensive guide at: https://github.com/arendst/Sonoff-Tasmota/wiki/Hardware-Preparation)
## Flashing
2. Connect FTDI adapter to PC by USB
3. Hold down reset button of ESP8266 and connect VCC, GND pins to ESP8266 board to enter flashing mode
4. Connect also RX and TX, but have them reversed.
5. Finally select platformio.ini in VS code file browser and press Build and then Upload from bottom tab. (Around 1 min)
## Check if everything works so far
1. Open PlatformIO serial monitor
2. Select USB FTDI adapter as port and set Baud rate to 115200
3. Reconnect VCC pin to force restart
4. Check if device succeeds to connect to Wifi and is given an IP address
## MQTT configuration
1. Open browser and write IP address from previous step to address bar
2. In web UI select ``Configuration - Configure module`` menu select according device, in this case ``Sonoff S2X``
3. In ``Configuration - Configure MQTT`` menu add credentials of your MQTT broker. I set Topic to: ``sonoff_1`` and Full topic to ``%prefix%/%topic%/`` This topic structure is just an example and it will be needed when adding the device as an MQTT client to the MQTT broker.  

Enjoy.
