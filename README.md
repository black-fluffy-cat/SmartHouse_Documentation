# SmartHouse Arduino and Raspberry codes

Documentation for SmartHouse project which currently consists of 4 repositories:
#### [Documentation](https://github.com/black-fluffy-cat/SmartHouse_Documentation)
#### [Server application](https://github.com/black-fluffy-cat/SmartHouseServer)
#### [Arduino nodes source codes](https://github.com/black-fluffy-cat/SmartHouse_ArduinoCodes)
#### [Raspberry nodes scripts](https://github.com/black-fluffy-cat/SmartHouse_Raspberry)

## Server (KtorSmartHouseServer)

Server written in Ktor, receives data from nodes with sensors, processes it and sends data to proper devices
- '/alert' - receives POST request with AlertData and pings Raspberry node to make photo
- '/heartbeat' - receives POST request with HeartbeatData from nodes
- '/raspPhoto' - POST/GET immediatelly ping Raspberry to make photo
- '/health' - responds text message for GET requests
- '/receiveNgrokAddresses' - receives POST request with Ngrok addresses of sender (node)
- '/receivePhoto' - receives POST request with photo as Multipart file
- '/sensor/postValues' - receives POST request with SensorValues and saves them to file
- '/receiveVideo' - receives POST request with video as Multipart file

## Arduino nodes source codes

Arduino codes for nodes with sensors

NodeMCU with IR sensors:
- sends HeartbeatData to server every 30 seconds
- sends AlertData to server when received signal from IR sensor

NodeMCU with BME280 sensor:
- sends HeartbeatData to server every 30 seconds
- sends BME280Data to server every 10 seconds

## Raspberry nodes scripts

Raspberry scripts for nodes with cameras

Raspberry Pi Zero with normal camera and Raspberry Pi Zero with IR wide-angle camera:
- sends HeartbeatData to server every 30 seconds
- takes and sends image to server after receiving POST message on '/alertPhoto' endpoint

Raspberry Pi 4B - currently used as Server


# SmartHouse Documentation
Documentation for SmartHouse project that contains informations about used sensors, devices, created Android application and Ktor server. Main target of this project is to create tools that will allow to monitor, control and gather data from external devices for various purposes (e.g. SmartHouse) but also to get experience and expand knowledge.

## Documents(Documents)
Documents and charts of SmartHouse systems
Contains valuable notes about how to setup server, raspberry and other nodes

## Used nodes
There are four main nodes that are used in current version of project:

- NodeMCU v3.0 (ESP8266) with sensors (temperature, humidity, pressure, proximity, etc.)
- Raspberry Pi Zero with camera
- Raspberry Pi 4B as Ktor server

### Nodemcu v3.0 (ESP8266) with sensors
#### Used sensors:
- HC-SR04 Ultrasonic Ranging Module
- DHT11 Internal temperature and humidity sensor
- BME280 Temperature, Humidity, Pressure sensor
#### Communication:
- with sensors - by jumper wires
- with server - by network, by sending data as JSON
#### Specification:
- Input (VCC) voltage 5V
- Logic pins input voltage 3.3V
- Sensors (VCC) input voltage 5V
#### Used external libraries:
- [Arduino DHT](https://github.com/markruys/arduino-DHT)
- [BME280](https://github.com/adafruit/Adafruit_BMP280_Library)
#### Pin layout:
- Nodemcu v3.0 TODO
- HC-SR04 TODO
- DHT11 TODO
#### Node schematics:
- TODO

### Raspberry Pi Zero WH
#### Used as:
- Camera node
#### External devices:
- ZeroCam 5Mpx
#### Communication:
- with camera - by camera flex cable
- with server - by network, sends image in form of `MultipartFile`
#### Specification:
- Input voltage 5V
#### Used external libraries:
- picamera
- datetime
- requests
- threading
- os
- time

### Raspberry Pi 4B
#### Used as:
- Server
#### External devices:
- None
#### Communication:
- with nodes - by network
#### Specification:
- Input voltage 5V
#### Used external libraries:
- same as used in Ktor server
