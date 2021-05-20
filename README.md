# ESPHome Quotes

![alt text](images/showoff.png "Show Off" )
Shows daily a new quote, or any text you would like to set via input helpers in Home Assistant. My version is battery powered (i should say underpowered).

## What you need

### Hardware

* esp32
* e-paper [display](https://www.waveshare.com/wiki/7.5inch_e-Paper_HAT)
* case
  * STL's [here](./stls/)
* battery

### Home Assistant

* Rest Sensor for a Quotes Provider, see my example with **They said So**. [sensors.yaml](./configs/sensors.yaml) in you configuration.yaml

  ```yaml
  sensor:
    - platform: rest
        name: "They said so"
        resource: "http://quotes.rest/qod.json"
        json_attributes_path: "$.contents.quotes[0]"
        value_template: "OK"
        json_attributes:
         - author
         - quote
        scan_interval: 43200

    - platform: template
        sensors:
        theysaidso_quote_body:
            friendly_name: "They said So Quote Body"
            value_template: '{{ states.sensor.they_said_so.attributes["quote"] }}'
        theysaidso_quote_author:
            friendly_name: "They said so Quote Author"
            value_template: '{{ states.sensor.they_said_so.attributes["author"] }}'
  ```

* Home Assistant Helpers
  * input_boolean.quote_darkmode
  * input_text.quote_body
  * input_text.quote_author (255 Max length)
* Automation
  * Update Automation [automation_update_text.yaml](./configs/automation_update_text.yaml)
* Lovelace Card
  * [card.yaml](./configs/card.yaml)

### ESPHome

* [esphome_quotes.yaml](./configs/esphome_quotes.yaml)
  * [font](https://fonts.google.com/specimen/Anonymous+Pro) goes into config/esphome/.esphome/fonts, I guess any monospace font will do

let me know, if something is missing.

## Known Issues

* [ ] Buggy lambda code
* [ ] Battery Consumption
* [ ] Battery metering is inaccurate with the voltage divider
