# Reverse engineering information

## MCU

![MCU PIN layout](https://i.imgur.com/eC3O0qr.png)

[MCU Datasheet](https://www.westberrytech.com/uploads/file/WB32FQ95xx/EN_DS1905020_WB32FQ95xC_V01.pdf)

### PINs not identified as of 2025-02-18

A5, A6, A7, A9, A11, A12, A13, A14, A15, B0, B1, B2, B6, B7, B8, B9, B10, B15, C10, C11, C14, C15, D0, D2

## MCU PINs for the Matrix

### Columns

| **Keys**   | ESC |  F1 |  F2 |  F3 |  F4 |  F5 |  F6 |  F7 |  F8 |  F9 | F10 | F11 | F12 | Split BS | F13 | F14 | F15 | F16 |
| ---------- | --: | --: | --: | --: | --: | --: | --: | --: | --: | --: | --: | --: | --: | -------: | --: | --: | --: | --: |
| **Matrix** |   0 |   1 |   2 |   3 |   4 |   5 |   6 |   7 |   8 |   9 |  10 |  11 |  12 |       13 |  14 |  15 |  16 |  17 |
| **PINs**   |  C0 |  C1 |  C2 |  C3 |  D1 | B10 | B11 | B12 | B13 | B14 | A10 |  C6 |  C7 |       C8 |  C9 |  A8 |  C4 |  C5 |

### Rows

| **Keys**  | **PINs** |
| --------- | -------- |
| ESC       | A0       |
| GRAVE     | A1       |
| Tab       | A2       |
| Caps Lock | A3       |
| LShift    | A4       |
| Mods      | C13      |

## EEPROM flash chip

![Flash chip PIN layout]()

[Flash chip datasheet](https://www.zettadevice.com/upload/file/20150821/DS_Zetta_25D40_20_RevA.pdf)

| MCU | Flash | Flash Description  | MCU Alternate function                             |
| --: | :---- | ------------------ | -------------------------------------------------- |
| C12 | CS#   | Chip Select        | TIM4_ETR / UART3_CK                                |
|  B4 | DO    | Serial Data Out    | TIM3_CH1 / QSPI_MI_IO1 / **SPIS1_SO**              |
| VDD | WP#   | Write Protect      |                                                    |
| VSS | GND   | Ground             |                                                    |
| VDD | VCC   | Supply Voltage     |                                                    |
| VDD | HOLD# |                    |                                                    |
|  B3 | CLK   | Serial Clock Input | SWO / TIM2_CH2 / QSPI_SCK / **SPIS1_SCK**          |
|  B5 | DIO   | Serial Data I/O    | TIM3_CH2 / I2C1_SMBAI / QSPI_MO_IO0 / **SPIS1_SI** |

## QMK Configuration Notes

### USB

All WB32FQ95-based keyboards require `"suspend_wakeup_delay": 400` in the USB section of `keyboard.json`. Without this, the USB PHY may not stabilize after resume.

### EEPROM / Wear Leveling

QMK defaults to `wear_leveling` with the `efl` (embedded flash) backend on WB32FQ95. This uses the MCU's internal flash -- no external SPI flash needed for basic EEPROM functionality. The external Zetta 25D40 SPI flash chip can optionally be configured for `spi_flash`-backed wear leveling (more write cycles), but requires a complete configuration stack:

- `halconf.h`: `HAL_USE_SPI TRUE`, `SPI_USE_WAIT TRUE`, `SPI_SELECT_MODE SPI_SELECT_MODE_PAD`
- `mcuconf.h`: `WB32_SPI_USE_QSPI TRUE`
- `config.h`: SPI pin defines + `EXTERNAL_FLASH_SPI_SLAVE_SELECT_PIN`
- `keyboard.json`: `"eeprom": {"driver": "wear_leveling"}`, `"wear_leveling": {"driver": "spi_flash", ...}`

### SPI / HAL Warning

Enabling SPI at the ChibiOS HAL level (`HAL_USE_SPI`, `WB32_SPI_USE_QSPI`) without a corresponding QMK feature that uses SPI (e.g. `wear_leveling` with `spi_flash` driver) can cause the firmware to hang at startup -- before USB even initializes. The keyboard will not enumerate as a USB device and Bootmagic reset will not work. Always ensure HAL-level peripheral configuration matches the QMK feature configuration.
