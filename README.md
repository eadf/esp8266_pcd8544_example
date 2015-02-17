# esp8266_pcd8544
[PCD8544 LCD driver](https://github.com/eadf/esp8266_pcd8544) example for esp8266 (Nokia 5110 &amp; 3110 display)

The driver is a direct port of code found at [arduino playground.](http://playground.arduino.cc/Code/PCD8544)

The interface requires 5 available GPIO outputs so an ESP-01 will not work. 

This is how the code is hooked up by default:

PCD8544| ESP8266
-------|------------------
RST Pin 1 | GPIO4
CE  Pin 2 | GPIO5
DC  Pin 3 | GPIO12
Din Pin 4 | GPIO13
Clk Pin 5 | GPIO14

Some ESP-12 have GPIO4 & GPIO5 reversed.
All of the pins are configurable, you just set the pins you want to use in the setting struct.

I don't know if it is required but i put 1KΩ resistors on each GPIO pin, and it does not seem to cause any problems. 

Take a look at [esp_mqtt_lcd](https://github.com/eadf/esp_mqtt_lcd) to see another example on how the pcd8544 driver can be used as a library module (git subtree) in your own project.

The makefile is copied from [esp_mqtt.](https://github.com/tuanpmt/esp_mqtt)

###Building and installing:

First you need to install the sdk and the easy way of doing that is to use [esp_open_sdk.](https://github.com/pfalcon/esp-open-sdk)

You can put that anywhere you like (/opt/local/esp-open-sdk, /esptools etc etc)

Then you could create a small ```setenv.sh``` file, containing the location of your newly compiled sdk and other platform specific info;
```
export SDK_BASE=/opt/local/esp-open-sdk/sdk
export PATH=${SDK_BASE}/../xtensa-lx106-elf/bin:${PATH}
export ESPPORT=/dev/ttyO0  
```
(or setup your IDE to do the same)

To make a clean build, flash and connect to the esp console you just do this in a shell:
```
source setenv.sh # This is only needed once per session
make clean && make test
```

You won't be needing esptool, the makefile only uses esptool.py (provided by esp-open-sdk)

I have tested this with sdk v0.9.5 and v0.9.4 (linux & mac)
