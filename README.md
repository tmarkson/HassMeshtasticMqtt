# HassMeshtasticMqtt
Integrate a Meshtastic device into Home assistant via MQTT

https://meshtastic.org/docs/software/mqtt/home-assistant

### Features
* [DONE] NodeInfo packets to HASS sensors
* [DONE] group packets into HASS device for use in History and Automations
* [TODO] store POSITION packets
* [TODO] store TELEMETRY packets
* [TODO] store text messages

### Structure
* one Home assistant installation accessible by the Device,
* one Device running Meshtastic, with Uplink and Downlink enabled on 1 or more channels (usually the Primary),
* one MQTT broker, accessible by both the Home Assistant and Device.

### Setup
Refer to the guide here: https://meshtastic.org/docs/software/mqtt/home-assistant

Expanded with more detail below. 

#### Meshtastic Device 
1. Ensure your Meshtastic device is connected to your MQTT broker. These settings can be changed via Python CLI, Web UI, or Mobile App. 

Configuring Wifi

```
meshtastic
  --set network.wifi_enabled true
  --set network.wifi_ssid "my network"
  --set network.wifi_psk mypassword
```

Configure MQTT, uplink, downlink, JSON. 

Set the server address or the default will be used `mqtt.meshtastic.org`

```
meshtastic
  --set mqtt.enabled true
  --set mqtt.json_enabled true
  --set mqtt.address broker.myserver.net
  --set mqtt.username user1
  --set mqtt.password password
  --set mqtt.tls_enabled true
  --set mqtt.root mesh-topic-without-slashes
  --ch-set uplink_enabled true --ch-index 0
  --ch-set downlink_enabled true --ch-index 0
```
#### Home Assistant setup
1. Install and setup the MQTT integration. There are many instructions for this online.
1. Install and open the File Editor Add On: https://my.home-assistant.io/redirect/supervisor_addon/?addon=core_configurator
1. Open configuration.yaml and include the following line: `mqtt: !include mqtt.yaml`
1. Create a new text file called `mqtt.yaml` in the root directory of Home Assistant (the same folder as configuration.yaml).
1. Follow instructions at the top of the file `mqtt.yaml` in this repo as a template.
1. Copy modified template to `mqtt.yaml` on the HASS instance.
1. Navigate to Developer Tools, click CHECK CONFIGURATION
1. If Configuration passed, click ALL YAML CONFIGURATION.
1. Navigate to Settings -> Device and Services -> Devices.  Type in the Search box 'mesh' and you should see newly added sensors.

### Example

![image](https://github.com/tmarkson/HassMeshtasticMqtt/assets/896199/7eda4628-72c7-46e0-801d-bcd390874e5d)

![image](https://github.com/tmarkson/HassMeshtasticMqtt/assets/896199/d54c129d-2736-4d8c-87da-e35ea1b84f75)

