# smart-irrigation-simulator
Arduino-based smart irrigation simulator that turns a pump ON when soil moisture drops below a threshold. Built on Wokwi.

https://wokwi.com/projects/478056834107943937
''' 
int sensorPin = A0;
int ledPin = 13;
int threshold = 500;

void setup() {
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  int moisture = analogRead(sensorPin);
  Serial.println(moisture);

  if (moisture < threshold) {
    digitalWrite(ledPin, HIGH);
  } else {
    digitalWrite(ledPin, LOW);
  }
  delay(500);
}
'''
