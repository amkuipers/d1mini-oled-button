# d1mini-oled-button

The goal is to create an application using a button, a screen, and interaction with an online IoT portal using MQTT.

## Hardware list

 * Wemos.cc D1 Mini v2.3.0
 * Wemos.cc OLED Shield v1.1.0
 * Wemos.cc 1-button Shield v2.0.0
 * Wemos.cc Tripler base v1.0.0
 * USB cable
 * Button cap
 
Most hardware is ordered via the AliExpress Wemos store. It combines shipping costs when ordering multiple products. The button cap and USB cable are from my stock. Since the tripler base contains a prototyping area, it is easy to add other I/O.

## Reference

 * [Wemos](https://github.com/wemos)
 * [Solder configuration 'male below'](https://github.com/wemos/Fritzing-Part-WeMos-D1-Mini)
 

## Hardware configuration 
 
![Image of D1 mini](https://github.com/wemos/Fritzing-Part-WeMos-D1-Mini/blob/master/src/svg.icon.WeMos-D1-mini-male-headers-below_icon.svg)

### D1 mini pinout

Looking at the board with the reset switch in the lower left corner. 

Left  | Right
----- | -----
RST   | TX
A0    | RX
D0    | D1
D5    | D2
D6    | D3
D7    | D4
D8    | GND
3V3   | 5V

### OLED pinout

Pin | Note
--- | -----
D1  | I2C SCL
D2  | I2C SDA

### Button pinout

Pin | Note
--- | -----
D3  | On/Off



