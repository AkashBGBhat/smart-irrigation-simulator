# smart-irrigation-simulator
Arduino-based smart irrigation simulator that turns a pump ON when soil moisture drops below a threshold. Built on Wokwi.

https://wokwi.com/projects/478056834107943937


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

The code below is for the diagram.json of the Smart Irrigation Simulator

    {
      "version": 1,
      "author": "Akash Bhat",
      "editor": "wokwi",
      "parts": [
        { "type": "wokwi-arduino-uno", "id": "uno", "top": 0, "left": 0, "attrs": {} },
        {
          "type": "wokwi-led",
          "id": "led1",
          "top": -61.2,
          "left": -101.8,
          "attrs": { "color": "red" }
        },
        { "type": "wokwi-potentiometer", "id": "pot1", "top": 104.3, "left": -105.8, "attrs": {} }
      ],
      "connections": [
        [ "led1:A", "uno:13", "green", [ "v0" ] ],
        [ "led1:C", "uno:GND.1", "green", [ "v0" ] ],
        [ "pot1:VCC", "uno:5V", "red", [ "v0" ] ],
        [ "pot1:GND", "uno:GND.2", "black", [ "v0" ] ],
        [ "pot1:SIG", "uno:A0", "green", [ "v0" ] ]
      ],
      "dependencies": {}
    }
