# IKEA KLIPPBOK Matter Leak Detector - Blueprint

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fcensay%2Fhaos-blueprints%2Frefs%2Fheads%2Fmaster%2Fikea-klippbok-leak-detector%2Fikea-klippbok-leak-detector.yaml)

![KLIPPBOK Leak Detector](https://github.com/censay/haos-blueprints/raw/master/ikea-klippbok-leak-detector/klippbok.png)

This blueprint provides leak detection and alerts for selected [IKEA KLIPPBOK Matter Leak Detector](https://www.ikea.com/us/en/p/klippbok-water-leak-sensor-smart-50617769/) -- it may work with other devices, this is designed to work with KLIPPBOK and matter.

Options for use:

- Monitors only the sensors you select.
- Alerts when any sensor becomes wet.
- Sends all-clear when all sensors are dry for 15 minutes.
- System notifications always work.
- Mobile notifications are optional (beta).

## Installation (options)

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fcensay%2Fhaos-blueprints%2Frefs%2Fheads%2Fmaster%2Fikea-klippbok-leak-detector%2Fikea-klippbok-leak-detector.yaml)
- **OR** Search for "IKEA KLIPPBOK Matter Leak Detector" in Settings > Automation & Scenes > Blueprints (tab) > "Discover more blueprints"
- **OR** Manually copy [full yaml](#yaml) below to `/blueprints/automation/censay/leak-alerts.yaml`
- **OR** Import a blueprint from this address: [github.com/censay/haos-blueprints](https://github.com/censay/haos-blueprints/blob/master/ikea-klippbok-leak-detector/ikea-klippbok-leak-detector.yaml)

Restart Home Assistant or go to Developer Tools and check all yaml to reload your yaml files including the new blueprint.

## Usage

To use this blueprint, follow these steps:

1. Navigate to the "Automations" section in the Home Assistant UI.
2. Click on " + Create automation" in the corner button.
3. Select the moisture sensors to monitor and choose if mobile notifications are enabled.
4. Enjoy!

### Inputs

The following inputs are required for this blueprint:

- **moisture_sensors**: Select the moisture sensors to monitor (binary sensors with device_class moisture).
- **notify_mobile**: Enable to send mobile notifications via notify.notify (optional, beta).

## Requirements

This blueprint is built from ["Triggering the holidays" 2025.12](https://www.home-assistant.io/blog/2025/12/03/release-202512/) guidance so is designed to work best with...

- Home Assistant version 2025.12.1 or later.

## License

This blueprint is licensed under the [MIT License](https://opensource.org/licenses/MIT).

## Contributing

Contributions are welcome! If you have any suggestions, improvements, or bug fixes, please submit a pull request or open an issue on this repository.

## Credits

This blueprint was created by [censay](https://github.com/censay).

## Changelog
- **Version 1.0.4**: Initial release with leak detection and all-clear notifications.

## YAML
```yaml
# ===================================================================
# 💧 Leak Alerts for Selected Sensors (Matter)
# Version: 1.0.4
#
# Watches ONLY the sensors you select.
# Alerts when any becomes wet.
# Sends all‑clear when all are dry for 15 minutes.
# System notifications always work.
# Mobile notifications are optional (beta).
# ===================================================================

blueprint:
  name: 💧 Leak Alerts for Selected Sensors (Matter)
  author: censay
  description: >
    Persistent notification moisture matter sensors, and sends an all‑clear
    when everything is dry for 15 minutes. System notifications always
    work. Mobile notifications are optional (beta).
  domain: automation
  homeassistant:
    min_version: 2025.12.1

  input:

    moisture_sensors:
      name: 💧 Leak Sensors to Monitor
      selector:
        entity:
          multiple: true
          domain: binary_sensor
          device_class: moisture

    notify_mobile:
      name: 📱 Send Mobile Notifications? (beta)
      description: >
        Sends alerts to notify.notify. If your mobile app is not set up,
        nothing breaks — mobile alerts are simply skipped.
      default: false
      selector:
        boolean: {}

# ===================================================================
# AUTOMATION LOGIC
# ===================================================================

trigger:
  - platform: state
    id: wet
    entity_id: !input moisture_sensors
    to: "on"

  - platform: state
    id: dry
    entity_id: !input moisture_sensors
    to: "off"
    for:
      minutes: 15

condition: []

action:

  - variables:
      moisture_sensors: !input moisture_sensors
      sensors: "{{ expand(moisture_sensors) }}"
      any_wet: >
        {{ sensors | selectattr('state','eq','on') | list | count > 0 }}
      all_dry: >
        {{ sensors | selectattr('state','eq','off') | list | count == (sensors | count) }}
      sensor_name: "{{ trigger.to_state.name }}"
      sensor_entity: "{{ trigger.entity_id }}"
      notify_mobile: !input notify_mobile

  - choose:

      # -----------------------------------------------------------
      # 💧 LEAK ALERT
      # -----------------------------------------------------------
      - conditions:
          - condition: template
            value_template: "{{ trigger.id == 'wet' }}"
        sequence:

          # 🏠 System notification (always works)
          - service: persistent_notification.create
            data:
              title: "💧 Leak Detected"
              message: "{{ sensor_name }} is WET ({{ sensor_entity }})."

          # 📱 Mobile notification (beta, safe)
          - choose:
              - conditions:
                  - condition: template
                    value_template: "{{ notify_mobile }}"
                sequence:
                  - service: notify.notify
                    data:
                      title: "💧 Leak Detected"
                      message: "{{ sensor_name }} is WET."
            default: []

      # -----------------------------------------------------------
      #  ☀️ ALL CLEAR
      # -----------------------------------------------------------
      - conditions:
          - condition: template
            value_template: "{{ trigger.id == 'dry' and all_dry }}"
        sequence:

          # 🏠 System notification (always works)
          - service: persistent_notification.create
            data:
              title: "☀️ Dry"
              message: "All sensors show dry."

          # 📱 Mobile notification (beta, safe)
          - choose:
              - conditions:
                  - condition: template
                    value_template: "{{ notify_mobile }}"
                sequence:
                  - service: notify.notify
                    data:
                      title: "☀️ Dry"
                      message: "All sensors show dry."
            default: []

mode: restart
```