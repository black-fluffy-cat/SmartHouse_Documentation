# SmartHouse Arduino and Raspberry codes

Source codes for Arduino and scripts for Raspberry. Part of SmartHouse project.


### [Server application (new - Ktor)](https://github.com/black-fluffy-cat/SmartHouseServer)
### [Images of external devices](Images%26Screenshots)

## Server (KtorSmartHouseServer)

Server written in Ktor, receives data from nodes with sensors, processes it and sends data to proper devices
- '/alert' - receives POST request with AlertData and pings Raspberry node to make photo
- '/heartbeat' - receives POST request with HeartbeatData from nodes
- '/raspPhoto' - POST/GET immediatelly ping Raspberry to make photo
- '/health' - responds text message for GET requests
- '/receiveNgrokAddresses' - receives POST request with Ngrok addresses of sender (node)
- '/receivePhoto' - receives POST request with photo as Multipart file

## ArduinoCodes

Arduino codes for nodes with sensors

NodeMCU with IR sensors:
- sends HeartbeatData to server every 30 seconds
- sends AlertData to server when received signal from IR sensor

NodeMCU with BME280 sensor:
- sends HeartbeatData to server every 30 seconds
- sends BME280Data to server every 10 seconds

## Documents

Documents and charts of SmartHouse systems
Contains valuable notes about how to setup server, raspberry and other nodes

# SmartHouse Documentation
Documentation for SmartHouse project that contains informations about used sensors, devices, created Android application and Ktor server. Main target of this project is to create tools that will allow to monitor, control and gather data from external devices for various purposes (e.g. SmartHouse) but also to get experience and expand knowledge.

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
