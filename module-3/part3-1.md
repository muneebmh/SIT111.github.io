# Introduction to Motor Control with Arduino


Welcome to Module 3.1, where we'll delve into the fascinating world of motor control using Arduino. In this section, you'll gain a comprehensive understanding of motor control principles, explore the basics of servo motor control, and discover the significant role of motors in robotics and automation.

# Understanding Motor Control

## Motor Control Basics:
Motor control is the process of managing the operation and movement of motors in various applications. Motors are essential components in countless devices and machines, from simple household appliances to advanced industrial robots. In this module, we'll primarily focus on DC (Direct Current) motors and servo motors.
In the Arduino world, motor control is all about making motors move just the way we want. We'll focus on two main types: DC (Direct Current) motors and servo motors. DC motors are like the workhorses of the motor world. They can spin in both directions and change speeds, making them great for lots of different Arduino projects.



# DC Motor Control

**DC (Direct Current)** motors are commonly used in various applications. They are simple devices that convert electrical energy from a power source, like a battery or power supply, into mechanical motion. DC motors can rotate in both directions and vary their speed, which makes them versatile for many tasks. Arduino can control DC motors by adjusting the voltage supplied to them, enabling precise control over their movement in various projects, from robotics to automation systems.
Some of the key features are:

+ **Versatile Actuators:** DC motors are the workhorses of Arduino projects due to their versatility.
+ **Bidirectional Movement:** They can rotate in both clockwise and counterclockwise directions, making them ideal for controlling wheels, fans, and more.
+ **Speed Control:** Arduino allows for precise speed regulation of DC motors, enabling applications like robot movement and conveyor systems.


## Real-World Examples:**

+ Arduino Robot Car: In the real-world example of an Arduino Robot Car, you can construct a mobile robot using DC motors. This robot can be programmed to navigate its environment autonomously, detecting obstacles and changing its path to avoid collisions. It showcases how DC motors and Arduino can be combined to create a simple but practical autonomous vehicle.
+ Smart Fan: In the case of a Smart Fan, you can design an IoT (Internet of Things) connected fan using DC motors. By integrating temperature sensors, the fan can monitor the surrounding temperature and adjust its speed accordingly. For instance, when it detects a rise in temperature, it can increase the fan speed to cool the room effectively. This example illustrates the application of DC motors in enhancing the functionality of everyday appliances through Arduino-based control and connectivity.


### Example: DC Motor Speed Control with Arduino
Let's start by demonstrating how to control the speed of a DC motor using an Arduino and other components. 

![Figure 3 11](https://github.com/muneebmh/SIT111.github.io/assets/149995551/2bb203d7-6a67-4745-99d3-b989bcb06e7e)

*Figure 3.11 Configuration of DC Motor Speed Control with Arduino (Source: https://circuitdigest.com/microcontroller-projects/dc-motor-speed-control-using-arduino-and-potentiometer)*


```cpp
int pwmPin = 12;     // Assigns pin 12 to the variable 'pwmPin'
int pot = A0;        // Assigns analog input A0 to the variable 'pot'
int c1 = 0;          // Declares variable 'c1'
int c2 = 0;          // Declares variable 'c2'

void setup() {
  pinMode(pwmPin, OUTPUT); // Set 'pwmPin' as an OUTPUT
  pinMode(pot, INPUT);     // Set 'pot' as an INPUT
}

void loop() {
  c2 = analogRead(pot);    // Read the analog value from 'pot' and store it in 'c2'
  c1 = 1024 - c2;          // Calculate the difference between 1024 and 'c2' and store it in 'c1'
  
  digitalWrite(pwmPin, HIGH);      // Set 'pwmPin' to HIGH
  delayMicroseconds(c1);           // Delay for 'c1' microseconds
  digitalWrite(pwmPin, LOW);       // Set 'pwmPin' to LOW
  delayMicroseconds(c2);           // Delay for 'c2' microseconds
}

```

This example demonstrates how to control the speed of a basic DC motor using Arduino.


# Servo Motor Control


A servo motor is a type of motor commonly used in various applications, including robotics and automation. Unlike DC motors, servo motors are known for their precision and ability to move to specific angles with great accuracy. They operate based on feedback control systems, which means they receive continuous feedback about their current position and adjust their rotation accordingly. This makes them ideal for tasks where precise positioning or angular control is essential. For instance, in a robotic arm, a servo motor can precisely control the angle of each joint, allowing for accurate and controlled movements. Arduino can be used to control servo motors, making them a valuable component in many DIY projects and robotics applications.
Some of the key features are:

+ **Precision Positioning:** Servo motors excel at accurately positioning objects, making them perfect for tasks requiring precision.
+ **Angle Feedback:** They come with built-in feedback mechanisms to maintain and adjust their positions, ensuring accuracy.
+ **Limited Angular Range:** Arduino can control servo motors within a specific angular range, ideal for tasks like controlling robotic arms or camera gimbals.

## Real-World Examples:
+ **Arduino Robotic Arm:** Imagine building a robot arm that moves just like your own arm. By using servo motors controlled by an Arduino, you can make the robot mimic your hand gestures and perform tasks such as picking up objects, drawing, or waving.

+ **Camera Stabilizer:** Think of creating a device that can keep your camera perfectly steady while you're filming. With Arduino, you can build a camera stabilizer that compensates for any unwanted movements, ensuring your videos are smooth and professional, even when you're on the move.

## Servo Control: 
Servo Control is a fundamental concept in robotics and automation. Servo motors are incredibly versatile and precise, and they are controlled using a method known as Pulse Width Modulation (PWM). In this system, the width or duration of the PWM signal is used to specify the position or angle at which the servo motor should rotate. By adjusting the width of the signal, you can finely control the servo's movement, making it stop at specific angles or smoothly transition between positions. This level of accuracy and control is crucial in applications such as robotic arms, remote-controlled vehicles, and even in simple mechanisms like opening and closing doors or adjusting the steering in radio-controlled cars. PWM signals provide the means to achieve these precise movements, making servo motors an essential component in various automated systems.

### Example: Controlling a Servo Motor with Arduino
Let's delve into controlling a servo motor with Arduino, enabling you to move it to specific angles accurately.

![Figure 3 12](https://github.com/muneebmh/SIT111.github.io/assets/149995551/7d456ea6-0955-4343-b0c5-382e9caa5e28)

*Figure 3.12 Schematic Diagram to Control Servo via Ardunio (Source: https://www.makerguides.com/servo-arduino-tutorial/)*

```cpp
#include "Servo.h"
Servo myservo;  // Create a servo object
#define servoPin 9  // Define the servo pin

void setup() {
  myservo.attach(servoPin);  // Attach the servo to the defined pin
}

void loop() {
  myservo.write(90);  // Set the servo angle to 90 degrees
  delay(1000);
  myservo.write(180);  // Set the servo angle to 180 degrees
  delay(1000);
  myservo.write(0);  // Set the servo angle to 0 degrees
  delay(1000);

  // Sweep the servo from 0 to 180 degrees
  for (int angle = 0; angle <= 180; angle += 1) {
    myservo.write(angle);
    delay(15);
  }

  // Sweep the servo from 180 to 0 degrees
  for (int angle = 180; angle >= 0; angle -= 1) {
    myservo.write(angle);
    delay(15);
  }
  delay(1000);
}

```

This code demonstrates how to control a servo motor using an Arduino board.

# Motors in Robotics

## Role of Motors in Robotics:
Motors are the driving force behind robots. They enable robots to move, interact with their environment, and perform tasks. Understanding motor control is crucial for anyone interested in robotics.

Types of Robot Motors: Robots use various types of motors, including DC motors, servo motors, stepper motors, and more, depending on their design and intended tasks.
### Example: Motor Applications in Robotics
### Everyday Examples of Motors:
+ **Electric Fans:** Electric fans found in homes and offices utilize electric motors for their operation. The motor drives the rotation of fan blades, creating airflow that helps cool the environment. This concept of motor-driven rotation is fundamental to understanding how motors work, which is essential in the context of motor control with Arduino.
+ **Power Windows in Cars:** Many modern cars feature power windows, which are equipped with electric motors. These motors enable the automatic raising and lowering of car windows with the push of a button. Understanding the principles of motor control, as covered in the course, provides insights into how such mechanisms function.
+ **Conveyor Belts in Manufacturing:** Manufacturing facilities often employ conveyor belts driven by motors to transport goods efficiently along production lines. Motor control knowledge is vital for optimizing conveyor belt performance.
+ **Drone Propulsion:** Drones utilize various types of motors, including brushless DC motors, for propulsion and maneuverability. Precise motor control is crucial for stable flight and control.
+ **3D Printers:** 3D printers employ stepper motors to control the movement of print heads and build objects layer by layer. Understanding motor control is integral to achieving accurate and high-quality 3D prints.

These everyday examples illustrate how motors are integrated into common devices, showcasing their practical applications and the importance of motor control knowledge. 
