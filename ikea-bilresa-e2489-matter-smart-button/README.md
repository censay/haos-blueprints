# IKEA BILRESA E2489 Matter Smart Button Blueprint

## Product Information

**Product Name:** BILRESA Remote control - white smart/dual button  
**Article Number:** 806.178.76  
**Price:** $5.99 USD (as of December 12, 2025)  
**Product Link:** [IKEA BILRESA Product Page](https://www.ikea.com/us/en/p/bilresa-remote-control-white-smart-dual-button-80617876/)

### Description
This remote control with dual buttons makes it easier to operate your smart products – helping you to make life at home smoother, more comfortable and safer.

Use to turn smart products on/off, dim and change the color of light sources, or operate a group or preset scenes.

This smart product uses the universal standard Matter, making it easy to install, operate and add to DIRIGERA hub and to other well-known systems.

Smart bulbs, sensors and remote controls from IKEA work together - across generations. Mix, expand and control your smart home your way.

### Features
- Dual button remote control
- Matter-compatible for interoperability with various smart home systems (Amazon, Apple, Google, Homey, Samsung)
- Supports on/off, dimming, color changing, and scene/group control
- Designed by W Braasch/M Arvonen

### Specifications
- **Dimensions:** Height: 1 ¼ ", Length: 3 ", Width: 1 "
- **Weight:** 2 oz
- **Material:** ABS plastic
- **Batteries:** Sold separately; recommended 2 x LADDA rechargeable batteries HR03 AAA 1.2V

### Images
![BILRESA Remote Control](bilresa-remote-control.jpg)

## Blueprint Details

This folder contains the Home Assistant blueprint for automating the IKEA BILRESA E2489 Matter smart button.

### Files
- `ikea-bilresa-e2489-matter-smart-button.yaml` - The blueprint YAML file
- `bilresa-remote-control.jpg` - Product image
- `README.md` - This file

### Installation
1. Download the `ikea-bilresa-e2489-matter-smart-button.yaml` file.
2. In Home Assistant, go to Settings > Automations & Scenes > Blueprints > Import Blueprint.
3. Paste the YAML content or upload the file.
4. Ensure your Home Assistant version is 2024.12.0 or higher.

### Configuration
- **Button Entity**: Select the event entity for your IKEA button.
- **Action on Short Press**: Choose the action to trigger on short press.
- **Target Area for Short Press**: Select the area for the short press action.
- **Enable Notifications for Short Press**: Toggle to send notifications on short press.
- **Action on Long Press**: Choose the action to trigger on long press.
- **Target Area for Long Press**: Select the area for the long press action.
- **Enable Notifications for Long Press**: Toggle to send notifications on long press.

### Example Usage
```yaml
blueprint: censay/haos-blueprints/ikea-bilresa-e2489-matter-smart-button
input:
  button_entity: event.ikea_button_press
  action_on_short_press:
    service: light.turn_on
    target:
      area_id: living_room
  target_area_short_press: living_room
  enable_notifications_short_press: true
  action_on_long_press:
    service: light.turn_off
    target:
      area_id: living_room
  target_area_long_press: living_room
  enable_notifications_long_press: false
```

### Changelog
- v1.0.0: Initial release with basic press support.
- v1.1.0: Added short and long press differentiation.

### Support
For issues or contributions, visit the [GitHub Repo](https://github.com/censay/haos-blueprints).