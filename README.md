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
	!

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

The LED is declare using LED_PIN variable to GPIO23 pin.

```Bash
int LED_PIN = 23;  // declaring LED pin GPIO
```
Then, in void setup() function we declare pin 23 which the LED as OUTPUT and pin 21 for the potentiometer as the INPUT.

```Bash
pinMode(LED_PIN, OUTPUT); // declaring GPIO23 –as an OUTPUT pin.
pinMode(21, INPUT); // declaring GPIO21 -as an INPUT pin.
```

In the void loop() function we set a variable name potentioValue to analogRead() function where it is the same as digitalRead() function and the different is we use analog instead of digital because potentiometer is analog components. Then, we declare another variable name brightness, where it scale the value from the 0 to 255 as the common brightness of a LED. We add delay to see the changes when you rotate the potentiometer.

```Bash
int potentioValue = analogRead(21); //read the input potentiometer value

int brightness = map(potentioValue, 0, 1023, 0, 255);
//scale the brightness from 0 to 255

delay (100); // delay 0.1 second
```

## Flowchart Explanation

![ex3f](https://user-images.githubusercontent.com/60383798/109740714-b0a23300-7c06-11eb-8b31-eeaec5864f3e.PNG)


# EXERCISE 4 :  LDR - Buzzer  ( Light Sensor ) 

In this exercise, we will use the LDR and Buzzer, where when the LDR is blocked to the light 	and the buzzer will ringing and stop ringing when it exposed to the light.

## Wiring Diagram

1. Connect the wiring as the following wiring diagram

![EX4](https://user-images.githubusercontent.com/60383798/109749901-717bde00-7c16-11eb-832f-929a2273e581.png)

2. Type this following code and upload to the board.

```C
const int Buzzer = 21;  // declaring Buzzer pin GPIO
const int LDR = 23;  // declaring ldr pin GPIO

void setup() 
  pinMode(Buzzer, OUTPUT); // declaring GPIO23 –as an OUTPUT pin.
  pinMode(LDR, INPUT); // declaring GPIO21 -as an INPUT pin.
  
}

void loop() {
  // put the main code here, to run repeated
	 int ldrStatus = analogRead(21); //read the ldr status

  if (ldrStatus>= 100) {
	    tone(Buzzer,100);
	    delay(100);

	    noTone(Buzzer);
	    delay(100);
  }
  else {
	    noTone(Buzzer);
    	    delay(1000);
	}
}
```

## Sketch Explanations

The buzzer and LDR are declared for each GPIO pin using variable int.

```Bash
const int Buzzer = 21;  // declaring Buzzer pin GPIO
const int LDR = 23;  // declaring ldr pin GPIO
```
Then, we declare the Buzzer as OUTPUT and LDR as INPUT.

```Bash
pinMode(Buzzer, OUTPUT); // declaring GPIO23 –as an OUTPUT pin.
pinMode(LDR, INPUT); // declaring GPIO21 -as an INPUT pin.
```
We use analogRead() to read the ldrStatus. Where, when the LDR measure the intensity of the light it received. We use if-else statement to determine the condition where the ldrStatus 	reach >=100 and the buzzer will beep and go off for each 0,1 second gap. We use tone and noTone fuction to make the buzzer on and off with the delay. If ldrStatus <=100, then the buzzer will remain off state.
	
## Flowchart Explanation

![exp4](https://user-images.githubusercontent.com/60383798/109742682-79ce1c00-7c0a-11eb-80c8-5f007f8ef25b.PNG)

# EXERCISE 5 :   DHT11 (Temperature and Humidity Sensor)

In this exercise, we will use the DHT11 sensor to measure the temperature and humidity of 	the surrounding. To monitor the reading, we will use serial monitor on your Arduino IDE. 

## Wiring Diagram 

1. Connect the wiring as the following wiring diagram

![EX5](https://user-images.githubusercontent.com/60383798/109749922-793b8280-7c16-11eb-9ecd-a71fbbaeb6c4.png)

2. Type this following code and upload to the board.

```C
#include “DHT11”  // use the DHT11 library
#define DHTPIN 4     // set to dht pin to GPIO 4
#define DHTTYPE DHT11  // we use DHT11 types of DHT sensor

DHT dht( DHTPIN, DHTTYPE);  // for grouping the dht element

void setup() {

  Serial.begin(9600); // we set the serial to 9600 baud rate
  Serial.println(“DHT test”); // printed in the serial monitor
  dht.begin(); //dht startup
}

void loop() {
  // sensor reading
	 float h = dht.readHumidity();  //read humidity function
  float t = dht.readTemperature();  //read temperature function

  Serial.println(“Humidity :”);  // print line
  Serial.println(h);  // print value h
  Serial.println(“Temperature :”); // print line
  Serial.println(t);  // print value t
  
  delay(2000);  //delay 2 second
	
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
float h = dht.readHumidity();  //read humidity function
float t = dht.readTemperature();  //read temperature function

Serial.println(“Humidity :”);  // print line
Serial.println(h);  // print value h
Serial.println(“Temperature :”); // print line
Serial.println(t);  // print value t
  
delay(2000);  //delay 2 second
```

## Flowchart Explanation

![ex5f](https://user-images.githubusercontent.com/60383798/109744118-c0247a80-7c0c-11eb-964b-dac57e10941f.PNG)




