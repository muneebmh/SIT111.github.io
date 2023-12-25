# Interfacing with Sensors

Welcome to Module 2.2, where we'll delve deep into the exciting world of interfacing with sensors using your Arduino. Sensors are the sensory organs of your projects, allowing your Arduino to interact with and respond to the physical world.

# Connecting and Reading Data from Common Sensors

## Understanding Sensors:

Sensors, essential components in the world of electronics and automation, play a pivotal role in detecting and quantifying a wide range of physical properties in the environment. These properties encompass crucial factors such as temperature, humidity, light levels, distance, and more. In this section, we delve into several common sensors suitable for Arduino projects. 
Examples of common sensors for Arduino projects:
+ DS18B20: Measures temperature with high accuracy.
+ DHT22: Measures temperature and humidity simultaneously.
+ HC-SR04: Utilizes sound waves for distance measurement.
+ BH1750: Monitors ambient light levels.
Further, we will explore sensors, detailing their connections and programming, enabling you to incorporate them effectively into your Arduino projects.

## Temperature Sensor (e.g., DHT22):

Temperature and humidity sensors, like the DHT22, are widely utilized for measuring ambient temperature and relative humidity levels. These sensors find extensive applications in climate control, weather monitoring, and environmental data collection due to their precision and reliability.

### Example:
We will connect a DHT22 temperature and humidity sensor to your Arduino and learn how to read temperature and humidity data:
![Figure 2 21](https://github.com/muneebmh/SIT111.github.io/assets/149995551/51037fbd-bcf9-40e1-a168-fe5b4d1d4abc)

*Figure 2.21 Connection Diagram for DHT22 Sensor (Source: https://www.ardumotive.com/how-to-use-dht-22-sensor-en.html)*

```cpp
//Libraries
#include <dht.h>
dht DHT;
//Constants
#define DHT22_PIN 2     // DHT 22  (AM2302) - what pin we're connected to

//Variables
float hum;  //Stores humidity value
float temp; //Stores temperature value

void setup()
{
    Serial.begin(9600);
}

void loop()
{
    int chk = DHT.read22(DHT22_PIN);
    //Read data and store it to variables hum and temp
    hum = DHT.humidity;
    temp= DHT.temperature;
    //Print temp and humidity values to serial monitor
    Serial.print("Humidity: ");
    Serial.print(hum);
    Serial.print(" %, Temp: ");
    Serial.print(temp);
    Serial.println(" Celsius");
    delay(2000); //Delay 2 sec.
}
```

This example demonstrates how to connect a DHT11 temperature and humidity sensor to your Arduino and retrieve temperature and humidity data.

## Soil Moisture Sensor :
The Soil Moisture Sensor, designed for compatibility with Arduino, serves as an essential component for monitoring soil moisture levels. This sensor is particularly valuable in agricultural applications, garden automation, and environmental sensing.

### Example:
You can connect a Soil Moisture Sensor to your Arduino and collect data on soil moisture for various purposes, such as automated watering systems or soil health monitoring. Here's an example of how to use it:
![Figure 2 22](https://github.com/muneebmh/SIT111.github.io/assets/149995551/5740d3b3-4e86-4612-ac4a-9c8fd32a11cf)

*Figure 2.22 Connection Diagram of Soil Moisture with Arduino (Source: https://www.electronicwings.com/arduino/soil-moisture-sensor-interfacing-with-arduino-uno)*

```cpp
const int sensor_pin = A1;	/* Soil moisture sensor O/P pin */

void setup() {
  Serial.begin(9600);	/* Define baud rate for serial communication */
}

void loop() {
  float moisture_percentage;
  int sensor_analog;
  sensor_analog = analogRead(sensor_pin);
  moisture_percentage = ( 100 - ( (sensor_analog/1023.00) * 100 ) );
  Serial.print("Moisture Percentage = ");
  Serial.print(moisture_percentage);
  Serial.print("%\n\n");
  delay(1000);
}
```


# Integrating Actuators and Understanding Output Control

## Actuators and Output Control:
Actuators represent a crucial component within the realm of automation and control systems, serving as the dynamic agents that bridge the gap between the digital world of data and the physical realm of actions. These devices operate as the responsive force that interprets signals or data emanating from sensors, translating them into tangible actions with precision and purpose. The spectrum of these actions is remarkably diverse, encompassing elementary functions such as illuminating an LED in response to environmental changes or executing intricate maneuvers to control the movements of robotic arms in industrial automation scenarios. Whether it's a humble LED, a motor, a solenoid, or a complex mechanical system, actuators serve as the embodiment of automation, enabling machines and systems to interact with and manipulate the physical world, thereby unlocking a vast array of applications across industries, from home automation to manufacturing and beyond.
In this section, we'll explore how to integrate actuators into your projects and understand output control.

### LEDs:
Light Emitting Diodes (LEDs) are a fundamental component for visual output in your projects. You can control LEDs to display information, create visual indicators, or add illumination.

#### Example:
Let's create a project where an LED blinks when the temperature goes above certain thresholds:

![Figure 2 23](https://github.com/muneebmh/SIT111.github.io/assets/149995551/8feffe13-c5dd-4184-a7c0-bb4f29afa97a)

*Figure 2.23 Schematic Diagram for DHT22 with LEDS (Source: https://www.hackster.io/IreuN/dht22-setup-with-simple-error-checking-cdc67a)*

```cpp
// Example testing sketch for various DHT humidity/temperature sensors
// Written by ladyada, public domain

#include "DHT.h"

#define DHTPIN 2     // what digital pin we're connected to

#define DHTTYPE DHT22

DHT dht(DHTPIN, DHTTYPE);

void setup() {
	Serial.begin(9600);
	Serial.println("Reading DHT22 data!");
	dht.begin();
	pinMode(12, OUTPUT); // Green
	pinMode(11, OUTPUT); // Red
}

void loop() {
	// Reading temperature or humidity takes about 250 milliseconds!
	// Sensor readings may also be up to 2 seconds 'old' (its a very slow sensor)
	float hum1 = dht.readHumidity();
	// Read temperature as Celsius
	float temp1 = dht.readTemperature();


	// Check if any reads failed and exit early (to try again).
	if (isnan(hum1) || isnan(temp1)) {
		digitalWrite(11, HIGH);
		digitalWrite(12, LOW);
		Serial.println("Error in reading sensor data!");
		while (isnan(hum1) || isnan(temp1)) {
			hum1 = dht.readHumidity();
			temp1 = dht.readTemperature();
		}
	}
	else {
		digitalWrite(11, LOW);
		digitalWrite(12, HIGH);
	}

	// Wait a few seconds between measurements.
	delay(3000);
	float hum2 = dht.readHumidity();
	float temp2 = dht.readTemperature();

	// Compute heat index in Celsius (isFahreheit = false)
	float hic = dht.computeHeatIndex(temp1, hum1, false);
	Serial.print("Humidity: ");
	Serial.print(round)(hum1 + hum2) / 2));
	Serial.print(" % ");
	Serial.print("Temperature: ");
	Serial.print((temp1 + temp2) / 2);
	Serial.print(" *C ");
	Serial.print("Heat index: ");
	Serial.print(round(hic));
	Serial.println(" *C ");
}

```

In this example, we use an LED as an actuator to indicate when the temperature goes above specified thresholds.

# Advanced Sensor Integration
In this section, we will take our journey into sensor integration to the next level by delving even deeper into the world of advanced sensors.

## Interfacing with More Advanced Sensors
### Advanced Sensors:
In this section, we'll explore more advanced sensors that expand the capabilities of your Arduino projects. These sensors offer greater precision and can measure a wider range of physical properties.
+ **Ultrasonic Sensor (e.g., HC-SR04):** Measures distance via ultrasonic waves, suitable for obstacle avoidance in robotics and precise distance measurement.
+ **IR Sensor (e.g., IR Receiver Module):** Detects infrared signals, ideal for remote control applications, infrared communication, and automation systems.

#### Example 1: Distance-Dependent LED Indicator with Ultrasonic Sensor
This code snippet establishes a distance-dependent LED indicator system using an ultrasonic sensor. It configures the Arduino with multiple LEDs, each associated with a specific distance threshold. The ultrasonic sensor continuously measures distances, and based on the detected distance from an object, individual LEDs are illuminated accordingly. For instance, if the distance is greater than or equal to 10 centimeters, LED1 lights up, and this pattern continues for LEDs 2 through 10 at varying distance thresholds. This project is a valuable foundation for creating proximity-based visual indicators, such as parking assist systems or interactive displays, where LED status corresponds to the proximity of objects in the sensor's range.

![Figure 2 23](https://github.com/muneebmh/SIT111.github.io/assets/149995551/f29d8eba-9b86-4f05-8945-b30e3acfce34)


*Figure 2.23 Schematic Diagram for Distance-Dependent LED Indicator with Ultrasonic Sensor (Source: https://www.hackster.io/brillianttechnoz/led-distance-measurement-using-ultrasonic-sensor-and-aurdino-4480f6)*

```cpp
int trig = 10;
int echo = 11;
int led1 = 13;
int led2 = 12;
int led3 = 9;
int led4 = 8;
int led5 = 7;
int led6 = 6;
int led7 = 5;
int led8 = 4;
int led9 = 3;
int led10 = 2;


void setup() {
  // put your setup code here, to run once:
  pinMode(13, OUTPUT);
  pinMode(12, OUTPUT);
  pinMode(11, INPUT);
  pinMode(10, OUTPUT);
  pinMode(9, OUTPUT);
  pinMode(8, OUTPUT);
  pinMode(7, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(5, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(2, OUTPUT);
}

void loop() {
  // put your main code here, to run repeatedly:
  long duration, distance;
  digitalWrite(trig, LOW);
  delayMicroseconds(2);
  digitalWrite(trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(trig, LOW);
  duration = pulseIn(echo, HIGH);
  distance = (duration / 2) / 29.1;

  if (distance >= 10)
  {
    digitalWrite(led1, HIGH);
  }
  else
  {
    digitalWrite(led1, LOW);
  }

  if (distance >= 20)
  {
    digitalWrite(led2, HIGH);
  }
  else
  {
    digitalWrite(led2, LOW);
  }

  if (distance >= 30)
  {
    digitalWrite(led3, HIGH);
  }
  else
  {
    digitalWrite(led3, LOW);
  }

  if (distance >= 40)
  {
    digitalWrite(led4, HIGH);
  }
  else
  {
    digitalWrite(led4, LOW);
  }

  if (distance >= 50)
  {
    digitalWrite(led5, HIGH);
  }
  else
  {
    digitalWrite(led5, LOW);
  }

  if (distance >= 60)
  {
    digitalWrite(led6, HIGH);
  }
  else
  {
    digitalWrite(led6, LOW);
  }

  if (distance >= 70)
  {
    digitalWrite(led7, HIGH);
  }
  else
  {
    digitalWrite(led7, LOW);
  }

  if (distance >= 80)
  {
    digitalWrite(led8, HIGH);
  }
  else
  {
    digitalWrite(led8, LOW);
  }

  if (distance >= 90)
  {
    digitalWrite(led9, HIGH);
  }
  else
  {
    digitalWrite(led9, LOW);
  }

  if (distance >= 100)
  {
    digitalWrite(led10, HIGH);
  }
  else
  {
    digitalWrite(led10, LOW);
  }

}

```

