---
title: Personal Block Diagram
---

## General Description
The Block Diagram schematic that you can see below is responcible for demonstrating all connections between the MCU(Microcontroller) and all in-circuit elements/devices that are implemented within the Sensor Subsystem of Team 204 project device. Those elements include:
- PIC18F26Q10 -> MCU from the PIC device family
- 3x VL53L4CD -> Time-of-flight sensors implementing functionality of sensor-to-microcontroller data transfer over an I2C serial communication channel
- 3x TXS0102 -> Voltage Level Translators, responcible for synchronising communications between the MCU and the sensors, due to these devices operating on a different voltage levels(3.3V & 2.8V)
- 2x LED-s -> red and green Light Emitting Diodes, serving for debugging purposes
- Push Button -> a standart SMD-type in-circuit push button, serving for the debugging purposes along with the LED-s
- UART communication channel -> two pins were reserved to serve as a TX and RX terminals of the inter-system(Team level) serial communication channel utilizing the UART protocol

![diagram_01](PBD.png "Personal Block Diagram")

### Important Notes 
- In the last version of the system's hardware structure, two independent voltage regulators are required in order to ensure the proper operation of the device - 3.3V and 2.8V output correspondingly. As expected, the 3.3V voltage regulator is responcible for providing power to the MCU(Microcontroller), 2 on-board LED-s and a pushbutton, while 2.8V regulator will be powering 3 sensors. Delivering the exact voltage level of 2.8V to each sensor was considered important, as despite the fact that sensors of VL53 family can operate relatively stable with the 3.3V, the manufacturer's datasheet strongly recommends utilizing 2.8V for enhanced measurement precision and faster rate of data transfer
- 3-pin clusters labeled "Output Enable" and "Sensor Hardware interrupt" are crucial to the proper operation of the system. "Output Enable" pins are responcible for "turning on"(setting into the Active mode) the 3.3-2.8V Voltage regulators on the ToF Sensors daughterboards; they must be configured as Digital Output pins on the MCU's end. On the other hand, "Sensor Hardware Interrupt" are handling the task of getting the MCU to know when the scanning data is ready for reception, by raising a corresponding Interrupt; they they must be configured as Digital Input pins on the MCU's end

## Development Changes and Adjustments

The first version of the Block Diagram, prepared and released at the time of February, 2025, was found to be extremely unpractical, unefficient and, in some cases - even misleading. After a coherent revision, the updated version of the Block Diagram was produced, now incorporating elements that came to existence due to changes and updates in device's hardware structure. Below is placed the list representing what exact adjustments and modifications were added to this document:
- Separate I2C lines issue was fixed: now all 3 ToF sensors are tied to just a single serial communication line
- Introduced a schematic representation of the 2.8V regulator as a power source for ToF sensors
- Added clusters of digital I/O pins for handling sensor-produced hardware interrupts and managing the operation states of the Voltage Level Translators (On/Off)
- Introduced MasterClear, Data and Clock pins handling the In-Circuit Serial Programming
- Fixed the issue with incorrect/misleading inter-pin connections labeling


## Related Links and References
[Link to the PDF version of the Block Diagram shown above](https://github.com/LordAndrey17/andreypodoprigora.github.io/blob/main/docs/PBD.pdf)
