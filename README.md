# d1mini-oled-button

The goal is to create an application using a button, a screen, and interaction with an online IoT portal using MQTT.

## Hardware list

 * Wemos.cc D1 Mini v2.3.0
 * Wemos.cc OLED Shield v1.1.0
 * Wemos.cc 1-button Shield v2.0.0
 * Wemos.cc Tripler base v1.0.0
 * USB - Micro USB cable
 * Button cap
 
Most hardware is ordered via the AliExpress Wemos store. It combines shipping costs when ordering multiple products. The button cap and USB cable are from my stock. Since the tripler base contains a prototyping area, it is easy to add other I/O.

The configuration uses female headers on the triple base, and the d1 mini and shields next to each other using male header pins below. So the button can be operated, the OLED can be read and the LED on the d1 mini can be seen. 

## Arduino configuration

In the preferences, add one additional board manager URL `http://arduino.esp8266.com/stable/package_esp8266com_index.json`.
Then in the Board Manager menu, search for Wemos, and install the *esp8266* by *ESP8266 Community*. Select the correct board and COM/USB port.
To verify you can use the `SimplePush.ino` from the referenced button shield examples, that uses the button to switch on the LED on the ESP module.

The next step is to connect the OLED shield. The shield defaults to I2C address 0x3C. You can verify this addresss with the referenced `I2C_Scanner.ino` example. After uploading the sketch to the board, open the serial monitor and the address is printed there. This confirms the shield uses the D1/D2 ports for I2C and the I2C address.

In the Arduino IDE, use the library manager to install the `sparkfun micro oled breakout` so that `SFE_MicroOLED.h` is available. Use the wemos oled example `OLED_Clock_with_SparkFun.ino`. It displays an analog clock, but you need to set the time in the code yourself. This confirms the oled shield is working.

After this it is usefull to check your Wifi. Open the Arduino IDE example sketch `ESP8266Wifi/NTPClient` from the menu. Change in code the ssid and pass for your WiFi. And upload it to the D1 mini. Open the serial monitor, and select the correct baud rate. It displays about every 11 seconds, the UTC time. This confirms that the ESP8266 antenna has network reach at the moment.

The next step is to configure the MQTT libraries. Using the Arduino Library Manager, search for an MQTT library that is useful for your IoT MQTT server. Since I already have an account at [Cayenne MyDevices](http://cayenne.mydevices.com) the *CayenneMQTT* by *myDevices* seems to be a good choice, but unfortunately not for the ESP8266. From the dashboard you can follow a link to the GitHub account of MyDevicesIoT. Navigate to `https://github.com/myDevicesIoT/Cayenne-MQTT-ESP8266`, download `Cayenne-MQTT-ESP8266-master.zip`, then in Arduino IDE go to Libraries and add a Library as a ZIP file. Then in the Arduino IDE, select Examples, Cayenne-MQTT-ESP8266, ESP8266. That example needs additional configuration, so:

 * Login to your Cayenne.myDevices.com dashboard 
 * Select *Add new...*
 * Select the blue button *Bring Your Own Thing*
 * Copy your MQTT Username
 * Copy your MQTT Password
 * Copy your Client ID
 * Name your device `Wemos`

In the Arduino IDE, adjust these lines using your local WiFi login and the Cayenne settings.
 
    // WiFi network info.
    char ssid[] = "SSID";
    char wifiPassword[] = "PASS";

    // Cayenne authentication info. This should be obtained from the Cayenne Dashboard.
    char username[] = "MQTT_USERNAME";
    char password[] = "MQTT_PASSWORD";
    char clientID[] = "CLIENT_ID";
    
Now on your myDevices dashboard, there is a rectangle with a `+` to `Add to your dashboard`, so click it. Then the value is displayed. On the top right of the value widget, there is a `Settings`, change the Widget name to `uptime`, the icon to `Date/Time` and the decimals to `0`. Using `Details & Chart` you can see the values in a timeline. You can also change the device icon of your Wemos device name to `Wi-Fi`.

	
	

## Reference

 * [Wemos on GitHub](https://github.com/wemos)
 * [Wemos D1 mini Wiki](https://wiki.wemos.cc/products:d1:d1_mini)
 * [Solder configuration 'male below'](https://github.com/wemos/Fritzing-Part-WeMos-D1-Mini)
 * [Wemos Button Shield examples](https://github.com/wemos/D1_mini_Examples/tree/master/examples/04.Shields/1_Button_Shield)
 * [Wemos I2C Scanner example](https://github.com/wemos/D1_mini_Examples/tree/master/examples/02.Special/Wire/I2C_Scanner)
 * [Wemos OLED examples](https://github.com/wemos/D1_mini_Examples/tree/master/examples/04.Shields/OLED_Shield/Use_SparkFun_Library)
 * [SparkFun Micro OLED Library](https://github.com/sparkfun/SparkFun_Micro_OLED_Arduino_Library)
 * [myDevices IoT Cayenne library for MQTT and ESP8266](https://github.com/myDevicesIoT/Cayenne-MQTT-ESP8266)
 
 
## Hardware configuration 

### D1 mini pinout

The d1 mini has 4M bytes flash and runs at 80MHz/160MHz.

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

Pin | Function | ESP8266 Pin
--- | -------- | -----------
TX  | TXD | TXD
RX | RXD | RXD
A0 | Analog input, max 3.3V input | A0
D0 | IO | GPIO16
D1 | IO, SCL | GPIO5
D2 | IO, SDA | GPIO4
D3 | IO, 10k Pull-up | GPIO0
D4 | IO, 10k Pull-up, BUILTIN_LED | GPIO2
D5 | IO, SCK | GPIO14
D6 | IO, MISO | GPIO12
D7 | IO, MOSI | GPIO13
D8 | IO, 10k Pull-down, SS | GPIO15
G | Ground | GND
5V | 5V | -
3V3 | 3.3V | 3.3V
RST | Reset | RST

 * All of the IO pins have interrupt/pwm/I2C/one-wire support except D0.
 * All of the IO pins run at 3.3V.


### OLED pinout

Pin | Note
--- | -----
D1  | I2C SCL
D2  | I2C SDA

### Button pinout

Pin | Note
--- | -----
D3  | 10k pull-up, push connects GND



