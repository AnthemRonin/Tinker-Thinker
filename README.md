# Tinker-Thinker

const int trigPin = 11;
const int echoPin = 12;

int pirState = LOW;
int buzzerPin = 7;                // choose the pin for the BUZZER
int inputPin = 3;              // choose the input pin (for PIR sensor)
int val = 0;
void setup() {
  // initialize serial communication:
  Serial.begin(9600);
  pinMode(trigPin,OUTPUT);
  pinMode(echoPin,INPUT);

  pinMode(buzzerPin, OUTPUT);      // declare BUZZER as output
  pinMode(inputPin, INPUT);     // declare sensor as input

}

void loop() {

   val = digitalRead(inputPin);  // read input value
  if (val == HIGH) {            // check if the input is HIGH
    digitalWrite(buzzerPin, HIGH);  // turn BUZZER ON
    if (pirState == LOW) if (pirState == LOW) {
  unsigned char i;
  if (1) {
    //If we want to control the active buzzer to make sound continuously,
    //we only need to give a high level to the output port.
    for (i = 75; i < 100; i++) {
      digitalWrite(buzzerPin, HIGH);
      delay(2);  //wait for 1ms
      digitalWrite(buzzerPin, LOW);
      delay(25);  //wait for 1ms
    }

    //Try to shorten the delay of the buzzer to 1ms,
    //and we will hear a sound with a stable frequency.
    for (i = 80; i < 100; i++) {
      digitalWrite(buzzerPin, HIGH);
      delay(2);  //wait for 2ms
      digitalWrite(buzzerPin, LOW);
      delay(5);  //wait for 2ms
    }
  }
  }



    else {
    digitalWrite(buzzerPin, LOW); // turn BUZZER OFF
    if (pirState == HIGH){
      // we have just turned of
      Serial.println("Motion ended!");
      // We only want to print on the output change, not state
      pirState = LOW;
    }
  }
  }
  // establish variables for duration of the ping, and the distance result
  // in inches and centimeters:
  long duration, inches, cm;

  // The PING))) is triggered by a HIGH pulse of 2 or more microseconds.
  // Give a short LOW pulse beforehand to ensure a clean HIGH pulse:
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // The same pin is used to read the signal from the PING))): a HIGH pulse
  // whose duration is the time (in microseconds) from the sending of the ping
  // to the reception of its echo off of an object.
  duration = pulseIn(echoPin, HIGH);

  // convert the time into a distance
  inches = microsecondsToInches(duration);
  cm = microsecondsToCentimeters(duration);

  Serial.print(inches);
  Serial.print("in, ");
  Serial.print(cm);
  Serial.print("cm");
  Serial.println();
  delay(100);
  
}

long microsecondsToInches(long microseconds) {
  // According to Parallax's datasheet for the PING))), there are 73.746
  // microseconds per inch (i.e. sound travels at 1130 feet per second).
  // This gives the distance travelled by the ping, outbound and return,
  // so we divide by 2 to get the distance of the obstacle.
  // See: https://www.parallax.com/package/ping-ultrasonic-distance-sensor-downloads/
  return microseconds / 74 / 2;
}

long microsecondsToCentimeters(long microseconds) {
  // The speed of sound is 340 m/s or 29 microseconds per centimeter.
  // The ping travels out and back, so to find the distance of the object we
  // take half of the distance travelled.
  return microseconds / 29 / 2;
}

