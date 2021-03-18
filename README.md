# CIRCUIT-PLUS : ESP32-TUTORIAL

## INTRODUCTION

Before we start to program using the ESP32 on the Circuits+ board, we will learn a bit about the components embedded on the board.
 
First of all, In this board, the ESP32 used its own pins called GPIO Pins. The ESP32 has 18 x 12 bits Analog – Digital Converter (ADC) input channels. These are the GPIOs that can be used as ADC and respective channels. It has Input components which are USB connectors, MicroSD reader, Buttons, Potentiometer, DHT11 and LDR as well as output components LEDs, and Buzzer. We will program these I/O components later. But first, let’s learn about the GPIO setup for ESP32.

![circuitsPlus_label (1)](https://user-images.githubusercontent.com/60383798/109744207-dcc0b280-7c0c-11eb-9956-db41b67df5ac.png)

## How to set the GPIO pin as Output?

* First, you need to set the GPIO you want to control as an OUTPUT. Use the pinMode() function as follows:

```Bash
  pinMode(GPIO, OUTPUT);	Example : pinMode( 4, OUTPUT);
```

* To control a digital output you just need to use the digitalWrite() function, that accepts as arguments, the GPIO (int number) you are referring to, and the state, either HIGH or LOW.


```Bash
  digitalWrite(GPIO, STATE);	Example : digitalWrite(4, LOW);
```  

## How to set the GPIO pin as Input?
 
* First, set the GPIO you want to read as INPUT, using the pinMode() function as follows:

```Bash
  pinMode(GPIO, INPUT);	Example : pinMode(4, INPUT);
```  

* To read a digital input, like a button, you use the digitalRead() function, that accepts as argument, the GPIO (int number) you are referring to.

```Bash
  digitalRead(GPIO);	Example : digitalRead(4);
```  

  

# EXERCISE 1 :  BUTTON - LED (ON/OFF)

In this exercise, we will use the LED on the board as output and Button as Input where when it pressed the LED will light up and turn off when it released.

## Wiring Diagram

 1. Connect the wiring as the following wiring diagram

![EX1](https://user-images.githubusercontent.com/60383798/109749822-57420000-7c16-11eb-96fc-c884cee1446f.png)

 2. Type this following code and upload to the board.
 
```C
void setup() {
  pinMode(23, OUTPUT); // declaring GPIO23 – Button as an OUTPUT pin.
  pinMode(21, INPUT); // declaring GPIO21 - LED as an INPUT pin.
}

void loop() {
  // put the main code here, to run repeated
	 int button = digitalRead(21);
  if (button == HIGH) {
    digitalWrite(23, HIGH);
  } else  {
    digitalWrite(23, LOW);
  }
}
```

## Sketch Explanations

The LED is connected to the GPIO21 is declare as INPUT and Button connected to GPIO23 	is declared as OUTPUT. 

```C
pinMode(23, OUTPUT); // declaring GPIO23 – Button as an OUTPUT pin.
pinMode(21, INPUT); // declaring GPIO21 - LED as an INPUT pin.
```
In the void loop() function, the program declared variable int button. Like we have 	learn before, we used digitalRead() to the Input state and here we write a statement 	that if the button == HIGH which means the button is pressed. Then, digitalWrite() 	which the output state function also to be declared as HIGH is for the LED to light up. 	Else the digitalWrite() is declared LOW which the LED is turn off.

```C
int button = digitalRead(21);
  if (button == HIGH) {
    digitalWrite(23, HIGH);
  } else  {
    digitalWrite(23, LOW);
  }
```

## Flowchart Explanation

![EXF1](https://user-images.githubusercontent.com/60383798/109626876-fbc33400-7b7b-11eb-9b8c-59760f3e54d1.PNG)

# EXERCISE 2 :  BUZZER (ON/OFF)

In this exercise, we will use the Buzzer on the board as output where we will program the buzzer ON/OFF with milis() function.

## Wiring Diagram

1. Connect the wiring on following the wiring diagram below.

![EX3](https://user-images.githubusercontent.com/60383798/109749859-645eef00-7c16-11eb-9a06-d5dd04b4d193.png)

2. Type this following code and upload to the board.

```C
const int buzzer = 26; // declaring buzzer GPIO pin
int buzzerState = LOW;  // declaring the initial state for buzzer

//use unsigned long for a variables that hold time
unsigned long previousMilis = 0;  // update time from previous
const long interval = 1000;  // interval time to buzzer beep 1 second

void setup() {
  pinMode(buzzer, OUTPUT); // declaring Buzzer as an OUTPUT
}

void loop() {

Unsigned long currentMilis = milis();
  if (currentMilis – previousMilis >= interval){
	previousMilis = currentMilis;
	 
  if (buzzerState == LOW) {
	buzzerState = HIGH;
  } else  {
    	buzzerState = LOW;
  }

	digitalWrite(buzzer, buzzerState);
 }
}
```

## Sketch Explanations

The buzzer is declared to the 26 GPIO pin. For initial state of the buzzer it should be LOW means no action/ring. 

```Bash
const int buzzer = 26; // declaring buzzer GPIO pin
int buzzerState = LOW;  // declaring the initial state for buzzer
```	
Then we declare variable previousMilis to the initial state and interval for the previousMilis to the currentMilis is set to be 1 second.

```Bash
unsigned long previousMilis = 0;  // update time from previous
const long interval = 1000;  // interval time to buzzer beep 1 second
```	
In the loop function we want to the interval keep the previousMilis and currentMilis to be 0 second to 1 second and looping whitihn the interval so the buzzer will beep ON and OFF like an alarm sound.

```Bash

Unsigned long currentMilis = milis();
  if (currentMilis – previousMilis >= interval){
	previousMilis = currentMilis;
	 
  if (buzzerState == LOW) {
	buzzerState = HIGH;
  } else  {
    	buzzerState = LOW;
  }

	digitalWrite(buzzer, buzzerState);
 }
```

## Flowchart Explanation

![exf](https://user-images.githubusercontent.com/60383798/109741182-84d37d00-7c07-11eb-8d7c-4c2221ada527.PNG)


# EXERCISE 3 :  Potentiometer - LED  ( Dim - Bright ) 

In this exercise, we will use the Potentiometer as input on the board and LED as output where we will program the potentiometer to control the LED brightness from Dim to Bright or vice-versa.

## Wiring Diagram

1. Connect the wiring as the following wiring diagram

![EX3](https://user-images.githubusercontent.com/60383798/111412372-482f7780-8717-11eb-8dba-31238512d517.png)

2. Type this following code and upload to the board.

```C
const int POTENTIOMETER_PIN   = 34; // Arduino pin connected to Potentiometer pin
const int LED_PIN          = 16; // Arduino pin connected to LED pin
const float VOLTAGE_THRESHOLD = 2.5; // Voltages

void setup() {
  pinMode(LED_PIN, OUTPUT); // set arduino pin to output mode
}

void loop() {
  int analogValue = analogRead(POTENTIOMETER_PIN);      // read the input on analog pin
  float voltage = floatMap(analogValue, 0, 1023, 0, 255); // Rescale to potentiometer's voltage

  if(voltage > VOLTAGE_THRESHOLD)
    digitalWrite(LED_PIN, HIGH); // turn on LED
  else
    digitalWrite(LED_PIN, LOW);  // turn off LED
}

float floatMap(float x, float in_min, float in_max, float out_min, float out_max) {
  return (x - in_min) * (out_max - out_min) / (in_max - in_min) + out_min;
}

```


## Sketch Explanations

The LED is declare using LED_PIN variable to GPIO16 pin and pin 34 for the potentiometer as the INPUT. The VOLTAGE_THRESHOLD set the voltage to 2.5 set boundaries for the LED to turn on or turn off

```Bash
const int POTENTIOMETER_PIN   = 34; // Arduino pin connected to Potentiometer pin
const int LED_PIN          = 16; // Arduino pin connected to LED pin
const float VOLTAGE_THRESHOLD = 2.5; // Voltages
```
In the void setup() the led is declare as OUTPUt

```Bash
void setup() {
  pinMode(LED_PIN, OUTPUT); // set arduino pin to output mode
}
```

In the void loop() function we use analog syntax as the potentiometer is a analog device. Variable name voltage keep the analog value (0, 1023, 0, 255) indicate that when you turn the potentiometer, the analog value mark the condition.

```Bash
void loop() {
  int analogValue = analogRead(POTENTIOMETER_PIN);      // read the input on analog pin
  float voltage = floatMap(analogValue, 0, 1023, 0, 255); // Rescale to potentiometer's voltage
```
With the statement if-else, when the voltage is more that threshold voltage, then the led will turn ON, otherwise it will be off

```Bash
float floatMap(float x, float in_min, float in_max, float out_min, float out_max) {
  return (x - in_min) * (out_max - out_min) / (in_max - in_min) + out_min;
```
This is the variable floatmap operational that set the statement condition. 

## Flowchart Explanation

![newf](https://user-images.githubusercontent.com/60383798/111568073-0b2cb900-87db-11eb-8b1f-fed4f4903ae1.PNG)

# EXERCISE 4 :  LDR - Buzzer  ( Light Sensor ) 

In this exercise, we will use the LDR and Buzzer, where when the LDR is blocked to the light 	and the buzzer will ringing and stop ringing when it exposed to the light.

## Wiring Diagram

1. Connect the wiring as the following wiring diagram

![EX4](https://user-images.githubusercontent.com/60383798/109749901-717bde00-7c16-11eb-832f-929a2273e581.png)

2. Type this following code and upload to the board.

```C
int sensorValue;
const int buzzer = 26;
 
void setup()
{
  Serial.begin(9600); // starts the serial port at 9600
  pinMode (26,OUTPUT);
}
 
void loop()
{
  sensorValue = analogRead(23); // read analog input pin 23

  if (sensorValue < 150) {
    Serial.println(" - Very Bright");
    Serial.print(sensorValue);    
  } else if (sensorValue < 200) {
    Serial.println(" - Bright");
    Serial.print(sensorValue);
  } else if (sensorValue < 500) {
    Serial.println(" - Normal");
    Serial.print(sensorValue);
  } else if (sensorValue < 800) {
    Serial.println(" - Dim");
    Serial.print(sensorValue);
  } else {
    Serial.println(" - Dark");
    Serial.print(sensorValue);
    digitalWrite(26,HIGH);
    delay(500);
    digitalWrite(26,LOW);
  }
  delay(500);
}

```

## Sketch Explanations

The buzzer used GPIO pin 26 and variable name sensorValue with int type is declared.

```Bash
int sensorValue;
const int buzzer = 26;
```
Then, we declare the Buzzer in pin 26 as OUTPUT and start the serial port at 9600

```Bash
Serial.begin(9600); // starts the serial port at 9600
pinMode (26,OUTPUT);
```
Using the variable sensorValue, the LDR pin 23 is read

```Bash
sensorValue = analogRead(23); // read analog input pin 23
```

This if-else selection set the conditions and statements to be executed. For example, when the sensorValue <150 , then it will print in the serial monitor the value with the message "Very Bright". Same goes with other conditions, except when the sensorValue => to 800, then the buzzer will turn ON for 0.5 second and OFF and again continue reading the sensorValue.

```Bash
 if (sensorValue < 150) {
    Serial.println(" - Very Bright");
    Serial.print(sensorValue);    
  } else if (sensorValue < 200) {
    Serial.println(" - Bright");
    Serial.print(sensorValue);
  } else if (sensorValue < 500) {
    Serial.println(" - Normal");
    Serial.print(sensorValue);
  } else if (sensorValue < 800) {
    Serial.println(" - Dim");
    Serial.print(sensorValue);
  } else {
    Serial.println(" - Dark");
    Serial.print(sensorValue);
    digitalWrite(26,HIGH);
    delay(500);
    digitalWrite(26,LOW);
  }
  delay(500);
```

## Flowchart Explanation

![exp4](https://user-images.githubusercontent.com/60383798/109742682-79ce1c00-7c0a-11eb-80c8-5f007f8ef25b.PNG)

# EXERCISE 5 :   DHT11 (Temperature and Humidity Sensor)

In this exercise, we will use the DHT11 sensor to measure the temperature and humidity of 	the surrounding. To monitor the reading, we will use serial monitor on your Arduino IDE. 

## Wiring Diagram 

1. Connect the wiring as the following wiring diagram

![EX5](https://user-images.githubusercontent.com/60383798/109749922-793b8280-7c16-11eb-9ecd-a71fbbaeb6c4.png)

2. Type this following code and upload to the board.

```C
#include "DHT.h"

#define DHTPIN 4     // what digital pin we're connected to

// Uncomment whatever type you're using!
#define DHTTYPE DHT11   // DHT 11
//#define DHTTYPE DHT22   // DHT 22  (AM2302), AM2321
//#define DHTTYPE DHT21   // DHT 21 (AM2301)

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600);
  Serial.println("DHTxx test!");
  dht.begin();
}

void loop() {
  // Sensor readings may also be up to 2 seconds 'old' (its a very slow sensor)
  float h = dht.readHumidity();
  // Read temperature as Celsius
  float t = dht.readTemperature();

  // Check if any reads failed and exit early (to try again).
  if (isnan(h) || isnan(t)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }
  Serial.print("Humidity: ");
  Serial.print(h);
  Serial.print(" %\t");
  Serial.print("Temperature: ");
  Serial.print(t);
  Serial.println(" Celcius ");
  // Wait a few seconds between measurements.
  delay(2000);
}
```


## Sketch Explanations

We used #include when we use the Arduino library and the syntax must be “.h” as in 	DHT.h. We use #define to define the element. In this case we define DHTPIN and 	DHTTYPES and then we grouping this in a single special variable name DHT.

```Bash
#include “DHT11”  // use the DHT11 library
#define DHTPIN 4     // set to dht pin to GPIO 4
#define DHTTYPE DHT11  // we use DHT11 types of DHT sensor

DHT dht( DHTPIN, DHTTYPE);  // for grouping the dht element
```

Next, in setup() we use Serial.begin as a syntax for using the serial monitor. We use 	Serial.println to print message or to return a value to display on the serial monitor. 

```Bash
Serial.begin(9600); // we set the serial to 9600 baud rate
Serial.println(“DHT test”); // printed in the serial monitor
dht.begin(); //dht startup
```

In loop() function, we use float data types which represent a point or decimal value since the 	humidity and temperature will be measure in point value. We use dht.read to read both 	humidity and temperature. Then we display the measured value using Serial.println. The 	delay is to set the sensor to update measurement for each 2 second.


```Bash
void loop() {
  // Sensor readings may also be up to 2 seconds 'old' (its a very slow sensor)
  float h = dht.readHumidity();
  // Read temperature as Celsius
  float t = dht.readTemperature();

  // Check if any reads failed and exit early (to try again).
  if (isnan(h) || isnan(t)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }
  Serial.print("Humidity: ");
  Serial.print(h);
  Serial.print(" %\t");
  Serial.print("Temperature: ");
  Serial.print(t);
  Serial.println(" Celcius ");
  // Wait a few seconds between measurements.
  delay(2000);
}
```

## Flowchart Explanation

![ex5f](https://user-images.githubusercontent.com/60383798/109744118-c0247a80-7c0c-11eb-964b-dac57e10941f.PNG)


## EXERCISE 6 :   DHT11 (Temperature and Humidity Datalog using SD Card)

in this exercise, we will use SD Card to store the data from the DHT11 sensor in a txt file.

# Wiring Diagram

![sd](https://user-images.githubusercontent.com/60383798/111444288-2b119d80-8745-11eb-926a-e30326cdd818.png)

2. Type this following code and upload to the board.

```C
#include "DHT.h"
#include "FS.h"
#include "SD.h"
#include <SPI.h>
#include <WiFi.h>
#include <NTPClient.h>
#include <WiFiUdp.h>
#define DHTTYPE DHT11 // DHT 11
uint8_t DHTPin = 4; 
DHT dht(DHTPin, DHTTYPE); 
float Temperature;
float Humidity;
String formattedDate;
String dayStamp;
String timeStamp;
// Replace with your network credentials
const char* ssid     = "Shawaltechnologies@unifi";
const char* password = "st7418960";
// Define CS pin for the SD card module
#define SD_CS 5
String dataMessage;
// Define NTP Client to get time
WiFiUDP ntpUDP;
NTPClient timeClient(ntpUDP);
void setup() {
  Serial.begin(115200);
  pinMode(DHTPin, INPUT);
  dht.begin();
  Serial.print("Connecting to ");
  Serial.println(ssid);
  WiFi.begin(ssid, password);
//  while (WiFi.status() != WL_CONNECTED) {
//    delay(500);
//    Serial.print(".");
//  }
  Serial.println("");
  Serial.println("WiFi connected.");
  // Initialize a NTPClient to get time
  timeClient.begin();
  timeClient.setTimeOffset(19800);
  // Initialize SD card
  SD.begin(SD_CS);  
  if(!SD.begin(SD_CS)) {
    Serial.println("Card Mount Failed");
    return;
  }
  uint8_t cardType = SD.cardType();
  if(cardType == CARD_NONE) {
    Serial.println("No SD card attached");
    return;
  }
  Serial.println("Initializing SD card...");
  if (!SD.begin(SD_CS)) {
    Serial.println("ERROR - SD card initialization failed!");
    return;    // init failed
  }
  File file = SD.open("/log.txt");
  if(!file) {
    Serial.println("File doens't exist");
    Serial.println("Creating file...");
    writeFile(SD, "/log.txt", "Date, Time, Temperature, Humidity \r\n");
  }
  else {
    Serial.println("File already exists");  
  }
  file.close();
}
void loop() {
  while (WiFi.status() != WL_CONNECTED) {
    Read_TempHum();
    getTimeStamp();
    logSDCard();
    delay(5000); //Wait for 5 seconds before writing the next data 
  }
}
// Function to get temperature
void Read_TempHum()
{
  Temperature = dht.readTemperature(); 
  Humidity = dht.readHumidity(); 
  Serial.print("Temperature = ");
  Serial.println(Temperature);
  Serial.print("Humidity = ");
  Serial.println(Humidity);
}
// Function to get date and time from NTPClient
void getTimeStamp() {
  while(!timeClient.update()) {
    timeClient.forceUpdate();
  }
  //formattedDate = timeClient.getFormattedDate();
  Serial.println(formattedDate);
  int splitT = formattedDate.indexOf("T");
  dayStamp = formattedDate.substring(0, splitT);
  Serial.println(dayStamp);
  // Extract time
  timeStamp = formattedDate.substring(splitT+1, formattedDate.length()-1);
  Serial.println(timeStamp);
}
// Write the sensor readings on the SD card
void logSDCard() {
  dataMessage =  String(dayStamp) + "," + String(timeStamp) + "," + 
                String(Temperature) + "," + String(Humidity)+ "\r\n";
  Serial.print("Save data: ");
  Serial.println(dataMessage);
  appendFile(SD, "/log.txt", dataMessage.c_str());
}
// Write to the SD card (DON'T MODIFY THIS FUNCTION)
void writeFile(fs::FS &fs, const char * path, const char * message) {
  Serial.printf("Writing file: %s\n", path);
  File file = fs.open(path, FILE_WRITE);
  if(!file) {
    Serial.println("Failed to open file for writing");
    return;
  }
  if(file.print(message)) {
    Serial.println("File written");
  } else {
    Serial.println("Write failed");
  }
  file.close();
}
// Append data to the SD card (DON'T MODIFY THIS FUNCTION)
void appendFile(fs::FS &fs, const char * path, const char * message) {
  Serial.printf("Appending to file: %s\n", path);
  File file = fs.open(path, FILE_APPEND);
  if(!file) {
    Serial.println("Failed to open file for appending");
    return;
  }
  if(file.print(message)) {
    Serial.println("Message appended");
  } else {
    Serial.println("Append failed");
  }
  file.close();
}
```

## Coding Explaination


