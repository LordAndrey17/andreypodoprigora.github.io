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

## Messages Transmitted to the Sensor Subsystem

These are messages that the Sensor Subsystem receives from other subsystems of the device.
Each table demonstrates the message structure with along with a description of how it works and who is responcible for transmitting each type of message.

### Change Distance Keeping Threshold to X
| Type | Byte 1 | Byte 2 |
| ---- | ------ | ------ |
| Variable Name | message_type | distance_treshold |
| Variable Type | uint8_t | uint8_t |
| Min Value | 0 | 0 |
| Max Value | 8 | 100 |
| Example | 3 | 25 |

- <COMMENT>

### Start / Stop Subsystem Z
| Type | Byte 1 | Byte 2 | Byte 3 |
| ---- | ------ | ------ | ------ |
| Variable Name | message_type | target_subsystem | control_signal |
| Variable Type | uint8_t | uint8_t | uint8_t |
| Min Value | 0 | 1 | 0 |
| Max Value | 8 | 4 | 1 |
| Example | 1 | 3 | 1 |

- <COMMENT>

### Other Types of Messages

- Any message that I recieve that I do not have a protocol to handle the system will delete the message to help clean up the system and reduce clogging.
- If I recieve a message that I sent but no one recieved it I will delete the message so that the message is not cycling forever clogging the message system.
- Any message that I recieve that is not directed towards me but is directed to another teammember will be passed over to the next teammate in the subsystem so that they may recieve the message.
- If a message is addressed to someone not in my team then the system will delete the message preventing clogging due to dud messages.
