# ----------- Module 2: Arduino Programming Basics ---------------

Welcome to the next Module, where we'll embark on a comprehensive journey into the fundamental concepts of Arduino programming. In this section, "Arduino Programming Basics," we'll dive deep into the core elements that form the foundation of successful Arduino projects.

# Basics of the C/C++ Language for Arduino

## Understanding the C/C++ Language:
The Arduino programming environment is built upon a simplified version of the C/C++ programming language. To wield the full potential of Arduino, it's crucial to grasp the fundamental aspects:

### Variables and Data Types:
Variables are essential components of programming, allowing you to store and manipulate data. In Arduino, you'll frequently utilize various data types to declare variables:
+ **int (Integer):** The integer data type is instrumental for working with whole numbers. It's ideal for situations where you need to represent quantities that don't involve fractional or decimal values. For example, when measuring sensor readings like temperature in degrees Celsius, you'd typically use an integer variable to store the result because temperatures are often whole numbers (e.g., 25°C).
+ **float (Floating-Point):** UFloating-point data types are employed when precision with decimal point values is required. These data types accommodate real numbers with fractional parts. In scenarios where you need to deal with measurements involving decimal values, such as sensor readings for humidity (e.g., 56.7%), float variables are the go-to choice for retaining accuracy and granularity.
+ **char (Character):** The character data type is used for storing individual characters, which can be letters, numbers, or symbols. It's invaluable when working with strings or textual data. For instance, if you want to store a single letter like 'A' or a punctuation mark like '?' for textual processing, char variables provide the means to do so efficiently.
+ **boolean:** ooleans are essential when dealing with binary logic and conditions. They represent either a true or false value, making them indispensable for decision-making in control structures like if statements. In Arduino, boolean variables are frequently used to control the flow of the program based on certain conditions. For instance, you might use a boolean variable to determine if a sensor reading is within a specified range (true) or outside it (false), triggering specific actions accordingly.
  
```cpp
int age = 25; // Declares an integer variable 'age'
float temperature = 25.5; // Declares a float variable 'temperature'
char initial = 'A'; // Declares a character variable 'initial'
boolean isOn = true; // Declares a boolean variable 'isOn'
```

These examples demonstrate the use of various data types to represent different types of information.

### Control Structures:
Control structures are the backbone of any program, allowing you to make decisions and control the flow of your Arduino program. Some common control structures include:
+ **if statement:** The **if** statement is a cornerstone of conditional execution. It enables your Arduino program to assess a given condition and, if that condition is true, execute a predefined set of instructions. For example, you can employ an if statement to check whether a sensor reading exceeds a predetermined threshold. If the condition holds true, specific actions can be taken, such as triggering an alarm or adjusting a motor's speed.
+ **else statement:** Complementing the **if** statement, the **else** statement provides an alternative course of action when the condition evaluated by if is found to be false. This dual structure permits your program to encompass both primary and alternative pathways, enhancing its responsiveness to varying scenarios. For instance, if an infrared sensor detects an obstacle (true condition), the **if** block can initiate braking in a robot, while the **else** block can initiate a different action, like changing direction or sounding an alert, when no obstacle is detected (false condition).
+ **loops (e.g., for, while):** Loops are indispensable for automating repetitive tasks and executing code iteratively. Arduino offers versatile loop structures, including the **for** and **while** loops. A for loop, for instance, allows you to execute a block of code a specified number of times, making it invaluable for tasks like data acquisition at regular intervals. Conversely, a **while** loop keeps executing as long as a given condition remains true, facilitating continuous monitoring and control. For example, you can use a **while** loop to continuously monitor a temperature sensor until a specific temperature is reached before initiating a cooling mechanism.

```cpp
// Arduino Example: Using an if statement

const int buttonPin = 2;  // Define the button pin
const int ledPin = 13;    // Define the LED pin

void setup() {
  pinMode(buttonPin, INPUT);  // Set the button pin as an input
  pinMode(ledPin, OUTPUT);    // Set the LED pin as an output
}

void loop() {
  if (digitalRead(buttonPin) == HIGH) {  // Check if the button is pressed
    digitalWrite(ledPin, HIGH);          // Turn on the LED
  } else {
    digitalWrite(ledPin, LOW);           // Turn off the LED
  }
}

```

This example illustrates an 'if' statement controlling a fan based on the temperature. Control structures are pivotal for creating dynamic and responsive Arduino projects.

# Functions and Libraries in Arduino Programming

## Functions:
Functions are pivotal in Arduino programming for code organization and reusability. These constructs enable the encapsulation of specific tasks, breaking down complex operations into modular components. Arduino programmers leverage both built-in functions, covering a wide range of functionalities, and user-defined functions tailored to project-specific requirements. Custom functions enhance code readability and maintenance by encapsulating sequences of instructions within named entities, promoting modularity and reusability. 

### Creating Custom Functions:

Simple function example:
```cpp
void turnOnLED() {
  digitalWrite(ledPin, HIGH); // Turns on the LED
}
```

Here, 'turnOnLED' is a custom function that activates an LED when called. Functions enhance code organization, readability, and the ability to reuse code for different parts of your project.

Additional Example - Function with Parameters:

```cpp
int add(int a, int b) {
  return a + b; // Adds two numbers and returns the result
}
```

This example showcases a function 'add' that takes two integers as input and returns their sum. Functions with parameters allow you to create versatile and adaptable code.


#### Using and Calling Function

![Figure 2 11](https://github.com/muneebmh/SIT111.github.io/assets/149995551/629473f2-1bdf-4cd3-8459-26416f73ef5b)

 *Figure 2.11 Anatomy of Simple Arduino Function (Source: https://docs.arduino.cc/learn/programming/functions)*

To "call" our simple multiply function, we pass it parameters of the datatype that it is expecting:

```cpp
void loop(){
int i = 2;
int j = 3;
int k;

k = myMultiplyFunction(i, j); // k now contains 6
}
```



#### Functions in Real-Life Scenarios

Imagine you're building a simple Arduino-based temperature monitoring system. You want to display the temperature on an LCD screen and also send it via serial communication to your computer. To achieve this, you can create two functions:

+ **readTemperature():** This function reads the temperature from a sensor and returns the temperature value.

+ **displayTemperature():** This function takes the temperature value as an argument and displays it on the LCD screen and sends it via serial communication.

```cpp
#include <LiquidCrystal.h>

// Initialize the LCD screen
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

// Pin for the temperature sensor
const int temperatureSensorPin = A0;

void setup() {
  // Initialize LCD
  lcd.begin(16, 2);

  // Start serial communication
  Serial.begin(9600);
}

void loop() {
  // Read temperature from the sensor
  float temperature = readTemperature();

  // Display and send temperature data
  displayTemperature(temperature);

  // Delay for a moment
  delay(1000);
}

float readTemperature() {
  // Read the analog value from the temperature sensor
  int sensorValue = analogRead(temperatureSensorPin);

  // Convert the analog value to temperature in degrees Celsius
  float temperatureCelsius = (sensorValue / 1023.0) * 100.0;

  return temperatureCelsius;
}

void displayTemperature(float temperature) {
  // Display temperature on LCD
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Temp: ");
  lcd.print(temperature);
  lcd.print(" C");

  // Send temperature data via serial communication
  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.println(" C");
}
```

By creating these functions, you can easily reuse them throughout your program. For instance, you can call readTemperature() whenever you need to acquire temperature data, and displayTemperature() whenever you want to show or transmit the temperature value. This modular approach simplifies your code, makes it more readable, and allows you to efficiently manage temperature-related tasks within your Arduino project.

## Libraries:
Libraries in Arduino are like expert toolkits, packed with pre-written code that acts as shortcuts to simplify challenging tasks. They serve as comprehensive collections of functions and tools tailored for a wide range of hardware components. In your practical Arduino projects, leveraging libraries is akin to having a skilled assistant, saving you valuable time and effort while ensuring the reliability of your code.

### Examples:

#### Example # 01:
Imagine you're working on a basic Arduino project that involves controlling an RGB LED to display different colors. Instead of manually defining the RGB color values, you can use the "Adafruit NeoPixel" library to simplify the process. This library provides pre-written functions to control NeoPixel (WS2812) RGB LEDs. You can set colors by calling functions like setPixelColor() and show().

```cppp
#include <Adafruit_NeoPixel.h>

// Define the pin where the NeoPixel strip is connected
#define PIN 6

// Define the number of NeoPixels in the strip
#define NUMPIXELS 8

// Create an Adafruit_NeoPixel object
Adafruit_NeoPixel strip = Adafruit_NeoPixel(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);

void setup() {
  // Initialize the NeoPixel strip
  strip.begin();
  strip.show(); // Initialize all pixels to 'off'
}

void loop() {
  // Set the color of all NeoPixels to red
  colorWipe(strip.Color(255, 0, 0), 50); // Red color, 50ms delay

  // Set the color of all NeoPixels to green
  colorWipe(strip.Color(0, 255, 0), 50); // Green color, 50ms delay

  // Set the color of all NeoPixels to blue
  colorWipe(strip.Color(0, 0, 255), 50); // Blue color, 50ms delay
}

// Fill the dots one after the other with a color
void colorWipe(uint32_t color, int wait) {
  for (int i = 0; i < strip.numPixels(); i++) {
    strip.setPixelColor(i, color);
    strip.show();
    delay(wait);
  }
}
```

By using this library, you can create colorful lighting effects with minimal effort, making your project more accessible and efficient. This simple example highlights how libraries can simplify even the most basic tasks in Arduino projects, allowing you to achieve your goals with ease.

#### Example # 02:

This Arduino program leverages the "Servo" library to control a servo motor. It begins by including the library and creating a Servo object named myservo. In the setup() function, the servo is initialized and attached to a specific pin on the Arduino. The core servo control occurs within the loop() function, where the program commands the servo to rotate to specific positions using the myservo.write() function from the library. Intervals of 1-second delays are introduced to pause the servo at these positions, creating a repetitive back-and-forth motion. The "Servo" library streamlines servo motor control by providing pre-defined functions for angle positioning, enhancing the efficiency of this Arduino-based servo control application.

```cpp
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


## Other Arduino Examples: 

In the last week, we explored Blinky example. In this week, we will cover a few more basic examples:

### Example (Blink Without Delay):

In certain scenarios where multitasking is essential, such as simultaneously monitoring a button press while blinking an LED, the standard Arduino delay() function proves inadequate as it halts program execution, potentially causing missed events like button presses. This tutorial introduces an alternative method for LED blinking devoid of delay(). It begins by illuminating the LED and recording the time. During each iteration of the loop() function, it assesses if the prescribed time interval has elapsed. If affirmative, it toggles the LED state and updates the time, ensuring continuous LED blinking without any single instruction causing execution delays. Drawing an analogy to real-life multitasking, akin to microwaving a pizza while awaiting an important email, the tutorial elucidates the concept further. By the end, readers will possess the know-how to implement a similar timer mechanism, enabling responsive and concurrent task execution in Arduino programming.

![Figure 2 12](https://github.com/muneebmh/SIT111.github.io/assets/149995551/ae89f422-13d2-4393-929b-f3ddd63ee31d)
(Figure 2.12 Schematic for Blink without Delay (Source: Arduino Examples)*

```cpp
// constants won't change. Used here to set a pin number:
const int ledPin = LED_BUILTIN;  // the number of the LED pin

// Variables will change:
int ledState = LOW;  // ledState used to set the LED

// Generally, you should use "unsigned long" for variables that hold time
// The value will quickly become too large for an int to store
unsigned long previousMillis = 0;  // will store last time LED was updated

// constants won't change:
const long interval = 1000;  // interval at which to blink (milliseconds)

void setup() {
  // set the digital pin as output:
  pinMode(ledPin, OUTPUT);
}

void loop() {
  // here is where you'd put code that needs to be running all the time.

  // check to see if it's time to blink the LED; that is, if the difference
  // between the current time and last time you blinked the LED is bigger than
  // the interval at which you want to blink the LED.
  unsigned long currentMillis = millis();

  if (currentMillis - previousMillis >= interval) {
    // save the last time you blinked the LED
    previousMillis = currentMillis;

    // if the LED is off turn it on and vice-versa:
    if (ledState == LOW) {
      ledState = HIGH;
    } else {
      ledState = LOW;
    }

    // set the LED with the ledState of the variable:
    digitalWrite(ledPin, ledState);
  }
}
```

## Example 2: Button Press
Cover:
To wire and program a button for Arduino, connect one leg of the button to a digital pin (e.g., Pin 2) and the other leg to the ground (GND) pin on the Arduino, while also including a 10kΩ resistor between the button and the 5V output. In your Arduino code, define the button pin as an input using pinMode(), and in the loop() function, utilize digitalRead() to check the button's state. When the button is pressed (HIGH), execute the desired actions using conditional statements. This straightforward process enables you to integrate button functionality into your Arduino projects with ease.

![Figure 2 13](https://github.com/muneebmh/SIT111.github.io/assets/149995551/288b5947-8710-4540-ae65-ee7b740977c5)
 
 (Figure 2.13 Schematic for Arduino Button (Source: Arduino Examples)*

```cpp
// constants won't change. They're used here to set pin numbers:
const int buttonPin = 2;  // the number of the pushbutton pin
const int ledPin = 13;    // the number of the LED pin

// variables will change:
int buttonState = 0;  // variable for reading the pushbutton status

void setup() {
  // initialize the LED pin as an output:
  pinMode(ledPin, OUTPUT);
  // initialize the pushbutton pin as an input:
  pinMode(buttonPin, INPUT);
}

void loop() {
  // read the state of the pushbutton value:
  buttonState = digitalRead(buttonPin);

  // check if the pushbutton is pressed. If it is, the buttonState is HIGH:
  if (buttonState == HIGH) {
    // turn LED on:
    digitalWrite(ledPin, HIGH);
  } else {
    // turn LED off:
    digitalWrite(ledPin, LOW);
  }
}

```

These simplified examples will help you get comfortable with Arduino programming and set the stage for more exciting projects.
