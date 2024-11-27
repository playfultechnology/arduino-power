# arduino-power
Notes on power supply circuits for Arduinos, Raspberry Pis, ESP32s, and other 5V/3.3V devices


The following table compares various small DC-DC buck convertor modules commonly found on Amazon, AliExpress etc.

| Image | Description | Chipset | Input | Output | Max Current | Switching Frequency[^1] |  Pot. Adj. | Fixed Adj. | Notes |
| ----- | ----------- | ------- |------ |------- |------------ | ------------------- | ---------- | ---------- | ----- |
| <img src="https://github.com/playfultechnology/arduino-power/blob/main/images/CA1235.png" /> | [CA1235 module](https://www.aliexpress.com/item/1005005231661753.html) | [MP1495](https://www.monolithicpower.com/en/mp1495.html) | 5-16V | 1.25-5V | 3A | 500kHz | :white_check_mark:| :white_check_mark: | Adjustable voltage output selectable by pot or solder joints. Large holes designed for wire-to-board mean this can't easily be PCB mounted. |
| <img src="https://github.com/playfultechnology/arduino-power/blob/main/images/Mini.png" />  | ["Mini"](https://www.aliexpress.com/item/4000016739581.html) | Marked as "DKGAA" | 12-24V* | 1.8-12V | 3A | 500kHz |  :white_check_mark: | :white_check_mark: | Adjustable (need knife to break trace). Amazon reviews say not to exceed 15V input  | 
| <img src="https://github.com/playfultechnology/arduino-power/blob/main/images/MP1584EN.png" />| [MP1584EN](https://www.amazon.co.uk/DollaTek-MP1584EN-Step-Down-Adjustable-Converter/dp/B07DJ5HZ7G) | [MP1584](https://www.monolithicpower.com/en/mp1584.html) |  4.5-28V | 0.8-20V | 3A | 1.5MHz | :white_check_mark: | :white_large_square: | Pot adjustment _only_ | 
| <img src="https://github.com/playfultechnology/arduino-power/blob/main/images/QSKJ.jpg" />| [QSKJ "Fine"](https://www.aliexpress.com/item/32815170131.html) | [MP2315](https://www.openhacks.com/uploadsproductos/datasheet_77.pdf) | 6.5-24V | 5V | 3A | 500Khz |  :white_large_square:| :white_large_square: | Output is only via a USB socket |

[^1]: Higher switching frequency will mean less ripple on the output (more accurate voltage/current) but causes more overhead due to switching, which reduces the efficiency somewhat.

NOTE: These modules are typically based on somewhat old Monolithic Power Systems ICs which are not recommended for new designs.
 - MP1495 (used in "CA1235") and MP1584 are not recommended for new designs [MP2338](https://www.monolithicpower.com/en/mp2338.html) recommended instead.
 - MP2315 (used in "QSKJ Fine") not recommended for new designs. [MP2393](https://www.monolithicpower.com/en/mp2393.html) suggested alternative instead.

Additionally, the QSKJ is not usable due ot only having a USB interface, and CA1235 not usable in a custom PCB design due to its non-standard pin diameter. 
Which leaves "Mini" as the only useful choice from this list, but there is zero available documentation about the "DKGAA" chip it uses.

So, one alternative is to design a custom power subsystem....

Chipset | Input | Output | Max Current | Switching Frequency | Notes |
------- |------ |------- |------------ | ------------------- | ----- |
| [XL1509](https://www.lcsc.com/datasheet/lcsc_datasheet_2304140030_XLSEMI-XL1509-5-0E1_C61063.pdf) | 5-16V | 1.25-5V | 2A | 150kHz | Used in Kincony power supply circuitry with relatively few additional components: https://www.kincony.com/kc868-a4-hardware-design-details.html|



Also see https://blog.yavilevich.com/2017/03/efficient-dc-12v-to-5v-conversion-for-low-power-electronics-evaluation-of-six-modules/
