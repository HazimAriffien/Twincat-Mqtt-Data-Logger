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
