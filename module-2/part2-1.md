# ----------- Module 2: Arduino Programming Basics ---------------

Welcome to the next Module, where we'll embark on a comprehensive journey into the fundamental concepts of Arduino programming. In this section, "Arduino Programming Basics," we'll dive deep into the core elements that form the foundation of successful Arduino projects.

# Basics of the C/C++ Language for Arduino

## Understanding the C/C++ Language:
The Arduino programming environment is built upon a simplified version of the C/C++ programming language. To wield the full potential of Arduino, it's crucial to grasp the fundamental aspects:

### Variables and Data Types:
Variables are essential components of programming, allowing you to store and manipulate data. In Arduino, you'll frequently utilize various data types to declare variables:
+ **int (Integer):** Used for whole numbers.
+ **float (Floating-Point):** Used for numbers with decimal points.
+ **char (Character):** Used for single characters.
+ **boolean:** Used for representing true or false values.

```arduino
int age = 25; // Declares an integer variable 'age'
float temperature = 25.5; // Declares a float variable 'temperature'
char initial = 'A'; // Declares a character variable 'initial'
boolean isOn = true; // Declares a boolean variable 'isOn'
```

These examples demonstrate the use of various data types to represent different types of information.

### Control Structures:
Control structures are the backbone of any program, allowing you to make decisions and control the flow of your Arduino program. Some common control structures include:
+ **if statement:** Used for conditional execution.
+ **else statement:** Provides an alternative action.
+ **loops (e.g., for, while):** Used for repetitive tasks.

```arduino
int temperature = 28;

if (temperature > 30) {
  // If temperature is above 30 degrees, turn on a fan
  digitalWrite(fanPin, HIGH);
} else {
  // Otherwise, turn off the fan
  digitalWrite(fanPin, LOW);
}
```

This example illustrates an 'if' statement controlling a fan based on the temperature. Control structures are pivotal for creating dynamic and responsive Arduino projects.

# Functions and Libraries in Arduino Programming

## Functions:
Functions are powerful tools for code organization and reusability. They encapsulate specific tasks and allow you to break down complex operations into manageable parts. In Arduino, you can employ both built-in functions and create your custom functions.

### Creating Custom Functions:

```arduino
void turnOnLED() {
  digitalWrite(ledPin, HIGH); // Turns on the LED
}
```

Here, 'turnOnLED' is a custom function that activates an LED when called. Functions enhance code organization, readability, and the ability to reuse code for different parts of your project.
Additional Example - Function with Parameters:

```arduino
int add(int a, int b) {
  return a + b; // Adds two numbers and returns the result
}
```

This example showcases a function 'add' that takes two integers as input and returns their sum. Functions with parameters allow you to create versatile and adaptable code.

## Libraries:
Libraries are treasure troves of pre-written code that simplify complex tasks. They provide functions and tools for various hardware components. In your Arduino projects, you can include libraries to save time and effort.

Example:
```arduino
#include <Servo.h> // Include the Servo library

Servo myservo; // Create a Servo object

void setup() {
  myservo.attach(9); // Attach the servo to pin 9
}

void loop() {
  myservo.write(90); // Set the servo to the middle position (90 degrees)
  delay(1000); // Wait for 1 second
  myservo.write(0); // Set the servo to the minimum position (0 degrees)
  delay(1000); // Wait for 1 second
}
```

In this example, we include the Servo library to control a servo motor effortlessly. Libraries provide pre-written functions like 'attach' and 'write,' making complex tasks more accessible and allowing you to focus on the specific features of your project.

## Example 1: LED Blink
Cover:
In this project, you'll make an LED blink on and off. It's like making a tiny light bulb turn on and off with your code.

```arduino
int ledPin = 13; // Define the LED pin

void setup() {
  pinMode(ledPin, OUTPUT); // Set the LED pin as an output
}

void loop() {
  digitalWrite(ledPin, HIGH); // Turn on the LED
  delay(1000); // Wait for 1 second
  digitalWrite(ledPin, LOW); // Turn off the LED
  delay(1000); // Wait for 1 second
}
```

## Example 2: Button Press
Cover:
In this project, you'll make something happen when you press a button. It's like magic – press a button, and something changes!

```arduino
int buttonPin = 2; // Define the button pin
int ledPin = 13; // Define the LED pin

void setup() {
  pinMode(ledPin, OUTPUT); // Set the LED pin as an output
  pinMode(buttonPin, INPUT); // Set the button pin as an input
}

void loop() {
  int buttonState = digitalRead(buttonPin); // Read the button state

  if (buttonState == HIGH) {
    digitalWrite(ledPin, HIGH); // Turn on the LED when the button is pressed
  } else {
    digitalWrite(ledPin, LOW); // Turn off the LED when the button is released
  }
}
```

These simplified examples will help you get comfortable with Arduino programming and set the stage for more exciting projects.
