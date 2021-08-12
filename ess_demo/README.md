# Bluetooth ESS (Environmental Sensing Service) Sample Application

## Overview

This sample application demonstrates a Zephyr re-implementation of the
BL654 Sensor board smartBASIC application from
[https://github.com/LairdCP/BL654_BME280/](https://github.com/LairdCP/BL654_BME280/) -
it uses the on-board BME280 or BME680 sensor to read temperature,
humidity and air pressure and calculates the dew point for the specific
conditions which it then sends to a connected central Bluetooth Low
Energy device via GATT which has enabled notifications or reads the
characteristics.

## Supported Boards

* BL654 Sensor Board (included with Pinnacle 100 development kit)
* Pinnacle 100 development kit
* BL5340 development kit

## Requirements

* BL654 sensor board, Pinnacle 100 development board or BL5340
  development board to run this demo
* Pinnacle 100/MG100/BL5340 programmed with the BLE Gateway Firmware
  out-of-box demo application which will upload the data to AWS,
  alternatively an android mobile phone with the nRF connect mobile
  application

## Service Details

For details on the Bluetooth Low Energy service [see here.](docs/ble.md)

## Usage

### BL5340

The BL5340 version of this project utilises the LCD on the BL5340
development kit to show an interactive chart of the data which plots
the temperature, humidity, pressure and dew point values on the graph,
each data set can be enabled or disabled independently by touching the
check boxes. To configure the project for the BL5340, run the following:

```
mkdir build
cd build
cmake -GNinja -DBOARD=bl5340_dvk_cpuapp ..
```

Then build the project using:

```
ninja
```

To flash the compiled code to a development kit use the command:

```
ninja flash
```

Once the board has been flashed, the display will update and show the
graph of the data which will populate over time.

### Pinnacle 100

The Pinnacle 100 version of this project uses the on-board BME680
sensor on the development board (not compatible with the MG100 as
there is no BME680 sensor present). To configure the project for the
Pinnacle 100, run the following:

```
mkdir build
cd build
cmake -GNinja -DBOARD=pinnacle_100_dvk ..
```

Then build the project using:

```
ninja
```

To flash the compiled code to a development kit use the command:

```
ninja flash
```

Once the board has been flashed, the module will begin advertising
which can then be read from a mobile phone or using the BLE Gateway
Firmware which can be downloaded and run on an [Pinnacle 100/MG100 from here](https://github.com/LairdCP/Pinnacle-100-Firmware-Manifest/releases)
or [BL5340 development kit from here](https://github.com/LairdCP/BL5340_Firmware_Manifest/releases).

### BL654 Sensor Board

The BL654 Sensor Board version of this project will build and operate
in a low-power mode with all debugging options disabled to maximum
battery life and utilises the on-board BME280 sensor. To configure the
project for the BL654 Sensor Board, run the following:

```
mkdir build
cd build
cmake -GNinja -DBOARD=bl654_sensor_board ..
```

Then build the project using:

```
ninja
```

To flash the compiled code to a sensor, it must be connected to a SWD
programming device such as a [Laird Connectivity USB-SWD Programming Board](https://www.lairdconnect.com/usb-swd-programmer)
or [Segger J-Link](https://www.segger.com/products/debug-probes/j-link/)
with a [Tag Connect TC2030-CTX cable](https://www.tag-connect.com/product/tc2030-ctx-6-pin-cable-for-arm-cortex),
refer to the [Zephyr documentation](https://docs.zephyrproject.org/latest/boards/arm/bl654_sensor_board/doc/bl654_sensor_board.html)
for details on how to program the sensor. If using the USB-SWD
programming board, flash the code using the command:

```
ninja flash
```

Once the sensor has been flashed, it can be removed from the programming 
unit and used standalone.

## PTS

Note that this application is provided as a sample only to demonstrate
basic sensor functionality over BLE and is for evaluation use only, it
has not been tested through PTS for confirming that it adheres to the
ESS service specification.

## Links

* [Pinnacle 100 product page](https://www.lairdconnect.com/wireless-modules/cellular-solutions/pinnacle-100-modem)
* [MG100 product page](https://www.lairdconnect.com/iot-devices/iot-gateways/sentrius-mg100-gateway-lte-mnb-iot-and-bluetooth-5)
* [BL5340 product page](https://www.lairdconnect.com/wireless-modules/bluetooth-modules/bluetooth-5-modules/bl5340-series-multi-core-bluetooth-52-802154-nfc-modules)
* [Pinnacle 100/MG100 firmware](https://github.com/LairdCP/Pinnacle-100-Firmware-Manifest/releases)
* [BL5340 firmware](https://github.com/LairdCP/BL5340_Firmware_Manifest/releases)
* [nRF Connect Android app](https://play.google.com/store/apps/details?id=no.nordicsemi.android.mcp)
