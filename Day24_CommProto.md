# Day 24[Communication_Protocols]: You cant hurt SOC-mas, Mayor Malware!

## Story :
The city of Wareville has invested in smart lights and heating, ventilation, and air conditioning (HVAC). Mayor Malware figured out how these devices were controlled and sabotaged them. Help McSkidy figure out which commands were sent.

## Learning Objectives : 
- The basics of the MQTT protocol
- How to use Wireshark to analyze MQTT traffic
- Reverse engineering a simple network protocol

## Abbreviations and Applications :
- [MQTT](https://mqtt.org/) : Message Queuing Telemetry Transport, MQTT is an OASIS standard messaging protocol for the Internet of Things (IoT). Extrememly lightweight, ideal for remote devices with small footprint and less network bandwidth.
- [IoT](https://developer.tuya.com/en/docs/Document/introduction-of-iot?id=Kamwscyddoegn) : IoT (Internet of Things) refers to the network of physical objects, or "things", that are embedded with sensors and software which allow them to collect and exchange data over the Internet.

## Process Key Steps and Points :
- MQTT Clients: MQTT clients are IoT devices, such as sensors and controllers, that publish or subscribe to messages using the MQTT protocol.
- MQTT Broker: An MQTT broker receives messages from publishing clients and distributes them to the subscribing clients based on their preferences.
- MQTT Topics: Topics are used to classify the different types of messages.

## Tools and Commands Used :
- `mosquitto_pub`

## Questions, Hints and Answers :
1. What is the flag?
   - Hint :
     - Topic : `d2FyZXZpbGxl/Y2hyaXN0bWFzbGlnaHRz` 
     - Message : `on`
     - Command : `mosquitto_pub -h localhost -t "d2FyZXZpbGxl/Y2hyaXN0bWFzbGlnaHRz" -m "on"`
   - ![flag_mqtt](/Screenshots/D24.png)
   - Ans : `THM{Ligh75on-day54ved}`