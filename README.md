# LizBall - ZMK Firmware Configuration

This repository contains the ZMK firmware configuration for the LizBall, a compact 3-key wireless trackball keyboard with a rotary encoder.

## Hardware Specifications

- **MCU**: Seeed Studio Xiao NRF52840
- **Optical Sensor**: PMW3610 (25mm trackball)
- **Keys**: 3 Kailh V2 Low Profile Switches
- **Rotary Encoder**: EC12
- **Form Factor**: Rectangle shape

## Building the Firmware

1. Clone this repository
2. Push to your own GitHub repository
3. GitHub Actions will automatically build the firmware
4. Download the firmware from the "Actions" tab

## Flashing the Firmware

1. Connect your Xiao BLE in bootloader mode (press reset button twice)
2. Copy the `.uf2` file to the USB drive that appears
3. The board will automatically restart with the new firmware

## Credits

- Based on the PMW3610 driver implementation from [inorichi](https://github.com/inorichi)
- Inspired by the [Nape trackball](https://men-bou.net/nape-trackball-buildguide/)