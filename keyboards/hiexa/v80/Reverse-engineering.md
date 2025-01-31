# Reverse engineering information

## MCU

![MCU PIN layout](https://i.imgur.com/eC3O0qr.png)

[MCU Datasheet](https://www.westberrytech.com/uploads/file/WB32FQ95xx/EN_DS1905020_WB32FQ95xC_V01.pdf)

### PINs not identified as of 2025-02-18

A5, A6, A7, A9, A11, A12, A13, A14, A15, B0, B1, B2, B6, B7, B8, B9, B10, B15, C10, C11, C14, C15, D0, D2

## MCU PINs for the Matrix

### Colunmns

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

[Flash chip datasheet](http://www.zettadevice.com/upload/file/20150821/DS_Zetta_25D40_20_RevA.pdf)

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

### MCU PINs

[tbc.]
