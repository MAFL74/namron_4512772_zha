
# Namron 4512772 Zigbee 8-Button Switch – ZHA Custom Quirk & Home Assistant Blueprint

## Overview

This repository contains a **custom ZHA quirk** and a **Home Assistant automation blueprint** for the Namron 8-button Zigbee switch (model 4512772).  
The combination enables full support for all short and long button presses, giving you precise control over automations in Home Assistant.

---

## Why Use This Quirk?

The Namron 4512772 is not fully supported out-of-the-box in ZHA/Home Assistant.  
Only the "Identify" button typically works, while the rest of the buttons do not appear as triggers in the Home Assistant automation UI.

By installing this custom quirk, the switch exposes *all* its buttons as device triggers, supporting:

- **Short press (on/off)**
- **Long hold (dimming up/down)**
- **Long release**

The included **automation blueprint** makes it easy to use these triggers to control anything you want – lights, scenes, scripts, etc.

---

## Features

- Full support for 8 (or 2/4, depending on your configuration) individual channels.
- Each channel supports:
  - Short press "on" / "off"
  - Long hold (on) for dimming
  - Long release (on) for stopping dimming
- Automations are easy to set up thanks to the included Home Assistant blueprint.

---

## Installation

### 1. Copy the Quirk

1. Place the custom quirk Python file (`namron_4512772_zha.py`) in your Home Assistant instance at:

   ```
   /config/custom_zha_quirks/
   ```

   *(If this folder doesn't exist, create it)*

2. In `configuration.yaml`, make sure you point to your custom quirks folder:

   ```yaml
   zha:
     custom_quirks_path: /config/custom_zha_quirks
   ```

3. **Restart Home Assistant** for the quirk to take effect.

### 2. Pair the Device

- Remove and re-add the Namron 4512772 switch via ZHA.
- All button actions will now appear as device triggers!

### 3. Import the Blueprint

1. In Home Assistant, go to **Settings > Automations & Scenes > Blueprints**.
2. Click **Import Blueprint** and paste the YAML from [`blueprint.yaml`](namron_4512772_blueprint.yaml) in this repo.
3. Save the blueprint.

### 4. Create Automations

- Use the blueprint to create automations.
- Select your Namron switch as the device, and assign actions to any button/trigger you want (short press, long hold, etc).

---

## Usage

**What the quirk does:**

- Registers all buttons and actions of the Namron 4512772 as ZHA device automations.
- Triggers are exposed with clear names:
  - `short_press` / `long_hold` / `long_release`
  - `channel_1_on`, `channel_1_off`, ... up to `channel_4_on`, `channel_4_off`

**What the blueprint does:**

- Lets you create automations based on any button and press type.
- All channels and actions are mapped to easily selectable actions in the Home Assistant UI.
- You don't need to write complex automations – just select your actions per button.

---

## Example

**Short press on channel 1 "on" → turn on a light:**

```yaml
trigger:
  - platform: device
    type: short_press
    subtype: channel_1_on
    device_id: <your device id>
```

**Long hold on channel 2 "on" → start dimming:**

```yaml
trigger:
  - platform: device
    type: long_hold
    subtype: channel_2_on
    device_id: <your device id>
```

**(The blueprint makes all of this point-and-click!)**

---

## Troubleshooting

- If triggers do not appear, ensure:
  - The quirk file is correctly installed and Home Assistant has been restarted.
  - The device has been re-paired after the quirk was added.
  - The blueprint matches the trigger format (`short_press`, `channel_1_on`, etc).
- If you still see only "Identify" or missing buttons, check that you have no conflicting quirks and that ZHA is using the custom quirk.

---

## Credits

- Based on community discussions and testing in Home Assistant with ZHA.
- Special thanks to everyone providing feedback and code!

Developed and maintained by MAFL74  
[GitHub profile](https://github.com/MAFL74)  
Feel free to open an issue or pull request!
