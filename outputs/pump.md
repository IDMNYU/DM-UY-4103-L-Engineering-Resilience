
```

// These constants won't change. They're used to give names to the pins used:
const int soilPin = A0;  // Analog input pin that the potentiometer is attached to
const int redPin = 5;    // Analog output pin that the LED is attached to
const int greenPin = 7;  // Analog output pin that the LED is attached to
const int bluePin = 6;   // Analog output pin that the LED is attached to
const int pumPin = 8;


int sensorValue = 0;  // value read from the pot
int outputValue = 0;  // value output to the PWM (analog out)

void setup() {
  // initialize serial communications at 9600 bps:
  Serial.begin(9600);
  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);
  pinMode(pumPin, OUTPUT);

  
}

void loop() {
  // read the analog in value:
  sensorValue = analogRead(soilPin);
  // map it to the range of the analog out:
  //outputValue = map(sensorValue, 0, 1023, 0, 255);
  // change the analog out value:
  //analogWrite(analogOutPin, outputValue);

  // print the results to the Serial Monitor:
  Serial.print("sensor = ");
  Serial.println(sensorValue);

  // soil moisture higher or equal 400 = dry

  if (sensorValue >= 400) {
    digitalWrite(bluePin, HIGH);
    digitalWrite(redPin, LOW);
    digitalWrite(greenPin, LOW);
    // turn on the pump
    digitalWrite(pumPin, HIGH);
    delay(1000);
    digitalWrite(pumPin, LOW);
    Serial.println("turn pump on! I am dry");
  }

  // soil moisture between 400 & 250 = moist and ideal

  if ((sensorValue < 400)&&(sensorValue > 250)) {
      digitalWrite(greenPin, HIGH);
      digitalWrite(redPin, LOW);
      digitalWrite(bluePin, LOW);
      // pump off
      digitalWrite(pumPin, LOW);
      Serial.println("turn pump off! I am happy");
    }

  // soil moisture lower than 250 = too wet, stop watering!

  if (sensorValue <= 250) {
    digitalWrite(redPin, HIGH);
    digitalWrite(greenPin, LOW);
    digitalWrite(bluePin, LOW);
    // pump off
    digitalWrite(pumPin, LOW);
    Serial.println("turn pump on! I am soaked");
  }

  else {
    Serial.println("weirdness happening");
  }

  //Serial.print("\t output = ");
  //Serial.println(outputValue);

  // wait 2 milliseconds before the next loop for the analog-to-digital
  // converter to settle after the last reading:
  delay(10000);
}

```
