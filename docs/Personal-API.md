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

### Change Following Distance
| Type | Byte 1 | Byte 2 |
| ---- | ------ | ------ |
| Variable Name | message_type | set_distance |
| Variable Type | uint8_t | uint8_t |
| Min Value | 0 | 0 |
| Max Value | 9 | 100 |
| Example | 1 | 20 |

- This message sets the distance at which the robot is supposed to stay away from the object it is detecting. The message begins with byte one, the message type, allowing the reciever to sort the message easier, then byte 2 is the value of the distance that the robot is supposed to keep away from the object its tracking. The set_distance value does not directly communicate with sensors or motor it only states the distance goal that the robot is supposed to keep. This message will be sent to both Andrey and Divine's subsystems that they will use accordingly.

#### Change Motor Speed
| Type | Byte 1 | Byte 2 |
| ---- | ------ | ------ |
| Variable Name | message_type | motor_speed |
| Variable Type | uint8_t | int8_t |
| Min Value | 0 | 0 |
| Max Value | 9 | 100 |
| Example | 0 | 50 |

- This message changes the speed at which the motors will move at. The message begins with the message type allowing the reciever to sort the message easier, then byte 2 is the target speed at which the motor will travel at. The speed value does not control the motor directly just states at what speed all the motors will move at. The message will send to both Divine and Jacob's subsystem and they will update accordingly.


#### Drive Individual motor
| Type | Byte 1 | Byte 2 | Byte 3 |
| ---- | ------ | ------ | ------ |
| Variable Name | message_type | motor_id | motor_speed |
| Variable Type | uint8_t | uint8_t | int8_t |
| Min Value | 0 | 1 | 0 |
| Max Value | 9 | 2| 100 |
| Example | 0 | 1 | 30 |

- This message is for driving the motors independently so that the user can directly control the motors using the buttons on the robot. Byte 1 in the message is the meesage type allowing the reciever to sort the message easier. Then byte 2 is the motor_id to select which motor the message is targeting. Byte 3 is the speed at which the motor will be moving at. This message would be sent to Jacob's subsytem.

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
