# Gestro : Enabling gesture based support for standard devices
## Introduction
Gestro is an innovative solution designed to transform the way users interact with their electronic devices through intuitive gesture-based controls. This project aims to provide a seamless, user-friendly experience that enhances convenience and accessibility while promoting environmental sustainability. By enabling touch-free operation, Gestro offers a modern and hygienic alternative to traditional device interaction, making it ideal for various settings, including homes, offices, and healthcare facilities. Gestro not only enhances user experience but also contributes to reducing electronic waste, aligning with sustainable practices and supporting a more eco-friendly future.
## Overview
The system employs ultrasonic sensors to detect hand movements by emitting ultrasonic waves and measuring their reflection times, allowing for precise recognition of gestures such as swipes. A Bluetooth module enables wireless communication between Gestro and various devices, ensuring seamless integration and reliable control signals. At the heart of the system is a development board, VSD Squadron Mini/Arduino Uno, which processes sensor data and manages communication. The firmware, developed using Moun River Studio, ensures that sensor data is accurately interpreted and converted into commands for connected devices. This approach not only enhances user experience by providing a modern, touch-free interface but also promotes environmental sustainability by extending the lifespan of existing devices and reducing electronic waste. Gestro’s design focuses on user-friendly setup and customization, making it accessible for a wide range of users, including the elderly and disabled, and ideal for environments where hygiene is critical. The project delivers significant benefits, such as cost savings, improved accessibility, and enhanced convenience, positioning Gestro as a versatile and sustainable solution for modern device interaction.
## Components Required:
### For Wired 
- Arduino Uno - 500INR
- HC-SR04 Ultrasonic Sensor (x2) - 725 INR
- Perfboard - 200 INR
- Jumper Wires - 100 INR
--------------------------------------------
- Total cost - 1525 INR
### For Wireless (Future implementation)
- VSD Squadron Mini (x2)
- HC-SR04 Ultrasonic Sensor (x2)
- HC-05 Bluetooth Transmitter Module (x2)
- Perfboard
- Jumper Wires
## Table for Pin Connections
### For Wired Product
| HC-SR04 Ultrasonic Sensor 1| Arduino Uno |
| ------------- | ------------- |
| Trigger pin | D11 |
| Echo pin | D10 |
| VCC | 5V |
| GND | GND |

| HC-SR04 Ultrasonic Sensor 2| Arduino Uno |
| ------------- | ------------- |
| Trigger pin | D6 |
| Echo pin | D5 |
| VCC | Vin |
| GND | GND |

### For Wireless Product (Future implementation)
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
<img width="666" alt="Wired" src="https://github.com/user-attachments/assets/6bc0be68-e7b0-42a3-a7ae-c3add451e5d3">

### Wireless Product (Future implementation)
#### Transmitter Module
![Screenshot 2024-07-02 012521](https://github.com/ppattanaik/Gestro/assets/63561037/c3ff742f-7037-46ba-95c6-60103578b66b)

#### Receiver Module
![Screenshot 2024-07-02 012536](https://github.com/ppattanaik/Gestro/assets/63561037/06ddab72-ce73-47a4-8427-400ba97b2194)

## Working Code
### Code for Arduino
```
const int trigPin1 = 11; // the number of the trigger output pin ( sensor 1 )
const int echoPin1 = 10; // the number of the echo input pin ( sensor 1 )     
const int trigPin2 = 6;  // the number of the trigger output pin ( sensor 2 ) 
const int echoPin2 = 5;  // the number of the echo input pin ( sensor 2 ) 

// variables used for distance calculation 
long duration;                               
int distance1, distance2; 
float r;
unsigned long temp=0;
int temp1=0;
int l=0;


void find_distance (void);

// this function returns the value in cm.
void find_distance (void)                   
{ 
  digitalWrite(trigPin1, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin1, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin1, LOW);

  duration = pulseIn(echoPin1, HIGH, 5000);// pulsein function wont wait more then 5000us for the ultrasonic sound to came back
                                          
 
  r = 3.4 * duration / 2;                  // calculation to get the measurement in cm using the time returned by the pulsein function.     
  distance1 = r / 100.00;

  digitalWrite(trigPin2, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin2, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin2, LOW);

  duration = pulseIn(echoPin2, HIGH, 5000);
  r = 3.4 * duration / 2;     
  distance2 = r / 100.00;
  delay(100);
}

void setup() 
{
  Serial.begin(9600);
  pinMode(trigPin1, OUTPUT); // initialize the trigger and echo pins of both the sensor as input and output:
  pinMode(echoPin1, INPUT);
  pinMode(trigPin2, OUTPUT);
  pinMode(echoPin2, INPUT);
  delay (1000);
    
}

void loop()
{
  find_distance(); 
                  
  
  if(distance2<=35 && distance2>=15) 
  { 
    temp=millis();                
    while(millis()<=(temp+300))     
    find_distance();
    if(distance2<=35 && distance2>=15) 
    {
     temp=distance2;                        
     while(distance2<=50 || distance2==0)   
     {
       find_distance();                      
       if((temp+6)<distance2)                
       {
       Serial.println("down");             
       }
       else if((temp-6)>distance2)       
       {
        Serial.println("up");              
       }
     }
    }
    else                                   
    {
      Serial.println("next");               
    }
  }

  else if(distance1<=35 && distance1>=15)  
  { 
  
    temp=millis();                           
  
    while(millis()<=(temp+300))             
    {
       find_distance();
       if(distance2<=35 && distance2>=15)  
       {
         Serial.println("change");        
         l=1;                             
         break;                         
       }
    }
    
    if(l==0)                          
    {
    Serial.println("previous");           
    while(distance1<=35 && distance1>=15) 
    find_distance();                      
    }
    l=0;                           
   }
   
}

```
### Code for performing gestures
```
import serial                                      # add Serial library for serial communication
import pyautogui                                   # add pyautogui library for programmatically controlling the mouse and keyboard.

Arduino_Serial = serial.Serial('com8',9600)       # Initialize serial and Create Serial port object called Arduino_Serial
 
while 1:
    incoming_data = str (Arduino_Serial.readline()) # read the serial data and print it as line
    print incoming_data                           
     

    if 'next' in incoming_data:                    # if incoming data is 'next'
        pyautogui.hotkey('ctrl', 'pgdn')         
        
    if 'previous' in incoming_data:                # if incoming data is 'previous'
        pyautogui.hotkey('ctrl', 'pgup')      

    if 'down' in incoming_data:                    # if incoming data is 'down'          
        pyautogui.scroll(-100)                   
         
    if 'up' in incoming_data:                      # if incoming data is 'up'                           
        pyautogui.scroll(100)                   
        
    if 'change' in incoming_data:                  # if incoming data is 'change'
        pyautogui.keyDown('alt')                
        pyautogui.press('tab')
        pyautogui.keyUp('alt')
        
    incoming_data = "";                            # clears the data
```
## Gestro Connections
![20240717_001157](https://github.com/user-attachments/assets/501957a3-13c6-490f-8e52-08c7bfee43c6)

## Demo Video
https://drive.google.com/file/d/1VSeHloKG6HW3EjwDA_6HP7rHV9mbXZ-R/view?usp=sharing

## Acknowledements
 - Kunal Ghosh, Co-Founder and Director, VSD Corp. Pvt. Ltd.
 - International Institute of Information Technology, Bangalore
 - Electronic City Industries Association(ELCIA), Bangalore
