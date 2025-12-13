# IKEA BILRESA E2489 Matter Smart Button Blueprint

![BILRESA Matter Remote](bilresa-remote.jpg)

This blueprint provides automation for controlling the [IKEA BILRESA E2489 Matter Smart Button](https://www.ikea.com/us/en/p/bilresa-remote-control-white-smart-dual-button-80617876/) in Home Assistant. 

Options for use (tested with lights and scripts):

- Turn on/off lights
- Control the brightness
- Initiate scenes
- Start scripts

## Installation (3 options)

- Search for "IKEA BILRESA" in Settings > Automation & Secenes > Blueprints (tab) > "Discover more blueprints"
- Manually create and copy contents into `/blueprints/automation/censay/bilresa-remote.yaml`
- Import a blueprint from this address: < placeholder >

Restart Home Assistant or go to Devleoper Tools and check all yaml to reload your yaml files including the new blueprint.

## Usage

To use this blueprint, follow these steps:

1. Navigate to the "Automations" section in the Home Assistant UI.
2. Click on the "Blueprints" tab.
3. Search for the "IKEA BILRESA E2489 Matter Smart Button" blueprint.
4. Click on the "Add" button to add the blueprint to your automations.

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

- **Version 1.0.2**: Initial release.