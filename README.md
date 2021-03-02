# CIRCUIT-PLUS : ESP32-TUTORIAL

## INTRODUCTION

Before we start to program using the ESP32 on the Circuits+ board, we will learn a bit about the components embedded on the board.
 
First of all, In this board, the ESP32 used its own pins called GPIO Pins. The ESP32 has 18 x 12 bits Analog – Digital Converter (ADC) input channels. These are the GPIOs that can be used as ADC and respective channels. It has Input components which are USB connectors, MicroSD reader, Buttons, Potentiometer, DHT11 and LDR as well as output components LEDs, and Buzzer. We will program these I/O components later. But first, let’s learn about the GPIO setup for ESP32.

![CP](https://user-images.githubusercontent.com/60383798/109624171-da147d80-7b78-11eb-8482-00507ddaa1cc.png)

## How to set the GPIO pin as Output?

*	First, you need to set the GPIO you want to control as an OUTPUT. Use the pinMode() function as follows:

```Bash
  pinMode(GPIO, OUTPUT);	Example : pinMode( 4, OUTPUT);
```

*	To control a digital output you just need to use the digitalWrite() function, that accepts as arguments, the GPIO (int number) you are referring to, and the state, either HIGH or LOW.


```Bash
  digitalWrite(GPIO, STATE);	Example : digitalWrite(4, LOW);
```  

## How to set the GPIO pin as Input?
 
*	First, set the GPIO you want to read as INPUT, using the pinMode() function as follows:

```Bash
  pinMode(GPIO, INPUT);	Example : pinMode(4, INPUT);
```  

*	To read a digital input, like a button, you use the digitalRead() function, that accepts as argument, the GPIO (int number) you are referring to.

```Bash
  digitalRead(GPIO);	Example : digitalRead(4);
```  

  

# EXERCISE 1 :  BUTTON - LED (ON/OFF)

In this exercise, we will use the LED on the board as output and Button as Input where when it pressed the LED will light up and turn off when it released.

## Wiring Diagram

 1. Connect the wiring as the following wiring diagram

![EX1](https://user-images.githubusercontent.com/60383798/109625536-63787f80-7b7a-11eb-94ee-35d2d4c30514.png)

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

![ex2](https://user-images.githubusercontent.com/60383798/109628525-cddeef00-7b7d-11eb-969f-ae3466fe89ed.png)

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
```

## Flowchart Explanation

![exf2](https://user-images.githubusercontent.com/60383798/109629101-755c2180-7b7e-11eb-8ad0-65a20187a32b.PNG)

