# Welcome to LoRaWeather!
LoRaWeather is a project that is created as a graduation assignment. The assignment:
</br></br>_"Create an open source weather station that sends data over the LoRa network to The Things Network."_</br>

All programs that were made and open source can be found [here](https://github.com/LoRaWeather) within the LoRaWeather organization on Github.

The project exists of the following contents:

1. BME280 to LoPy to The Things Network
2. Data from The Things Network to InfluxDB by MQTT broker
3. Xamarin application

### BME280 to LoPy to The Things Network
Firstly, two researches has been done. One to research what the best hardware is to use for the project and secondly to research what the best way is to send data over the LoRa network.

For the hardware: as a LoRa controller the Pycom LoPy is used. This is a ESP32 based microcontroller with a LoRa chip on top. The microcontroller is programmed in Python. The LoPy was the best choice for the project because it was easy to use, not too expensive and not too big. The BME280 sensor is the best option to use as a sensor. The BME280 is a sensor that reads temperature, humidity and pressure. I2C is used to communicate with the sensor and microcontroller.

LoRa network: The data that is read from the sensor is packed into one object. The object has only a size of 6 bytes. The object contains: Battery status, version, temperature (2 decimals), humidity, pressure (1 decimal). After reading the data the LoPy will try to connect to The Things Network, this is done by OTAA (Over The Air Activation). The Things Network is a community that makes it possible to use the LoRa network for free. Once connected the LoPy will start sending the bytes to The Things Network. Ideally the LoPy should go into deepsleep mode for about one hour, after that it repeats the process.

The program can be found [here](https://github.com/LoRaWeather/BME280-LoPy-TTN) on Github.

### Data from The Things Network to InfluxDB by MQTT broker
After

### Xamarin application
Lastly,
