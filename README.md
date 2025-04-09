# LizBall - ZMK Firmware Configuration

This repository contains the ZMK firmware configuration for the LizBall wireless trackball keyboard.

## Hardware Specifications

- **MCU**: Seeed Studio Xiao nRF52840
- **Optical Sensor**: PMW3610
- **Keys**: 3 Kailh V2 Low Profile Switches
- **Trackball**: 25mm
- **Rotary Encoder**: EC12
- **RGB Underglow**: 3x SK6812mini-E
- **Battery**: LiPo or AAA batteries
- **Shape**: Rectangle, designed to be placed above/below a low-profile keyboard

## Features

- Wireless Bluetooth connection with up to 5 profiles
- Trackball with adjustable sensitivity
- Multiple layers for different functions
- Scroll mode for the trackball
- Precision/snipe mode for detail work
- RGB underglow effects
- Rotary encoder for volume and other functions
- Low power consumption for extended battery life

## Directory Structure

```
zmk-config-lizball/
├── .github/
│   └── workflows/
│       └── build.yml
├── config/
│   ├── boards/
│   │   └── shields/
│   │       └── lizball/
│   │           ├── Kconfig.defconfig
│   │           ├── Kconfig.shield
│   │           ├── lizball.conf
│   │           ├── lizball.keymap
│   │           ├── lizball.overlay
│   │           └── lizball.zmk.yml
│   └── west.yml
└── build.yaml
```

## Building the Firmware

The firmware can be built automatically using GitHub Actions. Each commit to the repository will trigger a build.

To build locally:

1. Install the ZMK development environment following the [ZMK Documentation](https://zmk.dev/docs/development/setup)
2. Clone this repository
3. Run:

```bash
west init -l config
west update
west build -b seeeduino_xiao_ble -d build/lizball -- -DSHIELD=lizball
```

## Keyboard Layout and Layers

### Layer 0: Default
- Left Button: Right Click (hold for Mouse Layer)
- Middle Button: Middle Click
- Right Button: Left Click
- Rotary Encoder: Volume Up/Down

### Layer 1: Mouse Layer
- Activated automatically when trackball is moved or by holding left button
- Buttons function as normal mouse buttons
- Rotary Encoder: Page Up/Down

### Layer 2: Scroll Layer
- Activated by combo of middle + right buttons
- Trackball acts as a scroll wheel
- Rotary Encoder: Scroll Up/Down

### Layer 3: Precision/Snipe Layer
- Lower sensitivity for detailed work
- Rotary Encoder: Left/Right

### Layer 4: Bluetooth Layer
- Activated by combo of left + middle buttons
- Left Button: BT Profile 0
- Middle Button: BT Profile 1
- Right Button: BT Clear
- Rotary Encoder: Brightness Up/Down

### Layer 5: RGB Control Layer
- Activated by combo of all three buttons
- Left Button: RGB Toggle
- Middle Button: RGB Effect
- Right Button: RGB Brightness
- Rotary Encoder: RGB Brightness Up/Down

## Hardware Integration

### PMW3610 Trackball Wiring

The PMW3610 sensor requires specific wiring:

| PMW3610 Pin | Function | Connect To |
|-------------|----------|------------|
| 1           | SCLK     | Xiao D5 (SCL) |
| 2           | SDIO     | Xiao D4 (SDA) |
| 3           | GND      | GND |
| 4           | NC       | Not Connected |
| 5           | NCS      | Xiao D7 (RX) |
| 6           | VDDIO    | 3.3V |
| 7           | NRESET   | 3.3V through 2MΩ resistor |
| 8           | MOTION   | Xiao D6 (TX) |
| 9-16        | Other pins | See PMW3610 datasheet |

### Rotary Encoder Wiring

| EC12 Pin | Function | Connect To |
|----------|----------|------------|
| A        | A        | Xiao D3 (A3) with pull-up |
| C        | Common   | GND |
| B        | B        | Xiao D2 (A2) with pull-up |
| SW1      | Switch   | Xiao D1 (A1) |
| SW2      | Switch   | GND |

### RGB LEDs

The SK6812mini-E LEDs are connected in series to Xiao D0 (A0).

## Power Management Tips

- Enable deep sleep for longer battery life
- Set appropriate downshift times for the PMW3610 sensor
- Use the lowest RGB brightness needed for visual feedback
- Consider disabling RGB when operating on battery power

## License

This project is released under the MIT License.