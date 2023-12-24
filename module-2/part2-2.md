# Interfacing with Sensors

Welcome to Module 2.2, where we'll delve deep into the exciting world of interfacing with sensors using your Arduino. Sensors are the sensory organs of your projects, allowing your Arduino to interact with and respond to the physical world.

# Connecting and Reading Data from Common Sensors

## Understanding Sensors:

Sensors are electronic devices that can detect and measure physical properties in the environment. These properties can include temperature, humidity, light levels, distance, and much more. In this section, we will explore some common sensors and learn how to connect them to your Arduino.

## Temperature Sensor (e.g., DHT11):

Temperature sensors, such as the DHT11, are widely used to measure ambient temperature and humidity levels. These sensors are particularly useful for climate control, weather monitoring, and environmental data collection.

### Example:
We will connect a DHT11 temperature and humidity sensor to your Arduino and learn how to read temperature and humidity data:

```cpp
#include <DHT.h> // Include the DHT library

#define DHTPIN 2 // Define the digital pin to which the sensor is connected
#define DHTTYPE DHT11 // Define the type of sensor (DHT11 or DHT22)

DHT dht(DHTPIN, DHTTYPE); // Create a DHT object

void setup() {
  Serial.begin(9600); // Initialize serial communication
  dht.begin(); // Initialize the sensor
}

void loop() {
  float temperature = dht.readTemperature(); // Read temperature data
  float humidity = dht.readHumidity(); // Read humidity data

  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.println(" °C");

  Serial.print("Humidity: ");
  Serial.print(humidity);
  Serial.println("%");

  delay(2000); // Delay for 2 seconds before the next reading
}
```

This example demonstrates how to connect a DHT11 temperature and humidity sensor to your Arduino and retrieve temperature and humidity data.

## Light Sensor (e.g., LDR):
Light-dependent resistors (LDRs) are sensors that change resistance based on the amount of light they detect. They are commonly used in applications like automatic lighting control and ambient light sensing.

## Humidity Sensor (e.g., DHT11):
Humidity sensors, like the DHT11, are essential for monitoring and controlling humidity levels in environments such as greenhouses, weather stations, and HVAC systems.

# Integrating Actuators and Understanding Output Control

## Actuators and Output Control:
Actuators are devices that receive signals or data from sensors and perform actions based on that input. These actions can range from simple tasks like turning on an LED to more complex movements like controlling a robotic arm.
In this section, we'll explore how to integrate actuators into your projects and understand output control.

### LEDs:
Light Emitting Diodes (LEDs) are a fundamental component for visual output in your projects. You can control LEDs to display information, create visual indicators, or add illumination.

#### Example:
Let's create a project where an LED blinks when the temperature goes above a certain threshold:

```cpp
int temperaturePin = A0; // Define the analog pin for temperature sensor
int ledPin = 13; // Define the LED pin

void setup() {
  pinMode(ledPin, OUTPUT); // Set the LED pin as an output
  pinMode(temperaturePin, INPUT); // Set the temperature sensor pin as an input
}

void loop() {
  int temperatureValue = analogRead(temperaturePin); // Read temperature sensor value

  if (temperatureValue > 25) {
    digitalWrite(ledPin, HIGH); // Turn on the LED if temperature is above 25°C
  } else {
    digitalWrite(ledPin, LOW); // Turn off the LED otherwise
  }
}
```

In this example, we use an LED as an actuator to indicate when the temperature goes above a specified threshold.

# Advanced Sensor Integration
Welcome to Module 2.4, where we'll dive even deeper into sensor integration, exploring more advanced sensors and understanding the principles of sensor fusion.
## Interfacing with More Advanced Sensors
### Advanced Sensors:
In this section, we'll explore more advanced sensors that expand the capabilities of your Arduino projects. These sensors offer greater precision and can measure a wider range of physical properties.
+ **Ultrasonic Sensor (e.g., HC-SR04):** Measures distance using ultrasonic waves.
+ **IR Sensor (e.g., IR Receiver Module):** Detects infrared signals from remote controls and other devices.

#### Example 1: Distance Measurement with HC-SR04 Ultrasonic Sensor
The HC-SR04 ultrasonic sensor is widely used for measuring distance. In this example, we'll interface the HC-SR04 sensor with your Arduino and create a distance measurement project.

```cpp
const int trigPin = 9; // Trigger pin of the HC-SR04
const int echoPin = 10; // Echo pin of the HC-SR04

void setup() {
  Serial.begin(9600); // Initialize serial communication
  pinMode(trigPin, OUTPUT); // Set the trigger pin as an output
  pinMode(echoPin, INPUT); // Set the echo pin as an input
}

void loop() {
  digitalWrite(trigPin, LOW); // Ensure the trigger pin is low
  delayMicroseconds(2); // Wait for 2 microseconds
  
  digitalWrite(trigPin, HIGH); // Send a 10 microsecond pulse to trigger the sensor
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  long duration = pulseIn(echoPin, HIGH); // Measure the duration of the echo pulse
  float distance_cm = duration * 0.034 / 2; // Calculate distance in centimeters

  Serial.print("Distance: ");
  Serial.print(distance_cm);
  Serial.println(" cm");
  
  delay(1000); // Delay for 1 second before the next measurement
}

```

This example demonstrates how to measure distance using the HC-SR04 ultrasonic sensor and display the results on the serial monitor.
