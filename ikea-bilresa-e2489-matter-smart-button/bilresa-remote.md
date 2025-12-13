# IKEA BILRESA E2489 Matter Smart Button Blueprint

This blueprint provides automation for controlling the IKEA BILRESA E2489 Matter Smart Button in Home Assistant. It includes the following automation scenarios:

- Turn on/off lights
- Control the brightness
- Initiate scenes
- Start scripts

## Installation

1. Clone this repository to your Home Assistant configuration directory.
2. Copy the `bilresa-remote.yaml` blueprint file to the `blueprints` directory.
3. Restart Home Assistant to load the new blueprint.

## Usage

To use this blueprint, follow these steps:

1. Navigate to the "Automations" section in the Home Assistant UI.
2. Click on the "Blueprints" tab.
3. Search for the "IKEA BILRESA E2489 Matter Smart Button" blueprint.
4. Click on the "Add" button to add the blueprint to your automations.

## Inputs

The following inputs are required for this blueprint:

- **Button Type**: Select the type of button press (single, double, long press, etc.).
- **Action**: Select the action to perform when the button is pressed (turn on, turn off, change brightness, etc.).
- **Entity**: Select the entity to control (e.g., switch.bilresa_remote).

## Example Automations

Here are some example automations you can create using this blueprint:

- Turn on the Matter Smart Button when it is pressed once:
  - Button Type: Single Press
  - Action: Turn On
  - Entity: switch.bilresa_remote

- Change the color of the Matter Smart Button when it is pressed twice:
  - Button Type: Double Press
  - Action: Change Color
  - Entity: switch.bilresa_remote

## Requirements

This blueprint requires the following:

- Home Assistant version 2022.12 or later.
- The `ikea_tradfri` integration configured and enabled.
- The `switch.bilresa_remote` entity available in your Home Assistant configuration.

## License

This blueprint is licensed under the [MIT License](https://opensource.org/licenses/MIT).

## Contributing

Contributions are welcome! If you have any suggestions, improvements, or bug fixes, please submit a pull request or open an issue on this repository.

## Credits

This blueprint was created by [censay](https://github.com/censay).

## Changelog

- **Version 1.0.2**: Initial release.