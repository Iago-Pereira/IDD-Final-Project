# IDD-Final-Project

## Project Description and Initial Plan

### Idea and Application

The project consists of a prototype for a wheelchair that can be controlled via electroencephalogram (EEG) sensing. The main application of this wheelchair is to enable paralyzed individuals to have control over their transportation by using their thoughts.

### Team

Alana Crognale

Eva Esteban

Tomi Kalejaiye

### Rough Form and Paper Prototype

<img align="center" width="375" height="500" src="https://github.com/evaesteban/IDD-Final-Project/blob/master/IMG_0893.jpeg">
<img align="center" width="500" height="375" src="https://github.com/evaesteban/IDD-Final-Project/blob/master/IMG_0894.jpeg">
<img align="center" width="375" height="500" src="https://github.com/evaesteban/IDD-Final-Project/blob/master/IMG_0895.jpeg">
<img align="center" width="375" height="500" src="https://github.com/evaesteban/IDD-Final-Project/blob/master/IMG_0896.jpeg">
<img align="center" width="375" height="500" src="https://github.com/evaesteban/IDD-Final-Project/blob/master/IMG_0902.jpeg">

### Expected Parts

EEG headset, arduino, wheels, motors, LEDs, small physical wheelchair prototype.

### Interaction Plan

The person will wear the headset, which will be connected to the wheelchair, and control the wheelchair movement with it.

## Project Implementation 

### Hardware Components

We bought the Star Wars Force Trainer II toy, which contains an EEG sensing headset that uses a NeuroSky board. We also gathered a green LED and a green LED with the corresponding 220 Ohm resistors, and a motor with the corresponding components to build a protective circuit around it: a transistor, a 2.2 KOhm resistor, and a diode. We used an Arduino Uno to control the different components, and jumper wires to connect them together. 

### System Description

The EEG headset measures the different values such as attention, meditation, beta waves and other measurements of the human brain. These values are read by using an Arduino Uno connected to the transmitter (T) pin of the EEG sensing board - for this we opened up the toy and soldered a cable to the T pin. 

The attention values range from 0 to 100, with 0 indicating that the user is not concentrating at all, and 100 meaning the user has reached the maximum atttention value measurable. Using the Arduino, this value gets thresholded at around 60 - a threshold that can be modified according to the difficulty the person wearing the headset might have. When the attention value is above 60, the Arduino turns the motor on and the wheel starts rotating. Also, the green LED turns on and the red LED turns off to indicate that the chair is moving to both the user and the people around. When the value goes below 60, the wheel stops, the green LED turns off, and the red LED turns on to indicate that the chair is not moving. 

The state diagram for the product can be found below. 

![](State_Diagram.jpeg)

### Firmware

In order to read from the headset, the code from https://github.com/JimRoskind/NeuroskyHacking was used as a base code. The code and libraries were later modified in order to read only the attention value from the headset, and remove the parts of the code reading and processing unnecessary values. Additional code was incorporated to interact with the LEDs and the wheel motor. 

A link to the final code can be found below.

[Link to Code](https://github.com/evaesteban/IDD-Final-Project/blob/master/ForceTrainerV2/ForceTrainerV2.ino)

### Testing and Debugging 

Even though the initial idea for the project was to create the full wheelchair prototype, the final deliverable was a proof of concept to demonstrate that both the wheels and the LEDs can be controlled with the mind. This simplification was implemented for two main reasons: a large amount of time had to be spent on debugging and understanding the data being read from the headset, rather than building a small wheel chair structure, and green/red LED functionality to provide feedback on the chair movement was included. Even though the light feature was not in the original plan, user testing proved it to be necessary for the person to know whether the chair was moving and they were concentrating appropriately, so the feature was prioritized.

Firstly, in order to read the values from the headset, a baud rate of 9600 bits/sec was initially used. We then realized that this only worked for the Force Trainer I device, but the new Force Trainer II used a baud rate of 57600. Secondly, we found that the packets from the headset were being sent to the Arduino and filling up the buffer at a very high speed, causing even printing to serial to corrupt the data reading process. We therefore decided to remove all delays and limit the use of the serial interface. Once these errors were fixed, we could read the values from the headset correctly. 

In order to use the motor and prevent it from drawing too much power, we used a diode and a transistor. Debugging the circuit, we found that the transistor was damaged and exchanged it for a new one. We found this fault by isolating and testing each component, as well as testing the hardware separate from the firmware.

## Project Video 

[Link to Video](Wheel_Video.mp4)
