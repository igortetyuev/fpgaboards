# Logisim-evolution board definitions for inexpensive FPGA boards

Board description files for [Logisim-evolution](https://github.com/logisim-evolution/logisim-evolution)'s
**FPGA Commander**. They let you map a circuit drawn in Logisim onto the LEDs, buttons and I/O
headers of cheap FPGA/CPLD boards from AliExpress, Amazon and eBay, then synthesize it and
download it to real hardware.

Each `.xml` file contains the FPGA part information, the on-board clock, the pin mapping of the
user LEDs, buttons and header pins, and an embedded photo of the board that is shown in the
FPGA Commander's mapping dialog.

## Boards

| File | Board | Vendor / family | FPGA chip | Package | Clock | LEDs | Buttons | Header I/O pins |
|------|-------|-----------------|-----------|---------|-------|------|---------|-----------------|
| [`A7-LITE.xml`](A7-LITE.xml) | MicroPhase A7-Lite | AMD/Xilinx Artix-7 | XC7A35T-2 | FGG484 | 50 MHz (J19) | 2 | 3 | 88 |
| [`XS616N.xml`](XS616N.xml) | Spartan-6 XC6SLX16 core board | AMD/Xilinx Spartan-6 | XC6SLX16-2 | FTG256 | 50 MHz (T7) | 4 | 3 | 52 |
| [`XS625N.xml`](XS625N.xml) | Spartan-6 XC6SLX25 core board | AMD/Xilinx Spartan-6 | XC6SLX25-2 | FTG256 | 50 MHz (T7) | 4 | 3 | 52 |
| [`EP4CE6E22_MiniBoard.xml`](EP4CE6E22_MiniBoard.xml) | Cyclone IV EP4CE6 mini board | Intel/Altera Cyclone IV E | EP4CE6E22C8N | EQFP144 | 50 MHz (PIN_24) | 5 | 4 | 70 |
| [`EPM240_MAXII.xml`](EPM240_MAXII.xml) | MAX II EPM240 CPLD minimum system board | Intel/Altera MAX II | EPM240T100C5N | TQFP100 | 50 MHz (PIN_12) | 1 | 1 | 76 |

All LEDs and buttons on these boards are active-low.

### MicroPhase A7-Lite (Artix-7)

A small Artix-7 board with DDR3, Gigabit Ethernet, HDMI out, USB-JTAG and USB-UART. It is sold with
XC7A35T, XC7A100T and XC7A200T chips; this definition is for the **XC7A35T** version. For the other
versions, change `Part` in `FPGAInformation`. The configuration flash is an IS25LP128F.

- [MicroPhase A7-Lite reference manual](https://fpga-docs.microphase.cn/en/latest/DEV_BOARD/A7-LITE/A7-Lite_Reference_Manual.html)
- [Product page (OpenSourceSDRLab)](https://opensourcesdrlab.com/products/fpga-development-board-core-board-xilinx-artix-7-xc7a35t-100t-a7-lite)
- Example projects: [LED blink](https://github.com/kisek/fpga_a7-lite_led), [HDMI output](https://github.com/kisek/fpga_a7-lite_hdmi)

Toolchain: AMD Vivado.

The third button is the board's reset key, which is not connected to a user FPGA pin (`RESET_UNMAPPED`).

### Spartan-6 XC6SLX16 / XC6SLX25 core boards (XS616N / XS625N)

A common Chinese Spartan-6 core board with SDRAM, a W25Q16 SPI flash, 4 LEDs (D1–D4), 2 user keys
(K1, K2), a RST key and a 6-pin JTAG header. The two files use the same pinout and differ only in the
FPGA part (XC6SLX16 or XC6SLX25).

- [AliExpress: Spartan-6 XC6SLX16 core board](https://www.aliexpress.com/item/32801899786.html)
- [Art of Circuits: Spartan-6 core board, XC6SLX16-FTG256](https://artofcircuits.com/product/spartan-6-fpga-core-board-with-256mbit-sdram-xc6slx16-ftg256)

Toolchain: Xilinx ISE 14.7. Vivado does not support Spartan-6.

### Cyclone IV EP4CE6E22C8N mini board

A low-cost Cyclone IV board with 50 MHz and 27 MHz oscillators, a CH340 USB-UART, W25Q flash,
5 LEDs, 4 user buttons and a reset button. The UART is on PIN_10 (FPGA TX) and PIN_23 (FPGA RX).
The reset button (PIN_88) is left out of the definition on purpose.

- [Getting started with the EP4CE6E22C8N board (IoT Engineering Education, KMUTNB)](https://iot-kmutnb.github.io/blogs/fpga/fpga_ep4ce6_board/)
- [Amazon: EP4CE6E22C8N development board with CH340](https://www.amazon.com/HanOaki-EP4CE6E22C8N-Development-Dual-Crystal-Oscillators/dp/B0GF28QSMR)
- [FPGAkey: board introduction and pinout](https://www.fpgakey.com/technology/details/intel-altera-cyclone-iv-fpga-ep4ce6e22c8n-development-board-introduce-including-datasheet-and-pinout)

Toolchain: Intel Quartus Prime Lite 20.1 or older. Newer releases no longer support Cyclone IV.

### MAX II EPM240 CPLD minimum system board

The classic blue/red EPM240T100C5N breakout with four 2×10 headers, a 50 MHz oscillator and a
JTAG port. Header pins are labelled with the chip pin number, which matches the silkscreen.

- [Amazon: MAX II EPM240 minimum system core board](https://www.amazon.com/Electronic-Components-EPM240T100C5N-Minimum-Development/dp/B08B855CNB)
- [diymore: MAX II EPM240 CPLD development board](https://www.diymore.cc/products/max-ii-epm240-cpld-development-board-experiment-board-learning-breadboard-module)
- [Aideepen: 5V MAX II EPM240 core board](https://www.aideepen.com/products/5v-max-ii-epm240-cpld-minimum-system-core-board-development-board-module)

Toolchain: Intel Quartus Prime Lite.

> **Note:** the FPGA pin of the tactile button J6 is not documented for this board, so it is set to
> `PIN_unassigned`. If you know the pin, replace it in `EPM240_MAXII.xml`.

## Usage

1. Install [Logisim-evolution](https://github.com/logisim-evolution/logisim-evolution/releases)
   and the vendor toolchain for your board (Vivado, ISE or Quartus).
2. Open your circuit and select **FPGA → Synthesize & Download** to open the FPGA Commander.
3. In the board selection, pick **Other** and load the board's `.xml` file from this repository.
4. Set the toolchain paths under **Settings**, map your circuit's inputs and outputs to the
   components on the board picture, then run **Execute**.

## Contributing

Corrections and new boards are welcome. If you find a wrong pin, please open an issue or a pull
request and mention where the correct pinout comes from (a schematic, the vendor manual or a test
on real hardware).

## License

[MIT](LICENSE)
