---
layout: default
---
# RCJS

RCJS is a utility that allows multiple <b>R</b>elay boards to be <b>C</b>ontrolled through <b>J</b>ava<b>S</b>cript. RCJS can be implemented on the following devices:
- Raspberry Pi 2 Model A+
- Raspberry Pi 2 Model B
- _Raspberry Pi 2 Model B+_
- Raspberry Pi 3 Model B
- _Raspberry Pi 3 Model B+_

``
Italics indicates the model is currently in use, running RCJS, by the developer.
``

RCJS can be used wirelessly, or through ethernet. The Raspberry Pi hosts a webpage through which devices on the [LAN](https://en.wikipedia.org/wiki/Local_area_network) may use to control multiple relay boards. It is likely that RCJS can be modified by the end-user to work over [IP](https://en.wikipedia.org/wiki/Internet_Protocol).

The control of multiple relays is accomplished through the use of the [I2C](https://en.wikipedia.org/wiki/I%C2%B2C) protocol. Testing communications with I2C devices can be aided on Linux with the use of [i2c-tools](https://git.kernel.org/pub/scm/utils/i2c-tools/i2c-tools.git/), which comes pre-installed on Raspian. Consult the [man pages](https://www.mankier.com/package/i2c-tools) for how to use i2c-tools.

## Dependencies
RCJS is built on [Node.js](https://nodejs.org/en/). Please consult [this guide](https://nodejs.org/en/download/package-manager/) for how to install Node.js.

### Packages used by RCJS:

```js
// Packages to allow client connections to a hosted HTTP server
var http = require('http')
var url = require('url')
var fs = require('fs')
var path = require('path')

// Packages to allow hardware control
var raspi = require('raspi')
var I2C = require('raspi-i2c')
```

In order to install these packages from the ``packages.json`` file, use ``npm install``.

Documentation for all of the packages used may be found [here](https://www.npmjs.com/).

## Wiring and Testing

A pinout table for compatible Raspberry Pi devices can be found [here](./raspberrypinout.html).

I2C1 SDA and SCL should be connected in parallel to all I2C devices to form the [I2C bus](https://www.i2c-bus.org/). Proper wiring of the I2C bus will have the clock, SCL; and the data, SDA lines independent from each other. This bus will be recognized by the operating system as I2C Bus 1, with addresses to each devices. It is important that no two devices on the I2C bus share an address (If you are unable to change the address of a device, an [I2C multiplexer](http://www.ti.com/interface/i2c/switches-and-multiplexers/products.html) may be used.) To view the addresses on I2C Bus 1, use:
```
i2c-detect -y 1
```

These addresses can be tested manually with:
```
//To send data to and I2C device
i2c-set -y 1 ADDRESS A B // Where A and B are hex bytes being sent to the I2C device.
```
and
```
//To read data from an I2C device
i2c-get -y 1 ADDRESS
```

##
