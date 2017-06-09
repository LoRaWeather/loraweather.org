# Welcome to LoRaWeather!
LoRaWeather is a project that is created as a graduation assignment. The assignment:

_"Create an open source weather station that sends data over the LoRa network to The Things Network."_

All programs that were made and open source can be found [here](https://github.com/LoRaWeather) in the LoRaWeather organization on Github.

The project exists of the following contents:

  1. BME280 to LoPy to The Things Network
  2. Data from The Things Network to InfluxDB by MQTT broker
  3. Xamarin application

### BME280 to LoPy to The Things Network
Firstly, two researches has been done. One to research what the best hardware is to use for the project and secondly to research what the best way is to send data over the LoRa network.

For the hardware: as a LoRa controller the Pycom LoPy is used. This is a ESP32 based microcontroller with a LoRa chip on top. The microcontroller is programmed in Python. The LoPy was the best choice for the project because it was easy to use, not too expensive and not too big. The BME280 sensor is the best option to use as a sensor. The BME280 is a sensor that reads temperature, humidity and pressure. I2C is used to communicate with the sensor and microcontroller.

LoRa network: The data that is read from the sensor is packed into one object. The object has only a size of 6 bytes. The object contains: Battery status, version, temperature (2 decimals), humidity, pressure (1 decimal). After reading the data the LoPy will try to connect to The Things Network, this is done by OTAA (Over The Air Activation). The Things Network is a community that makes it possible to use the LoRa network for free. Once connected the LoPy will start sending the bytes to The Things Network. Ideally the LoPy should go into deepsleep mode for about one hour, after that it repeats the process.

The program can be found [here](https://github.com/LoRaWeather/BME280-LoPy-TTN) on GitHub.

### Data from The Things Network to InfluxDB by MQTT broker
When the data has been send to The Things Network the data is only available for a small amount of time. A solution for this is MQTT (Message Queue Telemetry Transport). MQTT is a known protocol in the IoT scene. With MQTT there is a broker, the broker can be seen as a service. A program can subscribe to that service. When a message is send from that service, all programs that subscribed will get that message. The Things Network also has a MQTT broker. When data has been send to The Things Network, it will send the message to all programs that have subscribed to the broker. The program that has been created is a .NET Core application. The program subscribes to the broker and listens for incoming messages.

When there is a message the program will decode the data and store it into a InfluxDB database. InfluxDB is a time series database. This means it will save a timestamp every time new data has been stored. This way you get historical data which is very handy for weather stations.

The program can be found [here](https://github.com/LoRaWeather/TTN-MQTT-InfluxDB) on GitHub.
### Xamarin application
A Xamarin Forms application has been made to show all data that is stored into InfluxDB. When opening the app it will show a map of the Netherlands with all available devices. By clicking on the pins on the map another page will open with info about the device. By clicking the data button another page will open with data of the sensor.

A picture of the app:

![Begin Page](https://user-images.githubusercontent.com/25667411/26977425-1f8be570-4d28-11e7-9b25-f6adc192159a.png)

The application and other pictures can be found [here](https://github.com/LoRaWeather/loraweather-app) on GitHub.
