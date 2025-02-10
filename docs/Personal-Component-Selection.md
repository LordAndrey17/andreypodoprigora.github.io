---
title: Personal Component Selection
---
## 1. Major Component Selection

### Inroduction 
The type of sensor proposed and selected earlier for this semester’s group project is a distance measuring sensor. Nowadays, a variety of physical phenomena is utilised to create this type of sensors, including, but not limited to: infrared emitting, ultrasonic “listening” and laser-based detection. Taking into account the guidelines of the current project, the sensor selection process was performed under the following considerations: the sensor chip should incorporate at least 1 serial communication protocol; the sensor chip should not come from the manufacturer as a part of “daughterboard”-type PCB, unless the chip itself is too small to be manually soldered on the self-designed PCB. The results of this selection are presented below: 

### Distance Sensor Module

| **Solution**                                                                                                                                                                                      | **Pros**                                                                                                                                    | **Cons**                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| ![](image1.png)<br>Option 1.<br> VL53L4CD Time-of-Flight high accuracy low power proximity sensor<br>$1/each<br>[link to product](https://www.digikey.com/en/products/detail/stmicroelectronics/VL53L4CDV0DH-1/16123783?s=N4IgTCBcDaIGoBkCsBmBAWAwgERAXQF8g)                 | \* Provides up to 1.3 meters of scanning distance range<br>\* Extremely compact and miniature (4.4 x 2.4 x 1 mm size)<br>\* Successfully operates under the standardized power supply of 3.3 Volts<br>\* Capable of reaching the communication frequency up to 1 MHz (I2C-based)<br>\* Incorporates a system driver based on the so-called “Ultra Light Driver” (ULD) - an API set developed by manufacturer(STMicroelectronics) as a uniform solution for various sensor models, that is actively supported and updated<br>\*                                               | \* Comes in a Land Grid Array(LGA)-type packaging, which is expected to be hard for traditional(solder iron-based) soldering (12 pins in total)<br>\* Provides Field of View(FoV) angle of only 18 degrees within a single plane |
| ![](image3.png)<br>\* Option 2. <br>\* CTX936TR-ND surface mount oscillator <br>\* $1/each <br>\* [Link to product](http://www.digikey.com/product-detail/en/636L3I001M84320/CTX936TR-ND/2292940) | \* Outputs a square wave <br>\* Stable over operating temperature <br> \* Direct interface with PSoC (no external circuitry required) range | * More expensive <br>\* Slow shipping speed                                                         |

**Choice:** Option 2: CTX936TR-ND surface mount oscillator

**Rationale:** A clock oscillator is easier to work with because it requires no external circuitry in order to interface with the PSoC. This is particularly important because we are not sure of the electrical characteristics of the PCB, which could affect the oscillation of a crystal. While the shipping speed is slow, according to the website if we order this week it will arrive within 3 weeks.

## 2. Microcontroller Selection
### Personal Role Within the Team 
The selected concept for the Spring 2025 semester project by team #204  is a bi-wheeled robot with object-following capabilities. Within the scope of this project,  my primary responsibility area is focused around sensing functionality of the proposed robotic device. In this regard, I proposed the design involving placement of 3 identical Time-of-Flight(ToF) sensors in the frontal part of the robot, each directed outwards to the robot’s center  in order to increase the Field of View available to the device. The process of selecting the actual market-available sensor solution was performed earlier in this document(the final choice was identified to be VL53L4CD). In order to transfer the observed data to the Host MCU, all three sensors will be using a single I2C bus (the approximated communication speed is expected to vary between 0.75-1 MHz). After the data was received and pre-processed(e.g. unit conversion) by the Host MCU, it will then be transferred to the neighboring MCU in the systems’ UART daisy chain.

## Proposed Microcontroller Solution: PIC18F25Q10

| PIC MCU Info                                      | Answer | Help                                                                                                      |
| --------------------------------------------- | ------ | --------------------------------------------------------------------------------------------------------- |
| Model                                         | PIC18F25Q10  SOIC/28     |
| Product Page URL                              | [link](https://www.microchip.com/en-us/product/pic18f25q10#Design%20Resources)                                    |
| Datasheet URL(s)                              | ?      | Do not paste links directly into the table.  Use a [link](#)                                              |
| Application Notes URL(s)                      | ?      | Do not paste links directly into the table.  Use a [link](#)                                              |
| Vendor link                                   | ?      | Digikey, Jameco, etc.  Do not paste links directly into the table.  Use a [link](#)                       |
| Code Examples                                 | ?      | url(s) for libraries on github or other sites related to the microcontroller and your planned peripherals |
| External Resources URL(s)                     | ?      | Search on Google and YouTube for other resources for each specific microcontroller.                       |
| Unit cost                                     | ?      | Find in the Microchip online store, or Digikey                                                            |
| Absolute Maximum Current for entire IC        | ?      | Find in the microcontroller datasheet                                                                     |
| Supply Voltage Range                          | ?      | Min / Nominal / Max / Absolute Max, as found in datasheet                                                 |
| Absolute Maximum current <br> (for entire IC) | ?      | as found in datasheet                                                                                     |
| Maximum GPIO current <br> (per pin)           | ?      | as found in datasheet                                                                                     |
| Supports External Interrupts?                 | ?      | as found in datasheet                                                                                     |
| Required Programming Hardware, Cost, URL      | ?      | found on the microcontroller's product page                                                               |
| Works with MPLabX?                            | ?      | Required.  See [Microchip Development Tools](https://www.microchip.com/development-tools)                 |
| Works with Microchip Code Configurator?       | ?      | Can be validated in MPLabX.  Screenshot required.                                                         |


| Module | # Available | Needed | Associated Pins (or * for any) |
| ---------- | ----------- | ------ | ------------------------------ |
| GPIO       | ?           | ?      | ?                              |
| ADC        | ?           | ?      | ?                              |
| UART       | ?           | ?      | ?                              |
| SPI        | ?           | ?      | ?                              |
| I2C        | ?           | ?      | ?                              |
| PWM        | ?           | ?      | ?                              |
| ICSP       | ?           | 1      | ?                              |
| ...        | ...         | ...    | ...                            |


