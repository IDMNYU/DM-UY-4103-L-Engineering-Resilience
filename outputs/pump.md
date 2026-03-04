# DC Pump 

A low-power 3.3–5V DC pump is a small electric pump designed to move water or other liquids using very little power. It typically runs directly from low-voltage sources such as microcontrollers (Arduino, ESP32), USB power, batteries, or small solar panels. These pumps are commonly used in DIY projects like small fountains, plant watering systems, hydroponics, cooling loops, or environmental sensing setups.

<img src="/images/pump.jpg" alt="DC Submersible Water Pump" width="300">


Because they operate at 3.3–5 volts, they are well suited for low-energy and intermittent systems, including solar-powered projects. Most are submersible, use a brushless motor, and draw relatively little current (often around 100–300 mA), making them easy to integrate into low-power electronics and creative prototypes. These pumps are popular in maker, art, and environmental projects where compact size and minimal energy consumption are important.

### Typical features:

- Operating voltage: 3.3–5V DC
- Small, lightweight, and inexpensive
- Submersible design with simple inlet/outlet tubing
- Suitable for low-flow circulation rather than high-pressure pumping

## 5V Relay 

<img src="/images/Single-Channel-Relay-Module-Pinout.jpg" alt="5V 1 Channel Relay Board" width="350">

A 5V single-channel relay board is a small electronic module that allows a low-voltage signal—such as from a microcontroller like an Arduino or ESP32—to safely switch higher-power devices on or off, acting as an electrically controlled switch between the control circuit and the load.

## Soil Moisture Triggering Water Pump 

<img src="/images/Uno_Leds_Pump_Relay_bb.png" alt="Fritzing Diagram of Arduino Uno with Soil Moisture sensor and 5V Relay board connected to Submersible DC Pump" width="400">


```
// These constants won't change. They're used to give names to the pins used:
const int soilPin = A0;  // Analog input pin that the potentiometer is attached to
const int redPin = 5;    // Analog output pin that the LED is attached to
const int greenPin = 7;  // Analog output pin that the LED is attached to
const int bluePin = 6;   // Analog output pin that the LED is attached to
const int pumPin = 8;

// Variable to contain sensor readings
int sensorValue = 0;  // value read from the soil moisture sensor

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

  // print the results to the Serial Monitor:
  Serial.print("sensor = ");
  Serial.println(sensorValue);

  // soil moisture higher or equal 400 = DRY

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
    //catch whatever edge cases might not have been caught but previous if statement
    Serial.println("weirdness happening");    
  }

  // wait 10 seconds before checking again. A more elegant solution would be to use millis() instead of delays

  delay(10000);
}

```
