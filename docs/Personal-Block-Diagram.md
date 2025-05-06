---
title: Personal Block Diagram
---

![diagram_01](PBD.png "Personal Block Diagram")

### Important Notes 
- 3-pin clusters labeled "Output Enable" and "Sensor Hardware interrupt" are crucial to the proper operation of the system. "Output Enable" pins are responcible for "turning on"(setting into the Active mode) the 3.3-2.8V Voltage regulators on the ToF Sensors daughterboards; they must be configured as Digital Output pins on the MCU's end. On the other hand, "Sensor Hardware Interrupt" are handling the task of getting the MCU to know when the scanning data is ready for reception, by raising a corresponding Interrupt; they they must be configured as Digital Input pins on the MCU's end
- In the last version of the system's hardware structure, two independent voltage regulators are required in order to ensure the proper operation of the device - 3.3V and 2.8V output correspondingly. As expected, the 3.3V voltage regulator is responcible for providing power to the MCU(Microcontroller), 2 on-board LED-s and a pushbutton, while 2.8V regulator will be powering 3 sensors. Delivering the exact voltage level of 2.8V to each sensor was considered important, as despite the fact that sensors of VL53 family can operate relatively stable with the 3.3V, the manufacturer's datasheet strongly recommends utilizing 2.8V for enhanced measurement precision and faster rate of data transfer

## Development Changes and Adjustments

The first version of the block diagram, prepared and released at the time of February, 2025, was found to be extremely unpractical, unefficient and, in some cases - even misleading. After coherent  



## Related Links and References
[Link to the PDF version of the Block Diagram shown above](https://github.com/LordAndrey17/andreypodoprigora.github.io/blob/main/docs/PBD.pdf)
