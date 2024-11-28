# arduino-power
Notes on power supply circuits for Arduinos, Raspberry Pis, ESP32s, and other 5V/3.3V devices


The following table compares various small DC-DC buck convertor modules commonly found on Amazon, AliExpress etc.

| Image | Description | Chipset | Input | Output | Max Current | Switching Frequency[^1] |  Pot. Adj. | Fixed Adj. | Notes |
| ----- | ----------- | ------- |------ |------- |------------ | ------------------- | ---------- | ---------- | ----- |
| <img src="https://github.com/playfultechnology/arduino-power/blob/main/images/CA1235.png" /> | [CA1235 module](https://www.aliexpress.com/item/1005005231661753.html) | [MP1495](https://www.monolithicpower.com/en/mp1495.html) | 5-16V | 1.25-5V | 3A | 500kHz | :white_check_mark:| :white_check_mark: | Adjustable voltage output selectable by pot or solder joints. Large holes designed for wire-to-board mean this can't easily be PCB mounted. |
| <img src="https://github.com/playfultechnology/arduino-power/blob/main/images/Mini.png" />  | ["Mini"](https://www.aliexpress.com/item/4000016739581.html) | Marked as "DKGAA" | 12-24V* | 1.8-12V | 3A | 500kHz |  :white_check_mark: | :white_check_mark: | Adjustable (need knife to break trace as described [here](https://forum.arduino.cc/t/confused-about-a-step-down-mini-dc-dc-12-24v/1159084/10)). Amazon reviews say not to exceed 15V input  | 
| <img src="https://github.com/playfultechnology/arduino-power/blob/main/images/MP1584EN.png" />| [MP1584EN](https://www.amazon.co.uk/DollaTek-MP1584EN-Step-Down-Adjustable-Converter/dp/B07DJ5HZ7G) | [MP1584](https://www.monolithicpower.com/en/mp1584.html) |  4.5-28V | 0.8-20V | 3A | 1.5MHz | :white_check_mark: | :white_large_square: | Pot adjustment _only_ | 
| <img src="https://github.com/playfultechnology/arduino-power/blob/main/images/QSKJ.jpg" />| [QSKJ "Fine"](https://www.aliexpress.com/item/32815170131.html) | [MP2315](https://www.openhacks.com/uploadsproductos/datasheet_77.pdf) | 6.5-24V | 5V | 3A | 500Khz |  :white_large_square:| :white_large_square: | Output is only via a USB socket |

[^1]: Higher switching frequency will mean less ripple on the output (more accurate voltage/current) but causes more overhead due to switching, which reduces the efficiency somewhat.

However, all of these modules have flaws of one sort of other:are typically based on somewhat old Monolithic Power Systems ICs which are not recommended for new designs.
 - MP1495 (used in "CA1235") and MP1584 are both old ICs from Monolithic Power Systems not recommended for new designs. (The [MP2338](https://www.monolithicpower.com/en/mp2338.html) is the recommended alternative instead).
 - MP2315 (used in "QSKJ Fine") is also not recommended for new designs, with the [MP2393](https://www.monolithicpower.com/en/mp2393.html) suggested alternative instead.
 - The QSKJ is not usable on a PCB due to the output only having a USB interface, while the CA1235 not usable in a custom PCB design due to its non-standard pin diameter. 
 - The "Mini" uses a "DKGAA" chip of unknown origin or specs, and it requires manual modification (removing trace to the potentiometer) to make it output a fixed voltage

So, one alternative is to design a custom power subsystem. There's a useful reference article here: https://medium.com/supplyframe-hardware/designing-power-supplies-that-are-97-efficient-179e8ab887c5  (based on the same MP2315 as the QSKJ Fine, which, as previously mentioned, is not recommended for new designs) 

Chipset | Input | Output | Max Current | Switching Frequency | Notes | Circuit |
------- |------ |------- |------------ | ------------------- | ----- | ------- | 
| [XL1509](https://www.lcsc.com/datasheet/lcsc_datasheet_2304140030_XLSEMI-XL1509-5-0E1_C61063.pdf) | 5-16V | 1.25-5V | 2A | 150kHz | Used in Kincony power supply circuitry with relatively few additional components: https://www.kincony.com/kc868-a4-hardware-design-details.html| <img src="https://github.com/playfultechnology/arduino-power/blob/main/images/Kincony-power-subsystem.png" /> |
| [XL1507-5.0](https://www.lcsc.com/datasheet/lcsc_datasheet_1811081616_XLSEMI-XL1507-5-0E1_C74195.pdf) | 54.5-40V | 5V (fixed version) | 3A | 150kHz | More current than above. Available in fixed and adjustable versions. 5000 in stock at LCSC. | <img src="https://github.com/playfultechnology/arduino-power/blob/main/images/XL1507.png" /> |
| [XL1530](https://crossic.com/wp-content/uploads/2021/12/XL1530-datasheet-English.pdf) | 3.6-18V | 0.8-16V | 3A | 380kHz | 4000 in stock at LCSC| <img src="https://github.com/playfultechnology/arduino-power/blob/main/images/XL1530.png" /> | 

Also see https://blog.yavilevich.com/2017/03/efficient-dc-12v-to-5v-conversion-for-low-power-electronics-evaluation-of-six-modules/
