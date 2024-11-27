# arduino-power
Notes on power supply circuits for Arduinos, Raspberry Pis, ESP32s, and other 5V/3.3V devices



| Image | Description | Chipset | Input | Output | Max Current | Switching Frequency |  Pot. Adj. | Fixed Adj. | PCB Mountable | Notes | Link |
| ----- | ----------- | ------- |------ |------- |------------ | ------------------- | ---------- | ---------- | ------------- | ----- | ---- |
| <img src="https://github.com/playfultechnology/arduino-power/blob/main/images/CA1235.png" /> | [CA1235 module](https://www.aliexpress.com/item/1005005231661753.html) | [MP1495](https://www.monolithicpower.com/en/mp1495.html) | 5-16V | 1.25-5V | 3A | 500kHz | :white_check_mark:| :white_check_mark: | Adjustable voltage output selectable by pot or solder joints. Can't be PCB mounted. | https://www.aliexpress.com/item/1005005231661753.html |
| <img src="https://github.com/playfultechnology/arduino-power/blob/main/images/Mini.png" />  | "Mini" | Marked as "DKGAA" | 12-24V* | 1.8-12V | 3A | 500kHz | -------------- | -------------- | Adjustable (need knife to break trace). Amazon reviews say not to exceed 15V input  | https://www.aliexpress.com/item/4000016739581.html |
| <img src="https://github.com/playfultechnology/arduino-power/blob/main/images/MP1584EN.png" />| [MP1584EN](https://www.amazon.co.uk/DollaTek-MP1584EN-Step-Down-Adjustable-Converter/dp/B07DJ5HZ7G) | [MP1584](https://www.monolithicpower.com/en/mp1584.html) |  4.5-28V | 0.8-20V | 3A | 1.5MHz | :white_check_mark: | :white_large_square: | Pot adjustment _only_ |  |
| <img src="https://github.com/playfultechnology/arduino-power/blob/main/images/QSKJ.jpg" />| [QSKJ "Fine"](https://www.aliexpress.com/item/32815170131.html) | [MP2315](https://www.openhacks.com/uploadsproductos/datasheet_77.pdf) | 5-16V | 1.25-5V | 3A |500Khz | | -------------- | -------------- |  |
| | [XL1509](https://www.lcsc.com/datasheet/lcsc_datasheet_2304140030_XLSEMI-XL1509-5-0E1_C61063.pdf) |  5-16V | 1.25-5V | 3A | 150kHz |||


NOTE: Neither 1584 or 1495 are recommended for new designs. Instead MP2338 recommended instead.

MP1584 not recommnded for new designs [MP2338](https://www.monolithicpower.com/en/mp2338.html) recommended instead.
MP2315 not recommended for new designs. [MP2393](https://www.monolithicpower.com/en/mp2393.html) suggested alternative instead.

Higher switching frequency will mean less ripple on the output (more accurate voltage/current) but causes more overhead due to switching, which reduces the efficiency a bit.

Also see https://blog.yavilevich.com/2017/03/efficient-dc-12v-to-5v-conversion-for-low-power-electronics-evaluation-of-six-modules/
