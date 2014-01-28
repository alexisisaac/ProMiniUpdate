ProMiniUpdate
=============

Arduino Pro Mini Library to embed a self update mechanism.
## Principle

## Usage
### Hardware
![Imgur](http://i.imgur.com/Zv3oz1t.png)
###Software
####Arduino

####Updating tool
Steps : 

1. Finding the Serial port
  * It can be done by multiple ways, for instance listing all the serias ports availabke before the user plugs the device then list them again once plugged.
2. Conecting to the device
  * using those parameters 960b bauds, 8 data bits, no parity, one stop bit.
3. Requesting the current verstion of the libraryand checking the application id and current application version.
  * Sending the command `HELLO PMU\n` will return `HELLO UPDATER(pmu_version, app_version, app_id)\n`
