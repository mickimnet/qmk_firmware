# Hiexa V80 (without wireless support)

![Hiexa V80 PCB (front)](https://i.imgur.com/cPmihKc.jpeg)
![Hiexa V80 PCB (back)](https://i.imgur.com/BD8wm9Z.jpeg)

A modern TKL / 80% multi-layout keyboard with 100% fully CNC finish, customized ball catch structure, magnetic connector assembly process and a dot-matrix circular LED light above the arrow keys. It supports PCB gasket, plate gasket, and top mount.

* Keyboard Maintainer: [Mick Hohmann](https://github.com/mickimnet)
* Hardware Supported: Westberry WB32FQ95
* Hardware Availability: [MonacoKeys](https://monacokeys.de/) (limited in stock)

Make example for this keyboard (after setting up your build environment):

    make hiexa/v80:default

Flashing example for this keyboard:

    make hiexa/v80:default:flash

See the [build environment setup](https://docs.qmk.fm/#/getting_started_build_tools) and the [make instructions](https://docs.qmk.fm/#/getting_started_make_guide) for more information. Brand new to QMK? Start with our [Complete Newbs Guide](https://docs.qmk.fm/#/newbs).

## Bootloader

Enter the bootloader in 3 ways:

* **Bootmagic reset**: Hold down the key at (0,0) in the matrix (usually the top left key or Escape) and plug in the keyboard
* **Physical reset button**: Briefly press the button on the back of the PCB - some may have pads you must short instead
* **Keycode in layout**: Press the key mapped to `QK_BOOT` if it is available
