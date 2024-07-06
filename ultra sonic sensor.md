Using an ultrasonic sensor with an Arduino allows you to measure distances to objects. One commonly used ultrasonic sensor is the HC-SR04. It uses sound waves to measure distance by sending out a sound wave and timing how long it takes to bounce back.

### Hardware Setup:

1. **Components:**
   - Arduino board (e.g., Arduino Uno)
   - HC-SR04 ultrasonic sensor
   - Breadboard
   - Jumper wires

2. **Connections:**
   - Connect the `Vcc` pin of the HC-SR04 to the `5V` pin on the Arduino.
   - Connect the `GND` pin of the HC-SR04 to the `GND` pin on the Arduino.
   - Connect the `Trig` pin of the HC-SR04 to a digital pin on the Arduino, e.g., `D9`.
   - Connect the `Echo` pin of the HC-SR04 to another digital pin on the Arduino, e.g., `D10`.

### Code:

Here is the Arduino code to read the distance from the HC-SR04 sensor and display it in the Serial Monitor:

```cpp
// Define the pins for the HC-SR04 sensor
const int trigPin = 9;
const int echoPin = 10;

void setup() {
  // Start the serial communication
  Serial.begin(9600);
  
  // Set the trigPin as an output
  pinMode(trigPin, OUTPUT);
  
  // Set the echoPin as an input
  pinMode(echoPin, INPUT);
}

void loop() {
  // Send a 10us pulse to the trigPin to initiate the sensor
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  
  // Read the echoPin and calculate the duration of the echo pulse
  long duration = pulseIn(echoPin, HIGH);
  
  // Calculate the distance based on the duration
  // Speed of sound is 34300 cm/s, so we divide by 2 to account for the round-trip
  float distance = (duration * 0.0343) / 2;
  
  // Print the distance to the Serial Monitor
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");
  
  // Wait for 100 milliseconds before taking another reading
  delay(100);
}
```

### Explanation:

- **`trigPin`**: This is the digital pin where the `Trig` pin of the HC-SR04 sensor is connected (D9 in this case).
- **`echoPin`**: This is the digital pin where the `Echo` pin of the HC-SR04 sensor is connected (D10 in this case).
- **`setup()`**: Initializes serial communication at 9600 baud rate, sets the `trigPin` as an output, and the `echoPin` as an input.
- **`loop()`**: Continuously sends a 10 microsecond pulse to the `trigPin` to trigger the sensor, reads the duration of the echo pulse on the `echoPin`, calculates the distance based on the duration, and prints the distance to the Serial Monitor. It waits for 100 milliseconds before taking another reading.

### Steps to Simulate on Tinkercad:

1. Open [Tinkercad](https://www.tinkercad.com/).
2. Click on "Circuits" and then "Create new Circuit".
3. Add an Arduino Uno board to the workspace.
4. Add an HC-SR04 ultrasonic sensor.
5. Connect the components as described in the hardware setup section.
6. Click on "Code" and switch to "Text" mode.
7. Copy and paste the provided code into the code editor.
8. Start the simulation and open the Serial Monitor to see the distance readings.

This setup will allow you to measure distances using an ultrasonic sensor and an Arduino board, displaying the results in centimeters in the Serial Monitor. Let me know if you need further assistance!