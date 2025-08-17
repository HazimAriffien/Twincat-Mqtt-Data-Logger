# TwinCAT 3 MQTT Logger with IO-Link (AL1330 + Sensor OID 254)
This project is my learning journey with **TwinCAT 3**, **Ethercat**, **IO-Link** and **MQTT**. It also serves as a Portfolio project as a student that is interested in Automation in the Industry.

The main Idea and Goal of this Project:
* Connect an optical sensor (OID 254) through an AL1330 IO-Link master into TwinCAT 3 Project and reading the sensor value.
* Configure EtherCAT master/slave and I/O mapping in the TwinCat3 Project.
* Use The MQTT Connection in TwinCat3(TF6701) to publish the sensor values from the PLC to a broker.
* Try and Implement a bidirectional MQTT Connection (Pub/Sub) between the PLC and the Broker.
* Visualize the Sensor Value and add a Trigger to Collect Value Using Node-Red API.

For me, this was about:
* Learning how to configure I/O in TwinCAT.
* Understanding and Learning how to read the Sensor Documentation for the Ethercat and IO-Link Interface.
* Writing simple Function Blocks in TwinCAT to execute my desired goal.
* Trying out MQTT Interface in TwinCat and connecting PLC ↔ Broker ↔ Node-RED.
* Working with a real sensor and seeing live data flow.

## Hardware and Software Prerequisites
### Hardware
* [IFM Optical Sensor (OID 254)](https://www.ifm.com/us/en/product/OID254)
* [IO-Link Master AL1330](https://www.ifm.com/us/en/product/AL1330)
* Windows laptop with TwinCAT runtime (TwinCat XAR)

### Software
* TwinCAT XAE
* Mosquitto MQTT Broker
* Node-RED (with dashboard Palette Installed)
* MQTT Explorer (optional for debugging)

## TwinCat Solution and Function Blocks Created
Below is a detailed explanation of the Function Blocks that are created in the TwinCat Solution that enables the reading of the Sensor Value and the Connection with the MQTT Broker.

![Function Blocks in TwinCat](https://github.com/HazimAriffien/Twincat-Mqtt-Data-Logger/blob/main/Pics%20%26%20Vids/MQTT_TwinCat_Function_Blocks.jpg)

### FB_OpticalSensor
This block links the PLC variables to the I/O data from EtherCAT and the IO-Link master. It reads the raw process data bits from the sensor and applies bit shifting to decode them. The output is the sensor’s distance value as an integer.
### FB_MyMqtt
This block extends Beckhoff’s FB_IotMqttClient to add custom behavior. It implements a callback method that ensures real-time handling of subscribed MQTT messages. This allows the PLC to react immediately to incoming data.
### FB_MqttClient
This block manages the overall MQTT connection and communication. It uses an instance of FB_MyMqtt to interact with the broker, handling both subscribe and publish operations. It also prepares the topic names and payloads for publishing.

## MQTT Communication Architecture
Below is a simple illustration of the MQTT Communication between three parties. TwinCat PLC, Mosquitto Broker and Node-Red

![MQTT Connection](https://github.com/HazimAriffien/Twincat-Mqtt-Data-Logger/blob/main/Pics%20%26%20Vids/MQTT_Connection_Pic.jpg)

In the implemented system, the optical sensor data is transmitted using the MQTT protocol, which follows a publish/subscribe model. The system consists of three components: the PLC (Hazim), the Mosquitto broker, and Node-RED. The PLC subscribes to the topic ***Hazim/Mqtt Logger/Optical Sensor/Get Data*** and only publishes sensor readings to ***Hazim/Mqtt Logger/Optical Sensor/Data*** when it receives a request signal  from Node-RED. Node-RED acts as the publisher for the topic ***Hazim/Mqtt Logger/Optical Sensor/Get Data*** and simultaneously subscribes to the topic ***Hazim/Mqtt Logger/Optical Sensor/Data*** to receive and visualize the sensor data on a dashboard. The Mosquitto broker handles all message routing between publisher and subscriber, enabling a decoupled, on-demand data transmission system where sensor data is only published when explicitly requested.

## Conclusion and Results
In conclusion, it was possible to display the optical sensor values in real time in Node-RED, with the PLC reacting according to the request signal sent to the Get Data topic. To demonstrate the results, a short video was recorded, which can be downloaded [here](https://github.com/HazimAriffien/Twincat-Mqtt-Data-Logger/blob/main/Pics%20%26%20Vids/MQTT_Result_Video.mp4). Overall, this small project was a success and provided valuable hands-on experience with MQTT communication, PLC programming, and real-time data visualization. It offered a great learning experience for me to get used to TwinCat and PLC Programming.




