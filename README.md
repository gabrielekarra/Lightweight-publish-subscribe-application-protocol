# Lightweight-publish-subscribe-application-protocol
Design and implement in TinyOS a lightweight publishsubscribe application protocol similar to MQTT and test it with simulations on a star-shaped network topology composed of 8 client nodes connected to a PAN coordinator. The PAN coordinator acts as an MQTT broker. 

### Connection
Upon activation, each node sends a CONNECT message
to the PAN coordinator. The PAN coordinator replies with a CONNACK message. If the PAN coordinator receives messages from not
yet connected nodes, such messages are ignored. Be sure to handle retransmissions if msgs get lost (retransmission if CONN or CONNACK
is lost).

### Subscribe 
After connection, each node can subscribe to one among
these three topics: TEMPERATURE, HUMIDITY, LUMINOSITY. In
order to subscribe, a node sends a SUBSCRIBE message to the PAN
coordinator, containing its node ID and the topics it wants to subscribe
to (use integer topics). Assume the subscriber always use QoS=0 for
subscriptions. The subscribe message is acknowledged by the PANC
with a SUBACK message. (handle retransmission if SUB or SUBACK
is lost)

### Publish 
Each node can publish data on at most one of the three aforementioned topics. The publication is performed through a PUBLISH
message with the following fields: topic name, payload (assume that
always QoS=0). When a node publishes a message on a topic, this is
received by the PAN and forwarded to all nodes that have subscribed
to a particular topic.

### Node Red Chart
The PAN Coordinator (Broker node) is connected to NodeRED, and periodically transmit data received on the topics to Thingspeak through MQTT. 
Thingspeak show one chart for each topic on a public channel.

## Tools used
- TinyOS 
  - nesC
- Tossim
  - Python
- Node-RED
- ThingSpeak

## How to run
1. Open the terminal
2. Start Node-RED launching `node-red` command or install it if you do not have it
3. Open you browser and go to `localhost:1880`
4. Import the flow on Node-RED from `Node-RED_flow.pdf`
5. Open [our ThingSpeak public channel](https://thingspeak.com/channels/2185815) where you can see the charts
6. Open another terminal window
7. Move to `src/`
8. Launch this command `make micaz sim`
9. Once the compile procedure is done, launch `RunSimulationScript.py`

## Credits
Developed by Davide Giannubilo & Salvatore Gabriele Karra | June 2023

