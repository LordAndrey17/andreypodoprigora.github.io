---
title: Personal Subsystem Schematics
---

## 1) Schematics, Diagrams and Image Captures

### Motherboard Subsystem Schematics
![scheme_01](Motherboard_Schematics.png "Motherboard Subsystem Schematics")

### Motherboard Front-side PCB Outline
![scheme_02](Motherboard_PCB_Front.png "Motherboard Front-side PCB Outline")

### Motherboard Back-side PCB Outline
![scheme_03](Motherboard_PCB_Back.png "Motherboard Back-side PCB Outline")

### [sensor-hosting] Daughterboard Subsystem Schematics
![scheme_04](Daughterboard_Schematics.png "Daughterboard Subsystem Schematics")

### Daughterboard Front-side PCB Outline
![scheme_05](Daughterboard_PCB_Front.png "Daughterboard Front-side PCB Outline")

### Daughterboard Back-side PCB Outline
![scheme_06](Daughterboard_PCB_Back.png "Daughterboard Back-side PCB Outline")

### Motherboard Isometric View
![scheme_07](Motherboard_Iso.png "Motherboard Isometric View")

### Daughterboard Isometric View
![scheme_08](Daughterboard_Iso.png "Daughterboard Isometric View")

### Final Bill of Materials 
![scheme_09](PBOM.png "Personal Subsystem Schematics")

<br>
## 2) Discussion, Evaluations and Suggestions
In order to find out how the board, captured on the diagrams above, had "shown itself in the field", we decided to directly ask the creator, Andrey Podoprigora! Here is what he told us about his experience of working with the board during the last two months:
  -"Thank you so much for contacting me on that occasion! I will be more than happy to share my experience and feelings about this particular PCB project!!!”
 - “To start with, I should definitely mention that overall, I am greatly satisfied by how the board’s performance turned out in general! When not a single power outage or voltage regulator malfunction happens in more than two months, you know that this is definitely a sign of quality. Considering how much code debugging I was performing directly within the board, configuring the hardware part to operate like a clockwork, especially regarding its power distribution segment,  was no less than essential to the project’s success - in the end, it was always pleasing to know, that in case a  fresh-uploaded program was not working out, first thing to check would have been the coding itself, and only then I would start suspecting issues to originate from the hardware side. I particularly enjoyed working with LM2575 Switching Voltage Regulators, as those ‘workhorses’ were always able to output both precise and stable 2.8 & 3.3 V, no matter whether the 6, 9 or even 12 Volt adapter was plugged into the board"
 - “When it comes to evaluating what exact ‘main helpers’ have accompanied me on the path of configuring the board to run the code exactly as supposed, I simply cannot not mention the pair of  Red and Green Light Emitting Diodes(LED-s). After dozens of hours spent debugging and eliminating code inconsistencies, I can admit that a simple recommendation from professors to incorporate an on-board LED-s ended up often becoming a day-saver. The amount of use combinations that I’d come up with in regards to these indicating devices still impresses me by that day - “heartbeat” oscillator, task(code function) completion indicator, serial communication sending and receiving trigger - and finally, differential pulsation generator dependent on the ToF distance sensor’s proximity to the target object. To think that all of these became possible with just two LED-s, makes me question myself, what are 3, or even 4 LED-s are capable of?”
 - “Finally, I think it worth mentioning, that as for the last design iteration - in case the system will operate on its full extent through utilizing all programming modules(UART, SPI, I2C) and specified GPIO pins, not a single pin out of the whole 28-pin array will be accessible for ‘unplanned’ uses. Although this doesn’t sound as something to be particularly proud of, I shall specify that at any moment of time, at least 3 GPIO pins are available for a multi-functional use, including potential application for ‘unexpected needs’. From what I can tell after ~2 months of continuous work over this project, is that PIC18F26Q10 with its 28 pins is just enough for assembling a circuit device like mine, but it is not a bad idea to try designing a similar device utilizing PIC microcontrollers with a higher pin count (e.g. F27Q10 or F47Q10)“ <br>

## 3) Version 2.0
If I were to create a **Version 2.0** of my **PCB and hardware design**, I would DEFINITELY:
 - Increase the amount of in-circuit push buttons up to two, or even three, for expanding the debugging capabilities and enhancing the interface experience
 - Establish mandatory capacitor-based hardware debouncing for every push button integrated into the circuit(even with thorough software debouncing, the   existing one had demonstrated noticeably poor performance)
 - Raise the amount of in-circuit LED-s up to three, introducing a new color(most likely - yellow or blue)
 - Add “accessibe-with-comfort”(for mounting the Oscilloscope probes) testpoints to the Motherboard part of I2C communication channel(for some reason, in the current version there is none!!!)
 - Relocate the ICSP 5x1 male pin header to the board’s side - right now it is positioned right in the PCB-s middle, neighboring the PIC MCU
<br>



## 4) Related Links and References

[Link to the PDF version of the schematics(Motherboard and Daughterboard) shown above](https://github.com/LordAndrey17/andreypodoprigora.github.io/blob/main/docs/Summary_Schematics.pdf)

[Link to the summary Altium™ project zip archive](https://github.com/LordAndrey17/andreypodoprigora.github.io/blob/main/docs/Podoprigora_Altium_Project_Final_release.zip)

[Link to the gerber files zip archive(Motherboard & Daugtherboard)](https://github.com/LordAndrey17/andreypodoprigora.github.io/blob/main/docs/Gerber_Cumulative.zip)

[Link to the PDF version of the table shown above](https://github.com/LordAndrey17/andreypodoprigora.github.io/blob/main/docs/PBOM.pdf)

[Link to the Google Sheets version of the table shown above](https://docs.google.com/spreadsheets/d/1AKsVAjezf8IYZDiDhJCl3jdnxlUkPmnE/edit?usp=sharing&ouid=117176938971734382879&rtpof=true&sd=true)

