# Data Logging and Storage

Welcome to Module 3.2, where we will explore the exciting world of data logging and storage with Arduino. In this section, you will learn the importance of storing sensor data on external storage devices, gain an overview of data logging techniques, and understand the real-world applications of data storage in various fields.

# Introduction to Storing Sensor Data
## The Significance of Data Storage:
In today's digital age, data is a valuable asset. Storing sensor data is critical in numerous applications, including environmental monitoring, scientific research, and industrial automation. Arduino can be a powerful tool for collecting and recording data from sensors.
External Storage Devices: Arduino can interface with various external storage devices like SD cards, EEPROM (Electrically Erasable Programmable Read-Only Memory), and even cloud-based services for data storage.
### Example: Storing Temperature Data on an SD Card

This experiment demonstrates how to create a data logger using an Arduino and an SD card module to record temperature sensor data. By interfacing the Arduino with the temperature sensor and configuring it to write data onto the SD card, users can collect and store temperature readings for further analysis and monitoring.

![Figure 3 21](https://github.com/muneebmh/SIT111.github.io/assets/149995551/00faa3ad-e52b-44a1-b592-0b460979e2bb)

*Figure 3.21 Schematic Diagram for Integration of SD Card with Arduino (Source: https://maker.pro/arduino/tutorial/how-to-make-an-arduino-sd-card-data-logger-for-temperature-sensor-data)*

```cpp
#include <SD.h>
#include <SPI.h>
#include <DS3231.h>
File sdcard_file;
DS3231  rtc(SDA, SCL);
int CS_pin = 10; // Pin 10 on Arduino Uno
const int sensor_pin = A0;
float temp;  
float output;

void setup() {
  Serial.begin(9600);
  pinMode(sensor_pin,INPUT);
  pinMode(CS_pin, OUTPUT);
  rtc.begin(); 
  // SD Card Initialization
  if (SD.begin())
  {
    Serial.println("SD card is ready to use.");
  } else
  {
    Serial.println("SD card initialization failed");
    return;
  }
  
  Serial.print("Date  ");   
  Serial.print("      ");
  Serial.print("   Time  ");
  Serial.print("     ");
  Serial.print("   Temp   ");
  Serial.println("     ");
  sdcard_file = SD.open("data.txt", FILE_WRITE);
  if (sdcard_file) { 
    sdcard_file.print("Date  ");   
    sdcard_file.print("      ");
    sdcard_file.print("   Time  ");
    sdcard_file.print("     ");
    sdcard_file.print("   Temp   ");
    sdcard_file.println("     ");
    sdcard_file.close(); // close the file
  }
  // if the file didn't open, print an error:
  else {
    Serial.println("error opening test.txt");
  }
}

void loop() {
  output = analogRead(sensor_pin);
  temp =(output*500)/1023;
  Serial.print(rtc.getDateStr());
  Serial.print("     ");
  Serial.print(rtc.getTimeStr());
  Serial.print("      ");
  Serial.println(temp);
 
  sdcard_file = SD.open("data.txt", FILE_WRITE);
  if (sdcard_file) {    
    sdcard_file.print(rtc.getTimeStr());
    sdcard_file.print("     ");   
    sdcard_file.print(rtc.getTimeStr());
    sdcard_file.print("     ");
    sdcard_file.println(temp);
    sdcard_file.close(); // close the file
  }
  // if the file didn't open, print an error:
  else {
    Serial.println("error opening test.txt");
  }
  delay(3000);
}
```
This Arduino code is used to create a temperature data logger system that records temperature readings with timestamps to an SD card. It utilizes an Arduino Uno, a DS3231 real-time clock module for timekeeping, and an SD card module for data storage. In the setup, it initializes hardware components, checks SD card availability, and prepares the data file with a header. The loop function continuously reads the analog temperature sensor, calculates temperature values, retrieves date and time information from the DS3231 module, and logs this data to the "data.txt" file on the SD card. With a 3-second delay between readings, it provides a simple yet effective solution for temperature data collection and monitoring.

# Overview of Data Logging Techniques
## Data Logging Methods:

Data logging involves the process of collecting data from sensors or other sources and storing it for future analysis. Various techniques can be employed for data logging, depending on the application.
+ **Continuous Logging:** This method involves regularly recording data at predefined intervals, making it suitable for applications like environmental monitoring, where you need to track changes in conditions over time. For example, you can log temperature data every minute to observe daily temperature fluctuations.
+ **Event-Based Logging:** Event-based logging is triggered by specific events or conditions. In Arduino, this is valuable when you want to capture data only when certain events occur. For instance, you can log sensor data when a motion detector detects movement or when a threshold value is exceeded, such as monitoring soil moisture and recording data only when it falls below a certain level.

### Example: Continuous Data Logging

```cpp
#include <SD.h>
#include <SPI.h>
#include <DHT.h>

#define DHTPIN 2           // Define the pin where your DHT sensor is connected
#define DHTTYPE DHT22      // Define the type of DHT sensor (DHT11 or DHT22)
#define CS_PIN 4            // Define the chip select pin for the SD card module

DHT dht(DHTPIN, DHTTYPE);   // Create a DHT object
File dataFile;              // Create a File object for data logging

void setup() {
  Serial.begin(9600);
  dht.begin();             // Initialize the DHT sensor
  
  // Initialize SD card
  if (SD.begin(CS_PIN)) {
    Serial.println("SD card is ready to use.");
  } else {
    Serial.println("SD card initialization failed.");
    while (1); // Halt the program if SD card initialization fails
  }
  
  // Open or create a file for data logging
  dataFile = SD.open("datalog.txt", FILE_WRITE);
  if (dataFile) {
    Serial.println("Data logging initialized.");
    dataFile.close(); // Close the file
  } else {
    Serial.println("Error opening datalog.txt");
  }
}

void loop() {
  float humidity = readHumidity();
  float temperature = readTemperature();

  Serial.print("Humidity (%): ");
  Serial.println(humidity);
  Serial.print("Temperature (°C): ");
  Serial.println(temperature);

  // Log data to the SD card
  dataFile = SD.open("datalog.txt", FILE_WRITE);
  if (dataFile) {
    dataFile.print("Humidity (%): ");
    dataFile.println(humidity);
    dataFile.print("Temperature (°C): ");
    dataFile.println(temperature);
    dataFile.close(); // Close the file
  } else {
    Serial.println("Error opening datalog.txt");
  }

  // Delay for 1 minute before logging the next data point
  delay(60000);
}

float readHumidity() {
  float humidity = dht.readHumidity(); // Read humidity from the DHT sensor
  return humidity;
}

float readTemperature() {
  float temperature = dht.readTemperature(); // Read temperature from the DHT sensor
  return temperature;
}

```
This Arduino code is designed to continuously collect humidity and temperature data from a DHT22 sensor and log it onto an SD card. It initializes the necessary components, including the DHT sensor and SD card module, then reads the sensor data, displays it on the Serial Monitor for real-time monitoring, and simultaneously writes it to a file called "datalog.txt" on the SD card. The code runs in a loop, periodically recording data at one-minute intervals, making it a practical solution for long-term environmental monitoring or data acquisition applications.

### Example: Event based Data Logging


```cpp
#include <SD.h>
#include <DHT.h>

#define DHTPIN 7        // Define the digital pin for DHT22 sensor
#define DHTTYPE DHT22   // DHT22 (AM2302) sensor type

const int buttonPin = 2; // Define the digital pin for the button
const int ledPin = 13;   // Define the built-in LED pin

File dataFile; // Create a File object for data logging
DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600);
  pinMode(buttonPin, INPUT_PULLUP);
  pinMode(ledPin, OUTPUT);

  // Initialize SD card
  if (SD.begin(4)) { // Use pin 4 for SD card communication
    Serial.println("SD card is ready to use.");
  } else {
    Serial.println("SD card initialization failed.");
    while (1); // Halt the program if SD card initialization fails
  }

  // Open or create a file for data logging
  dataFile = SD.open("datalog.txt", FILE_WRITE);
  if (dataFile) {
    Serial.println("Data logging initialized.");
    dataFile.close(); // Close the file
  } else {
    Serial.println("Error opening datalog.txt");
  }
}

void loop() {
  int buttonState = digitalRead(buttonPin);

  if (buttonState == LOW) {
    digitalWrite(ledPin, HIGH); // Turn on LED when button is pressed

    // Read sensor data
    float humidity = dht.readHumidity();
    float temperature = dht.readTemperature();

    // Log data to the SD card
    dataFile = SD.open("datalog.txt", FILE_WRITE);
    if (dataFile) {
      dataFile.print("Humidity (%): ");
      dataFile.println(humidity);
      dataFile.print("Temperature (°C): ");
      dataFile.println(temperature);
      dataFile.close(); // Close the file
      Serial.println("Data logged.");
    } else {
      Serial.println("Error opening datalog.txt");
    }

    // Wait for the button to be released
    while (digitalRead(buttonPin) == LOW) {
      delay(10);
    }

    digitalWrite(ledPin, LOW); // Turn off LED
  }
}
```

This code logs data when the button is pressed and released. It reads temperature and humidity from the DHT22 sensor and writes the data to an SD card file. The built-in LED indicates when data is being recorded. Press the button to capture and log data for event-based monitoring.


# Applications of Data Storage
## Real-World Data Storage Applications via Arduino:

Data storage has a wide range of applications in the real world, impacting various fields such as agriculture, healthcare, and transportation.
Environmental Monitoring: Arduino-based data loggers are used to monitor and record environmental parameters like temperature, humidity, and air quality, providing valuable data for scientific research and climate studies.

![Figure 3 22](https://github.com/muneebmh/SIT111.github.io/assets/149995551/66d462a3-f85c-48d1-868a-6ad5225ad48b)
*Figure 3.22 A Metaphorical Example of Data Logging Scenarios via Arduino (Source: Dall-E)*

Some of they key applications in real-world are as follows:

+ **Weather Station:** In this project, Arduino is used to collect data from various weather sensors such as temperature, humidity, and barometric pressure sensors. The Arduino then processes and stores this data on an SD card. Users can access historical weather data for analysis and forecasting.

+ **Aquaponics Monitoring:** Arduino is employed to measure water quality parameters like pH levels and nutrient concentrations in an aquaponics system. The collected data is stored on an SD card, enabling aquaponics enthusiasts to monitor and optimize the conditions for both fish and plant growth.

+ **Home Energy Monitor:** Current sensors connected to an Arduino track electricity consumption in a household. The Arduino logs this data onto an SD card at regular intervals. Homeowners can use the data to analyze their energy usage patterns and make informed decisions on energy conservation.

+ **Security Camera System:** Arduino is used to control motion sensors and cameras in a security system. When motion is detected, Arduino triggers the camera to capture images or videos. These files are stored on an SD card, allowing homeowners to review surveillance footage when necessary.

+ **Environmental Data Logger:** Various environmental sensors are connected to an Arduino to measure parameters like temperature, humidity, and gas levels. Arduino logs this data onto an SD card, making it useful for environmental research, indoor air quality monitoring, and safety applications.

# Wireless Communication
Welcome to Module 3.3, where we will explore the fascinating world of wireless communication with Arduino. In this section, you will learn the fundamentals of wireless communication protocols commonly used with Arduino, understand the principles of wireless communication, and explore the diverse applications of wireless control in Arduino projects.

## Basics of Wireless Communication
Introduction to Wireless Communication:
Wireless communication is the transmission of data between devices without the need for physical wires. It offers the advantage of remote control and monitoring, making it ideal for various applications, including home automation, robotics, and IoT.
Wireless Communication Protocols: Arduino supports various wireless communication protocols, including Bluetooth, Wi-Fi, and RF (Radio Frequency) modules. These protocols enable data transfer between Arduino boards and other devices.
### Example: Bluetooth Communication

```cpp
#include <SoftwareSerial.h>

SoftwareSerial bluetooth(2, 3); // Define software serial pins (RX, TX)
char incomingChar;

void setup() {
  Serial.begin(9600);
  bluetooth.begin(9600);
}

void loop() {
  if (bluetooth.available()) {
    incomingChar = bluetooth.read();
    Serial.print("Received: ");
    Serial.println(incomingChar);
  }
  // You can add code here to perform actions based on received data
}
```

This example demonstrates basic Bluetooth communication between two Arduino boards.

## Understanding the Principles of Wireless Communication
### Key Principles of Wireless Communication:

Successful wireless communication relies on several key principles, including:
+ **Frequency Bands:** Wireless devices operate within specific frequency bands, such as 2.4 GHz for Bluetooth and Wi-Fi. Understanding frequency bands is crucial for avoiding interference.
+ **Modulation Techniques:** Data is modulated onto carrier signals using techniques like amplitude modulation (AM) or frequency modulation (FM).
+ **Data Encoding:** Data encoding methods like Manchester encoding ensure accurate data transmission.
+ **Signal Strength and Range:** Signal strength and range are critical factors. Devices must be within range and have a strong signal for reliable communication.

#### Example: RF Communication

```cpp
#include <RH_ASK.h>
#include <SPI.h>

RH_ASK rf_driver;

void setup() {
  Serial.begin(9600);
  if (!rf_driver.init())
    Serial.println("RF driver initialization failed.");
}

void loop() {
  const char *message = "Hello, Arduino!";
  rf_driver.send((uint8_t *)message, strlen(message));
  rf_driver.waitPacketSent();
  delay(1000); // Send the message every second
}
```

This example illustrates basic RF communication using an RF module with Arduino.

# Applications of Wireless Control
## Real-World Applications of Wireless Control:

### Wireless control using Arduino has a wide range of practical applications:
+ **Smart Home Automation:** Arduino-based devices can control lighting, appliances, and security systems wirelessly, enhancing home automation.
+ **Robotics:** Wireless communication enables remote control and monitoring of robots, making it ideal for robotics applications.
+ **IoT (Internet of Things):** Arduino can be used in IoT projects to collect and transmit data wirelessly, allowing for remote monitoring and control of devices.

#### Example: Remote-Controlled Robot
```cpp
// Simulated code for a remote-controlled robot
void loop() {
  if (receivedSignal == FORWARD_SIGNAL) {
    // Move the robot forward
    moveForward();
  } else if (receivedSignal == BACKWARD_SIGNAL) {
    // Move the robot backward
    moveBackward();
  } // Add more control logic for other directions
}
```

In this example, Arduino wirelessly controls the movements of a robot based on received signals.
