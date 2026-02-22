# Soil Moisture Sensor
![Capacitive Soil Moisture Sensor](/images/SoilSensor.png)

A capacitive soil moisture sensor measures how much water is in the soil by detecting changes in the soil’s dielectric constant (its ability to store electrical charge).

Water has a much higher dielectric constant than dry soil or air. The sensor contains two conductive plates (forming a capacitor). When placed in soil, the material between those plates is the soil itself. As moisture increases, the soil’s dielectric constant increases, which changes the capacitance value. The sensor’s circuitry converts this change in capacitance into a voltage (or digital signal) that can be read by a microcontroller.

Unlike resistive soil moisture sensors, capacitive sensors do not rely on electrical current passing directly through the soil, which makes them more resistant to corrosion and generally more stable over time.

<img src="https://github.com/IDMNYU/DM-GY-9103-L-Sensory-Ecology/blob/main/images/ESP32_Soil+Oled_bb.png" alt="ESP32 + Soil Moisture + OLED" width="420">


## Arduino Code Example to Read Soil Moisture via Serial Monitor 
This code example reads the raw data from the soil moisture sensor and prints the values to the Serial Monitor. It provides a simple way to observe how the sensor readings change in real time as soil conditions shift. This basic output is useful for testing, calibration, and understanding the range of values your specific sensor produces before building more complex interactions.

More water → higher dielectric constant → higher capacitance → different output signal.

```
// These constants won't change. They're used to give names to the pins used:
const int analogInPin = A0;  // Analog input pin that the potentiometer is attached to
const int analogOutPin = 9;  // Analog output pin that the LED is attached to

int sensorValue = 0;  // value read from the pot
int outputValue = 0;  // value output to the PWM (analog out)

void setup() {
  // initialize serial communications at 9600 bps:
  Serial.begin(9600);
}

void loop() {
  // read the analog in value:
  sensorValue = analogRead(analogInPin);
  // map it to the range of the analog out:
  outputValue = map(sensorValue, 0, 900, 0, 255);
  // change the analog out value:
  analogWrite(analogOutPin, outputValue);

  // print the results to the Serial Monitor:
  Serial.print("sensor = ");
  Serial.print(sensorValue);
  Serial.print("\t output = ");
  Serial.println(outputValue);

  // wait 2 milliseconds before the next loop for the analog-to-digital
  // converter to settle after the last reading:
  delay(10);
}
```



