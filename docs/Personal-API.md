---
title: Personal API and message processing features
---

# Overview

The Application Programming Interface (API) describes the features of data transfer between two/multiple computers(devices).
In our API-describing documents our team will provide information on what types of messages are being sent between different devices,
along with outline of which subsystem should act as receiver/transmitter in case of each separate message.
Below I present the API specification of the messages received/transmitted by the Sensor Subsystem

# Message Protocol

## Messages Transmitted by the Sensor Subsystem

These are messages that the Sensor Subsystem transmits to the rest of the device subsystems.
Each table demonstrates the message structure with along with a description of how it works and who will recieve the message.

### Set Motor 1 to Speed X and Motor 2 to Speed Y
| Type | Byte 1 | Byte 2 | Byte 3 |
| ---- | ------ | ------ | ------ |
| Variable Name | message_type | motor_1_speed | motor_2_speed |
| Variable Type | uint8_t | uint8_t | uint8_t |
| Min Value | 0 | 0 | 0 |
| Max Value | 8 | 100 | 100 |
| Example | 2 | 25 | 75 |

**Sent to:** <br>
Motor subsystem(Jacob) <br>
**Purpose:** <br>
This message is designed to provide the Motor(Actuator) Subsystem with the relevant data for configuring/adjusting the target-chasing movement and trajectory of the project's robot. Since the Motor Subsystem incorporates a double-motor based design, the message contains two variables, describing the desired speed levels for each of the two motors, calculated beforehand within the operational range of the Sensor subsystem. The mentioned speed values are expressed in the form of an unsigned integer numbers representing percent levels between 0 and 100, such that 0 is a 0% and 100 is 100%.

### Update Displayed Tracking Distance X		
| Type | Byte 1 | Byte 2 |
| ---- | ------ | ------ |
| Variable Name | message_type | tracking_distance |
| Variable Type | uint8_t | uint8_t |
| Min Value | 0 | 0 |
| Max Value | 8 | 100 |
| Example | 5 | 65 |

**Sent to:** <br>
UI subsystem(Jake), Wi-fi subsystem(Divine) <br>
**Purpose:** <br>
The single purpose of this message is to deliver data on the currently-observed distance between the robot and a tracking object to the built-in User Interface (UI) as well as to any relevant external UI-s (e.g. pc monitor, laptop, phone screen), accessible thorugh the Wi-fi communication. Aside from the identifiction bytem it contains only one uint_8 type variable, representing the observed distance in cm("0" -> 0 cm, "65" -> 65 cm)

### Subsystem Z Status Report
| Type | Byte 1 | Byte 2 | Byte 3 |
| ---- | ------ | ------ | ------ |
| Variable Name | message_type | sender_id | status_code |
| Variable Type | uint8_t | uint8_t | uint8_t |
| Min Value | 0 | 1 | 1 |
| Max Value | 8 | 4 | 25 |
| Example | 7 | 2 | 21 |

**Sent to:** <br>
UI subsystem(Jake), Wi-fi subsystem(Divine) <br>
**Purpose:** <br>
This type of messages is responsible for reporting the currently-observed status of the Sensor Subsystem to the various User Interfaces for maintenance, debugging and/or operation control purposes. The status-related data is delivered through a single uint8 variable, capable of taking values from (1) to (Max Value), with each number representing one and only type of a Sensor Subsystem condition; f.e. : "2" -> "Sensor subsystem is currently transmitting data to the Motor Subsystem", "5" -> "1 sensor is successfully observing the target object", "6" - "2 sensors are successfully observing the target object"

### Subsystem Z Error Report
| Type | Byte 1 | Byte 2 | Byte 3 |
| ---- | ------ | ------ | ------ |
| Variable Name | message_type | sender_id | error_code |
| Variable Type | uint8_t | uint8_t | uint8_t |
| Min Value | 0 | 1 | 1 |
| Max Value | 8 | 4 | 25 |
| Example | 8 | 3 | 21 |

**Sent to:** <br>
UI subsystem(Jake), Wi-fi subsystem(Divine) <br>
**Purpose:** <br>
This type of messages is responsible for reporting the currently-registered errors of the Sensor Subsystem to the various User Interfaces for maintenance, debugging and/or operation control purposes. The error-related data is delivered through a single uint8 variable, capable of taking values from (1) to (Max Value), with each number representing one and only type of a Sensor Subsystem error; f.e. : "2" -> "First sensor is not responding", "3" -> "Second sensor is not responding", "6" - "Sensors #1 and #3 are not responding"

## Messages Received by the Sensor Subsystem

These are messages that the Sensor Subsystem receives from other subsystems of the device.
Each table demonstrates the message structure with along with a description of how it works and who is responcible for transmitting each type of message.

### Start / Stop Subsystem Z
| Type | Byte 1 | Byte 2 | Byte 3 |
| ---- | ------ | ------ | ------ |
| Variable Name | message_type | target_subsystem | control_signal |
| Variable Type | uint8_t | uint8_t | uint8_t |
| Min Value | 0 | 1 | 0 |
| Max Value | 8 | 4 | 1 |
| Example | 1 | 3 | 1 |

**Received from:** <br>
UI subsystem(Jake), Wi-fi subsystem(Divine) <br>
**Purpose:** <br>
The message with an exclusive capability to externally "turn off"(put in a software sleep mode), as well as "turn on"(awake from the software sleep mode) various subsystems of the device, including the Sensor-elated one. Because the message type is designed to be utilised with multiple subsystems, the sender is required not only to specify the control signal(on/off), but also point out to the target subsystem through a code based uint8 variable(e.g. "1" -> "Motor Subsystem", "2" -> "Sensor Subsystem")

### Change Distance Keeping Threshold to X
| Type | Byte 1 | Byte 2 |
| ---- | ------ | ------ |
| Variable Name | message_type | distance_treshold |
| Variable Type | uint8_t | uint8_t |
| Min Value | 0 | 0 |
| Max Value | 8 | 100 |
| Example | 3 | 25 |

**Received from:** <br>
UI subsystem(Jake), Wi-fi subsystem(Divine) <br>
**Purpose:** <br>
The message type that configures the distance keeping trechold value for the object-tracking operations within the Sensor Subsystem. Can be sent from both external and internal UI-s, requires a uint8-type variable specifying the desired treshold value in cm ("0" -> 0cm, "100" -> 100cm)

### Other Types of Messages

- Any message that I recieve that I do not have a protocol to handle the system will delete the message to help clean up the system and reduce clogging.
- If I recieve a message that I sent but no one recieved it I will delete the message so that the message is not cycling forever clogging the message system.
- Any message that I recieve that is not directed towards me but is directed to another teammember will be passed over to the next teammate in the subsystem so that they may recieve the message.
- If a message is addressed to someone not in my team then the system will delete the message preventing clogging due to dud messages.
