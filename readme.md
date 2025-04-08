# Lizball - ZMK Firmware Configuration

This repository contains the ZMK firmware configuration for a custom 4-key wireless keyboard with a 25mm trackball.

## Hardware Specifications

- **MCU**: Xiao NRF52840
- **Optical Sensor**: PMW3610
- **Keys**: 4 Kailh Low Profile Switches with 1.25u keycaps
- **Trackball**: 25mm
- **Battery**: 250mAh LiPo
- **Shape**: Rectangle

## Getting Started

### Prerequisites

1. Install the ZMK development environment following the [ZMK Documentation](https://zmk.dev/docs/development/setup)
2. Clone this repository

### Building the Firmware

1. Make sure you've updated the `west.yml` file with your trackball-supporting ZMK fork URL
2. Run the following commands:

```bash
west init -l config
west update
west build -b xiao_nrf52840 -d build/lizball -- -DSHIELD=lizball
```

The compiled firmware will be located at `build/lizball/zephyr/zmk.uf2`.

### Building with GitHub Actions

Once you push this repository to GitHub, the GitHub Actions workflow will automatically build the firmware for you. You can download the firmware from the "Actions" tab after the build completes.

### Flashing the Firmware

1. Connect your board in bootloader mode
2. Copy the `zmk.uf2` file to the USB drive that appears

## Customizing the Keymap

The keymap is defined in `config/boards/shields/lizball/lizball.keymap`. Edit this file to customize your key layout and trackball behavior.

## Important Notes

### PMW3610 Implementation

The PMW3610 sensor currently requires custom implementation in ZMK. You'll need to:

1. Fork the ZMK repository
2. Add PMW3610 driver support (based on existing sensor drivers like PMW3360)
3. Update the `west.yml` to point to your fork

### Battery Configuration

The battery configuration is set up for a 250mAh LiPo battery. Adjust the voltage divider values in the device tree if your battery monitoring circuit differs.

### Power Management

This keyboard uses the ZMK sleep functionality to conserve battery power. The trackball sensor has custom power management to further extend battery life.

## Troubleshooting

- If you encounter issues with the trackball not responding, check the SPI pin configurations in the device tree overlay.
- For battery life issues, review the power management settings in the `lizball.conf` file.
- For Bluetooth connectivity problems, try adjusting the transmit power settings.

## Contributing

Contributions to improve this configuration are welcome! Feel free to submit pull requests with enhancements.
