# Gestro : Enabling gesture based support for standard devices
## Introduction
Gestro is an innovative solution designed to transform the way users interact with their electronic devices through intuitive gesture-based controls. This project aims to provide a seamless, user-friendly experience that enhances convenience and accessibility while promoting environmental sustainability. By enabling touch-free operation, Gestro offers a modern and hygienic alternative to traditional device interaction, making it ideal for various settings, including homes, offices, and healthcare facilities. Gestro not only enhances user experience but also contributes to reducing electronic waste, aligning with sustainable practices and supporting a more eco-friendly future.
## Overview
The system employs ultrasonic sensors to detect hand movements by emitting ultrasonic waves and measuring their reflection times, allowing for precise recognition of gestures such as swipes. A Bluetooth module enables wireless communication between Gestro and various devices, ensuring seamless integration and reliable control signals. At the heart of the system is a development board, VSD Squadron Mini, which processes sensor data and manages communication. The firmware, developed using Moun River Studio, ensures that sensor data is accurately interpreted and converted into commands for connected devices. This approach not only enhances user experience by providing a modern, touch-free interface but also promotes environmental sustainability by extending the lifespan of existing devices and reducing electronic waste. Gestro’s design focuses on user-friendly setup and customization, making it accessible for a wide range of users, including the elderly and disabled, and ideal for environments where hygiene is critical. The project delivers significant benefits, such as cost savings, improved accessibility, and enhanced convenience, positioning Gestro as a versatile and sustainable solution for modern device interaction.
## Table for Pin Connections
### For Wired Product
| HC-SR04 Ultrasonic Sensor 1| VSD Squadron Mini |
| ------------- | ------------- |
| Trigger pin | PD3 |
| Echo pin | PD2 |
| VCC | 5V |
| GND | GND |

| External Power Supply | HC-SR04 Ultrasonic Sensor 2| VSD Squadron Mini |
| ------------- | ------------- | ------------- |
| - | Trigger pin | PD4 |
| - | Echo pin | PD6 |
| 5V | VCC | - |
| GND | GND | GND |

### For Wireless Product
#### Transmitter Part
| HC-SR04 Ultrasonic Sensor 1| VSD Squadron Mini |
| ------------- | ------------- |
| Trigger pin | PD3 |
| Echo pin | PD2 |
| VCC | 5V |
| GND | GND |

| External Power Supply | HC-SR04 Ultrasonic Sensor 2| VSD Squadron Mini |
| ------------- | ------------- | ------------- |
| - | Trigger pin | PD4 |
| - | Echo pin | PD5 |
| 5V | VCC | - |
| GND | GND | GND |

| HC-05 Bluetooth Transmitter Module| VSD Squadron Mini on Transmitter Module |
| ------------- | ------------- |
| TXD | PD7 |
| RXD | PD6 |
| State | PC7 |
| VCC | 3.3V |
| GND | GND |

#### Receivers Part
| HC-05 Bluetooth Receiver Module| VSD Squadron Mini on Receiver Module |
| ------------- | ------------- |
| TXD | PD7 |
| RXD | PD6 |
| State | PC7 |
| VCC | 3.3V |
| GND | GND |

## Pinout Diagram
### Wired Product
![Screenshot 2024-07-02 012437](https://github.com/ppattanaik/Gestro/assets/63561037/01d86492-3292-43d2-a2c8-8d2e5bcedecd)

### Wireless Product
#### Transmitter Module
![Screenshot 2024-07-02 012521](https://github.com/ppattanaik/Gestro/assets/63561037/c3ff742f-7037-46ba-95c6-60103578b66b)

#### Receiver Module
![Screenshot 2024-07-02 012536](https://github.com/ppattanaik/Gestro/assets/63561037/06ddab72-ce73-47a4-8427-400ba97b2194)

## Acknowledements
 - Kunal Ghosh, Co-Founder and Director, VSD Corp. Pvt. Ltd.
 - International Institute of Information Technology, Bangalore
 - Electronic City Industries Association(ELCIA), Bangalore
