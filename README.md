# Obstacle-Avoiding-Arduino-Car

### Ultrasonic Sensor Testing :


* Test the ultrasonic sensor using this below code. If it showing distance values in Serial monitor then go to Obstacle Avoiding code.

![Ultrasonic sensor](https://microcontrollerslab.com/wp-content/uploads/2014/12/HC-SR04-Ultrasonic-Sensor-Pinout-diagram.jpg)

```C++

#define echopin A4 // echo pin  --- Change these two numbers to respective numbers those are connected in Arduino.
#define trigpin A5 // Trigger pin

int distance;
long duration;

void setup() {
  Serial.begin(9600);        
  Serial.println("Start");

  pinMode (trigpin, OUTPUT);
  pinMode (echopin, INPUT );
  
}

void loop() {
 distance = data();
 Serial.print("S=");
 Serial.println(distance);    // prints the distance of the object from Ultrasonic sensor
}


long data(){
  digitalWrite(trigpin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigpin, HIGH);
  delayMicroseconds(10);
  duration = pulseIn (echopin, HIGH);
  return duration / 29 / 2;
}


```
# Obstacle Avoiding code

* Copy and paste this code in arduino IDE. Check the connections before Uploading the code into arduino board.

```C++


#include "AFMotor.h"

#define echopin A3 // echo pin  --- Change these two numbers to respective numbers those are connected in Arduino.
#define trigpin A4 // Trigger pin

 

AF_DCMotor motor1(1, MOTOR12_64KHZ); // create motor object, 64KHz pwm
AF_DCMotor motor2(4, MOTOR12_64KHZ); // create motor object, 64KHz pwm



int distance;
long duration;

int set = 20;
 
void setup() {
  Serial.begin(9600);           // Initialize serial port
  Serial.println("Start");

  pinMode (trigpin, OUTPUT);
  pinMode (echopin, INPUT );
  
  motor1.setSpeed(255);          // set the motor speed to 0-255
  motor2.setSpeed(255);

}

void loop() {
 distance = data();
 Serial.print("S=");
 Serial.println(distance);
  if (distance > set){
    Serial.println("Forward");
    motor1.run(FORWARD);         // turn it on going forward
    motor2.run(FORWARD); 
    }
  else{
     motor1.run(BACKWARD);   // turn it on going left
     motor2.run(BACKWARD); 
     delay(600);
     motor1.run(BACKWARD);   // turn it on going left
     motor2.run(FORWARD);
     delay(1000); 
   }
}


long data(){
  digitalWrite(trigpin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigpin, HIGH);
  delayMicroseconds(10);
  duration = pulseIn (echopin, HIGH);
  return duration / 29 / 2;
}


``
