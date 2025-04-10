# LizBall - ZMK Firmware Configuration

This repository contains the ZMK firmware configuration for the LizBall, a custom 3-key wireless trackball keyboard with a rotary encoder.

## Hardware Specifications

- **MCU**: Seeed Studio Xiao NRF52840
- **Optical Sensor**: PMW3610 (25mm trackball)
- **Keys**: 3 Kailh V2 Low Profile Switches (1.25u keycaps)
- **Rotary Encoder**: EC12 with push button
- **RGB Underglow**: 3x SK6812mini-E LEDs
- **Battery**: LiPo or AAA size
- **Form Factor**: Rectangle shape, designed to be placed above or below a low-profile keyboard

## Features

- Wireless Bluetooth operation
- Mouse control via 25mm trackball
- Multiple layers accessible via combos and hold actions
- RGB underglow effects
- Rotary encoder for volume control and more
- Battery-saving power management
- PMW3610 Smart Algorithm for improved tracking

## Building the Firmware

### Prerequisites

1. A GitHub account
2. This repository forked to your GitHub account

### Building with GitHub Actions (Recommended)

1. Push any changes to your fork
2. GitHub Actions will automatically build the firmware
3. Download the firmware from the "Actions" tab after the build completes

### Building Locally

If you want to build the firmware locally:

1. Follow the ZMK [development setup guide](https://zmk.dev/docs/development/setup)
2. Clone this repository
3. Run the following commands:

```bash
west init -l config
west update
west build -b seeeduino_xiao_ble -d build/lizball -- -DSHIELD=lizball
```

4. The built firmware will be at `build/lizball/zephyr/zmk.uf2`

## Flashing the Firmware

1. Connect your Xiao BLE in bootloader mode (press reset button twice)
2. Copy the `zmk.uf2` file to the USB drive that appears
3. The keyboard will automatically restart with the new firmware

## Keyboard Layout

The LizBall has a simple 3-key layout with a rotary encoder and uses a PMW3610 trackball for mouse control:

```
[EC12 Encoder] [1.25u] [25mm Trackball] [1.25u] [1.25u]
```

### Default Layer Mapping

- **Left Button**: Middle-click (hold for Layer 4 - BT controls)
- **Middle Button**: Right-click
- **Right Button**: Left-click (hold for Layer 3 - Snipe mode)
- **Encoder Press**: Toggle Layer 2 (Scroll mode)
- **Encoder Rotation**: Volume up/down by default

### Layer Functionality

- **Layer 1 (Mouse)**: Automatically activated when trackball is moved
- **Layer 2 (Scroll)**: Trackball controls scrolling
- **Layer 3 (Snipe)**: Precision/slow trackball movement
- **Layer 4 (Bluetooth)**: Bluetooth profile switching
- **Layer 5 (RGB)**: RGB underglow controls

## Customizing

### Keymap

Edit the `config/boards/shields/lizball/lizball.keymap` file to change the key mappings and layer functions.

### Hardware Configuration

If you modify the hardware design, update the pin assignments in `config/boards/shields/lizball/lizball.overlay`.

### Settings

Edit `config/boards/shields/lizball/lizball.conf` to adjust trackball sensitivity, RGB settings, and power management.

## Troubleshooting

- If the trackball doesn't respond, check SPI connections and ensure the PMW3610 is correctly wired
- For battery life issues, adjust sleep settings in the configuration
- For Bluetooth problems, try clearing the bond using the BT_CLR key combo

## Credits

- Based on the PMW3610 driver implementation from [menbou0202](https://github.com/menbou0202/zmk-pmw3610-driver)
- Inspired by the [Nape trackball](https://men-bou.net/nape-trackball-buildguide/)