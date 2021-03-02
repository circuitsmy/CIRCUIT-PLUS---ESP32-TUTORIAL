# CIRCUIT-PLUS : ESP32-TUTORIAL

## INTRODUCTION

Before we start to program using the ESP32 on the Circuits+ board, we will learn a bit about the components embedded on the board.
 
First of all, In this board, the ESP32 used its own pins called GPIO Pins. The ESP32 has 18 x 12 bits Analog – Digital Converter (ADC) input channels. These are the GPIOs that can be used as ADC and respective channels. It has Input components which are USB connectors, MicroSD reader, Buttons, Potentiometer, DHT11 and LDR as well as output components LEDs, and Buzzer. We will program these I/O components later. But first, let’s learn about the GPIO setup for ESP32.

![CP](https://user-images.githubusercontent.com/60383798/109624171-da147d80-7b78-11eb-8482-00507ddaa1cc.png)

## How to set the GPIO pin as Output?

*	First, you need to set the GPIO you want to control as an OUTPUT. Use the pinMode() function as follows:

  pinMode(GPIO, OUTPUT);	Example : pinMode( 4, OUTPUT);

*	To control a digital output you just need to use the digitalWrite() function, that accepts as arguments, the GPIO (int number) you are referring to, and the state, either HIGH or LOW.

  digitalWrite(GPIO, STATE);	Example : digitalWrite(4, LOW);

## How to set the GPIO pin as Input?
 
*	First, set the GPIO you want to read as INPUT, using the pinMode() function as follows:

  pinMode(GPIO, INPUT);	Example : pinMode(4, INPUT);

*	To read a digital input, like a button, you use the digitalRead() function, that accepts as argument, the GPIO (int number) you are referring to.

  digitalRead(GPIO);	Example : digitalRead(4);



# EXERCISE 1 :  BUTTON - LED (ON/OFF)

In this exercise, we will use the LED on the board as output and Button as Input where when it pressed the LED will light up and turn off when it released.

 1. Connect the wiring as the following wiring diagram

![EX1](https://user-images.githubusercontent.com/60383798/109625536-63787f80-7b7a-11eb-94ee-35d2d4c30514.png)

 2. Type this following code and upload to the board.
 
<void setup() {
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


if (isAwesome){
  return true
}



