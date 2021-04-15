#define echopin A4 // echo pin
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
