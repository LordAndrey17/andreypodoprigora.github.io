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

- <COMMENT>

### Update Displayed Tracking Distance X		
| Type | Byte 1 | Byte 2 |
| ---- | ------ | ------ |
| Variable Name | message_type | tracking_distance |
| Variable Type | uint8_t | uint8_t |
| Min Value | 0 | 0 |
| Max Value | 8 | 100 |
| Example | 5 | 65 |

- <COMMENT>

### Subsystem Z Status Report
| Type | Byte 1 | Byte 2 | Byte 3 |
| ---- | ------ | ------ | ------ |
| Variable Name | message_type | sender_id | status_code |
| Variable Type | uint8_t | uint8_t | uint8_t |
| Min Value | 0 | 1 | 1 |
| Max Value | 8 | 4 | 25 |
| Example | 7 | 2 | 21 |

- <COMMENT>

### Subsystem Z Error Report
| Type | Byte 1 | Byte 2 | Byte 3 |
| ---- | ------ | ------ | ------ |
| Variable Name | message_type | sender_id | error_code |
| Variable Type | uint8_t | uint8_t | uint8_t |
| Min Value | 0 | 1 | 1 |
| Max Value | 8 | 4 | 25 |
| Example | 8 | 3 | 21 |

- <COMMENT>

### Messages I Recieve

These are the messages that I can recieve from my teammates. The tables show the message structure along with a description of the message and who I would recieve the message from.

#### Update Displayed Following Distance
| Type | Byte 1 | Byte 2 |
| ---- | ------ | ------ |
| Variable Name | message_type | display_distance |
| Variable Type | uint8_t | uint8_t |
| Min Value | 0 | 0 |
| Max Value | 9 | 100 |
| Example | 1 | 20 |

- This message that I recieve will allow my system to update the displayed speed on the OLED screen. Byte 1 is the message type allowing my system to easily figure out what the message will be. Then byte 2 is the new distance that I will be displaying OLED screen. I will recieve this message from Divine.

#### Update Displayed Motor Speed
| Type | Byte 1 | Byte 2 |
| ---- | ------ | ------ |
| Variable Name | message_type | display_speed |
| Variable Type | uint8_t | int8_t |
| Min Value | 0 | -100 |
| Max Value | 9 | 100 |
| Example | 0 | 50 |

- This message that I recieve allows my system to update the displayed motor speed to the OLED screen. Byte 1 is the message type allowing my system to easily sort the message. Byte 2 is the new speed that the OLED screen will be displaying. I will recieve this message from Divine.


### Other Types of Messages

- Any message that I recieve that I do not have a protocol to handle the system will delete the message to help clean up the system and reduce clogging.
- If I recieve a message that I sent but no one recieved it I will delete the message so that the message is not cycling forever clogging the message system.
- Any message that I recieve that is not directed towards me but is directed to another teammember will be passed over to the next teammate in the subsystem so that they may recieve the message.
- If a message is addressed to someone not in my team then the system will delete the message preventing clogging due to dud messages.
