# IKEA BILRESA E2489 Matter Smart Button - Blueprint

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fcensay%2Fhaos-blueprints%2Frefs%2Fheads%2Fmaster%2Fikea-bilresa-e2489-matter-smart-button%2Fikea-bilresa-e2489-matter-smart-button.yaml)

![BILRESA Matter Remote](https://github.com/censay/haos-blueprints/raw/master/ikea-bilresa-e2489-matter-smart-button/bilresa-remote.jpg)

This blueprint provides automation for controlling the [IKEA BILRESA E2489 Matter Smart Button](https://www.ikea.com/us/en/p/bilresa-remote-control-white-smart-dual-button-80617876/) in Home Assistant. 

Options for use (tested with lights and scripts):

- Turn on/off lights
- Control the brightness
- Initiate scenes
- Start scripts

## Installation (options)

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fcensay%2Fhaos-blueprints%2Frefs%2Fheads%2Fmaster%2Fikea-bilresa-e2489-matter-smart-button%2Fikea-bilresa-e2489-matter-smart-button.yaml)
- **OR** Search for "IKEA BILRESA" in Settings > Automation & Secenes > Blueprints (tab) > "Discover more blueprints"
- **OR** Manually copy [full yaml](#yaml) below to `/blueprints/automation/censay/bilresa-remote.yaml`
- **OR** Import a blueprint from this address: [github.com/censay/haos-blueprints](https://github.com/censay/haos-blueprints/blob/master/ikea-bilresa-e2489-matter-smart-button/ikea-bilresa-e2489-matter-smart-button.yaml)

Restart Home Assistant or go to Devleoper Tools and check all yaml to reload your yaml files including the new blueprint.

## Usage

To use this blueprint, follow these steps:

1. Navigate to the "Automations" section in the Home Assistant UI.
2. Click on " + Create automation" in the corner button.
3. Define how you want the buttons to work.
4. Enjoy!

### Inputs

The following inputs are required for this blueprint:

- **Button Type**: Select the type of button press (single, double, long press, etc.).
- **Action**: Select the action to perform when the button is pressed (turn on, turn off, change brightness, etc.).
- **Entity**: Select the entity to control (e.g., switch, light, camera toggle).

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
 - **Version 1.0.3**: Added [not_from/not_to](https://community.home-assistant.io/t/ikea-bilresa-matter-button-blueprint-for-ikea-matter-over-thread-button-actions-scripts-and-entities/962344/12) filters to prevent re-triggering on HA/Matter restarts ()
- **Version 1.0.2**: Initial release

## YAML
```
# ===================================================================
# IKEA BILRESA E2489 Dual Button
# Blueprint Template v1.0.3
#
# Internal Versioning:
#   schema_version: 1.0.3
#   last_updated: 2025-12-27
#
# Changelog:
#   v1.0.3: Added not_from/not_to filters to prevent re-triggering on HA/Matter restarts (https://community.home-assistant.io/t/ikea-bilresa-matter-button-blueprint-for-ikea-matter-over-thread-button-actions-scripts-and-entities/962344/12)
#   v1.0.2: Initial release
#
# Power-User Notes:
#   - This device exposes two event entities, one per physical button.
#   - You must select the correct event entity for Button 1 and Button 2.
#   - Each press updates the entity state (timestamp) and sets attributes.event_type.
# ===================================================================

blueprint:
  name: IKEA BILRESA E2489 Dual Button (Matter)
  author: censay
  description: >
    Full-featured automation for the IKEA BILRESA E2489 Matter dual-button
    remote. Supports single press, double press, and long press (on release)
    for both buttons. Uses event entities exposed by Home Assistant for
    Matter devices. Single-press actions are prioritized for reliability.
  domain: automation
  source_url: https://github.com/censay/haos-blueprints
  homeassistant:
    min_version: 2025.12.1

  input:
    target_device:
      name: BILRESA Button Device
      description: >
        Select the IKEA BILRESA E2489 matter device.
      selector:
        device:
          filter:
            - manufacturer: IKEA of Sweden

    button1_event:
      name: Button 1 – Event Entity
      description: >
        Select the event entity for Button 1 (for example:
        event.bilresa_dual_button_button_1_2).
      selector:
        entity:
          domain: event

    button2_event:
      name: Button 2 – Event Entity
      description: >
        Select the event entity for Button 2 (for example:
        event.bilresa_dual_button_button_2_2).
      selector:
        entity:
          domain: event

    # ---------------------------------------------------------------
    # BUTTON 1 ACTIONS
    # ---------------------------------------------------------------

    button1_single:
      name: Button 1 – Single Press
      description: Action for Button 1 single press (multi_press_1).
      default: []
      selector:
        action: {}

    button1_double:
      name: Button 1 – Double Press
      description: Action for Button 1 double press (multi_press_2).
      default: []
      selector:
        action: {}

    button1_long:
      name: Button 1 – Long Press (on release)
      description: Action for Button 1 long press completion (long_release).
      default: []
      selector:
        action: {}

    # ---------------------------------------------------------------
    # BUTTON 2 ACTIONS
    # ---------------------------------------------------------------

    button2_single:
      name: Button 2 – Single Press
      description: Action for Button 2 single press (multi_press_1).
      default: []
      selector:
        action: {}

    button2_double:
      name: Button 2 – Double Press
      description: Action for Button 2 double press (multi_press_2).
      default: []
      selector:
        action: {}

    button2_long:
      name: Button 2 – Long Press (on release)
      description: Action for Button 2 long press completion (long_release).
      default: []
      selector:
        action: {}

# ===================================================================
# AUTOMATION LOGIC
# ===================================================================

variables:
  button1_entity: !input button1_event
  button2_entity: !input button2_event

trigger:
  - platform: state
    id: button1
    entity_id: !input button1_event
    not_from: 'unavailable'
    not_to: 'unavailable'
  - platform: state
    id: button2
    entity_id: !input button2_event
    not_from: 'unavailable'
    not_to: 'unavailable'
  # Added not_from/not_to filters to prevent re-triggering on HA/Matter restarts; event entities use timestamp states

condition: []

action:
  - variables:
      press_type: "{{ trigger.to_state.attributes.event_type }}"
      trigger_id: "{{ trigger.id }}"

  - choose:

      # -------------------------------------------------------------
      # BUTTON 1
      # -------------------------------------------------------------

      - conditions:
          - condition: template
            value_template: >
              {{ trigger_id == 'button1' and press_type == 'multi_press_1' }}
        sequence: !input button1_single

      - conditions:
          - condition: template
            value_template: >
              {{ trigger_id == 'button1' and press_type == 'multi_press_2' }}
        sequence: !input button1_double

      - conditions:
          - condition: template
            value_template: >
              {{ trigger_id == 'button1' and press_type == 'long_release' }}
        sequence: !input button1_long

      # -------------------------------------------------------------
      # BUTTON 2
      # -------------------------------------------------------------

      - conditions:
          - condition: template
            value_template: >
              {{ trigger_id == 'button2' and press_type == 'multi_press_1' }}
        sequence: !input button2_single

      - conditions:
          - condition: template
            value_template: >
              {{ trigger_id == 'button2' and press_type == 'multi_press_2' }}
        sequence: !input button2_double

      - conditions:
          - condition: template
            value_template: >
              {{ trigger_id == 'button2' and press_type == 'long_release' }}
        sequence: !input button2_long

mode: restart
```