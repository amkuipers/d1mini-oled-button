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

The configuration uses female headers on the triple base, and the d1 mini and shields next to each other using male header pins below. So the button can be operated, the OLED can be read and the LED on the d1 mini can be seen. 

## Arduino configuration

In the preferences, add one additional board manager URL `http://arduino.esp8266.com/stable/package_esp8266com_index.json`.
Then in the Board Manager menu, search for Wemos, and install the *esp8266* by *ESP8266 Community*. Select the correct board and COM/USB port.
To verify you can use the `SimplePush.ino` from the referenced button shield examples, that uses the button to switch on the LED on the ESP module.

The next step is to connect the OLED shield. The shield defaults to I2C address 0x3C. You can verify this addresss with the referenced I2C_Scanner example. After uploading the sketch to the board, open the serial monitor and the address is printed there. This confirms the shield uses the D1/D2 ports for I2C and the I2C address.

In the Arduino IDE, use the library manager to install the `sparkfun micro oled breakout` so that `SFE_MicroOLED.h` is available. Use the wemos oled example `OLED_Clock_with_SparkFun`. It displays an analog clock, but you need to set the time in the code yourself. This confirms the oled shield is working.

After this it is usefull to check your Wifi. Open the Arduino IDE example sketch ESP8266Wifi/NTPClient from the menu. Change the ssid and pass for your WiFi. And upload it to the D1 mini. Open the serial monitor, and select the correct baud rate. It displays about every 11 seconds, the UTC time. This confirms that the ESP8266 antenna has network reach at the moment.

The next step is to configure the MQTT libraries.


## Reference

 * [Wemos](https://github.com/wemos)
 * [Solder configuration 'male below'](https://github.com/wemos/Fritzing-Part-WeMos-D1-Mini)
 * [Board manager ESP8266 boards URL](http://arduino.esp8266.com/stable/package_esp8266com_index.json)
 * [Wemos Button Shield examples](https://github.com/wemos/D1_mini_Examples/tree/master/examples/04.Shields/1_Button_Shield)
 * [Wemos I2C Scanner example](https://github.com/wemos/D1_mini_Examples/tree/master/examples/02.Special/Wire/I2C_Scanner)
 * [Wemos OLED examples](https://github.com/wemos/D1_mini_Examples/tree/master/examples/04.Shields/OLED_Shield/Use_SparkFun_Library)
 * [SparkFun Micro OLED Library](https://github.com/sparkfun/SparkFun_Micro_OLED_Arduino_Library)
 
 
## Hardware configuration 

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
D3  | Push connects GND



