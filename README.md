# attribute-entity-row
Show entity attribute value(s) on entity rows in Home Assistant's Lovelace UI.

[![GH-release](https://img.shields.io/badge/version-1.1.0-red.svg?style=flat-square)](https://raw.githubusercontent.com/benct/lovelace-attribute-entity-row/master/attribute-entity-row.js)
[![GH-last-commit](https://img.shields.io/github/last-commit/benct/lovelace-attribute-entity-row.svg?style=flat-square)](https://github.com/benct/lovelace-attribute-entity-row/commits/master)
[![GH-code-size](https://img.shields.io/github/languages/code-size/benct/lovelace-attribute-entity-row.svg?style=flat-square)](https://github.com/benct/lovelace-attribute-entity-row)

## Setup

Add [attribute-entity-row.js](https://raw.githubusercontent.com/benct/lovelace-attribute-entity-row/master/attribute-entity-row.js) to your `<config>/www/` folder. Add the following to your `ui-lovelace.yaml` file:

```yaml
resources:
  - url: /local/attribute-entity-row.js?v=1.1.0
    type: js
```

### *(Optional)* Add to custom updater

1. Make sure you have the [custom_updater](https://github.com/custom-components/custom_updater) component installed and working.

2. Add a new reference under `card_urls` in your `custom_updater` configuration in `configuration.yaml`.

```yaml
custom_updater:
  card_urls:
    - https://raw.githubusercontent.com/benct/lovelace-attribute-entity-row/master/tracker.json
```

## Options

| Name | Type | Default | Description
| ---- | ---- | ------- | -----------
| type | string | **Required** | `custom:attribute-entity-row`
| entity | string | **Required** | `sensor.my_sensor`
| name | string | | Override entity name / friendly_name
| name_attribute | string | | Use an attribute as the entity name
| unit | string | | Override state unit_of_measurement
| toggle | bool | `false` | Display a toogle instead of state
| hide_state | bool | `false` | Hide the entity state
| primary | object | *see below* | Primary attribute object
| secondary | object | *see below* | Secondary attribute object

### Primary/secondary object

| Name | Type | Default | Description
| ---- | ---- | ------- | -----------
| key  | string | **Required** | A valid attribute key within the entity
| name | string | | Name / prefix for attribute
| unit | string | | Unit / postfix for attribute
| entity | string | | Use attribute from another entity

## Example

![attribute-entity-row](https://raw.githubusercontent.com/benct/lovelace-attribute-entity-row/master/example.png)

```yaml
type: entities
title: attribute-entity-row
show_header_toggle: false
entities:
  - type: section
    label: Primary attribute

  - entity: sensor.smoke_sensor_livingroom_temperature
    type: custom:attribute-entity-row
    primary:
      key: battery_level
      name: Battery
      unit: '%'
  - entity: light.living_room
    type: custom:attribute-entity-row
    primary:
      key: min_mireds
      name: 'Attribute:'
  - entity: media_player.spotify
    type: custom:attribute-entity-row
    primary:
      key: media_title

  - type: section
    label: Toggle

  - entity: light.living_room
    type: custom:attribute-entity-row
    name: Light with Toggle
    toggle: true
    primary:
      key: min_mireds
      name: Mireds
  - entity: switch.power_office_pc
    type: custom:attribute-entity-row
    toggle: true
    primary:
      key: friendly_name

  - type: section
    label: Customization

  - entity: sensor.smoke_sensor_livingroom_temperature
    type: custom:attribute-entity-row
    name: Custom Name
    primary:
      key: battery_level
      name: Battery
      unit: '%'
  - entity: sensor.motion_hall_temperature
    type: custom:attribute-entity-row
    name: Sensor
    primary:
      key: battery_level
      name: 'Value:'
      unit: units
  - entity: sensor.motion_hall_temperature
    type: custom:attribute-entity-row
    name: Sensor
    unit: Unit
    primary:
      key: battery_level
      name: Battery
      unit: '%'

  - type: section
    label: Secondary attribute

  - entity: sensor.magnet_door_main_temperature
    type: custom:attribute-entity-row
    secondary:
      key: battery_level
      name: Battery
      unit: '%'
  - entity: vacuum.xiaomi_vacuum_cleaner
    type: custom:attribute-entity-row
    primary:
      key: battery_level
      name: Battery
      unit: '%'
    secondary:
      key: status
  - entity: vacuum.xiaomi_vacuum_cleaner
    type: custom:attribute-entity-row
    primary:
      key: status
      name: 'Status:'
    secondary:
      key: battery_level
      name: Battery
      unit: '%'

  - type: section
    label: Alternative entity

  - entity: sensor.smoke_sensor_livingroom_temperature
    type: 'custom:attribute-entity-row'
    primary:
      key: fan_speed
      name: 'Vacuum fan:'
      entity: vacuum.xiaomi_vacuum_cleaner
  - entity: sensor.template_smoke_sensor_livingroom
    type: custom:attribute-entity-row
    primary:
      key: battery_level
      name: Other entity attribute
      entity: sensor.smoke_sensor_livingroom_temperature
    secondary:
      key: status
      name: Another entity -
      entity: vacuum.xiaomi_vacuum_cleaner

  - type: section
    label: Hide State

  - entity: sensor.smoke_sensor_livingroom_temperature
    type: custom:attribute-entity-row
    hide_state: true
    primary:
      key: battery_level
      name: Battery
      unit: '%'
  - entity: sensor.smoke_sensor_livingroom_temperature
    type: custom:attribute-entity-row
    name: With secondary
    hide_state: true
    primary:
      key: battery_level
      name: Battery
      unit: '%'
    secondary:
      key: status
      entity: vacuum.xiaomi_vacuum_cleaner
```

Partially based on @thomasloven's [slider-entity-row](https://github.com/thomasloven/lovelace-slider-entity-row) lovelace card.

## My cards

[xiaomi-vacuum-card](https://github.com/benct/lovelace-xiaomi-vacuum-card) | 
[github-entity-row](https://github.com/benct/lovelace-github-entity-row) | 
[multiple-entity-row](https://github.com/benct/lovelace-multiple-entity-row) | 
[attribute-entity-row](https://github.com/benct/lovelace-attribute-entity-row)

[![BMC](https://www.buymeacoffee.com/assets/img/custom_images/white_img.png)](https://www.buymeacoff.ee/benct)
