ProMiniUpdate
=============

Arduino Pro Mini Library to embed a self update mechanism.
## Principle
A serial connection with a host computer can put the device into an update mode where it continuously reboots to wait for the new program to be uploaded.

The library requires 2 pins :

* 1 for the reset command, it triggers the reset pin through a condenser/resistor buffer.
* and one for the cancel switch (or jumper). It can be used for another purpose after the library's setup method has been called.

## Usage

### Hardware

![Breadboard](http://i.imgur.com/Zv3oz1t.png)
![Schematic](http://i.imgur.com/y6ux0Yi.png)

###Software

####Arduino

The most simple Arduino Sketch is : 

```CPP
#include "ProMiniUpdate.h"

#include <EEPROM.h>

#define VERSION 1
#define APPLICATION "net.alexisisaac.arduino.pmu.test"

ProMiniUpdate pmu(VERSION, APPLICATION,A3,2,0);
void setup(){
  pmu.setup();
}
void loop(){
  pmu.loop();
}
```

The parameters for the constructor are : 

1. Application Version (`unsigned int` >0)
2. Application id (`String` only letters, numbers and dot symbol)
3. Reset pin(see hardware)
4. Cancel pin (see hardware)
5. EEPROM address offset


####Updating tool
Steps : 

1. Finding the Serial port
  * It can be done by multiple ways, for instance listing all the serias ports availabke before the user plugs the device then list them again once plugged.
2. Conecting to the device
  * using those parameters 960b bauds, 8 data bits, no parity, one stop bit.
3. Requesting the current verstion of the libraryand checking the application id and current application version.
  * Sending the command `HELLO PMU\n` will return `HELLO UPDATER(pmu_version, app_version, app_id)\n`
4. Putting the device in update mode
 * Sending the command `UPDATE PMU\n` the device will respond with : `READY FOR UPDATE\n`
5. Send the new program using thestandard avr tools

If a command isn't understood the device will respond with `UNK command\n`
