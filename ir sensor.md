Using an IR (Infrared) sensor with an Arduino can allow you to measure the presence or distance of objects. One common type of IR sensor is the IR distance sensor (such as the Sharp GP2Y0A21YK0F), which provides an analog voltage output proportional to the distance to the nearest object.

### Hardware Setup:

1. **Components:**
   - Arduino board (e.g., Arduino Uno)
   - IR sensor (e.g., Sharp GP2Y0A21YK0F)
   - Breadboard
   - Jumper wires

2. **Connections:**
   - Connect the `Vcc` pin of the IR sensor to the `5V` pin on the Arduino.
   - Connect the `GND` pin of the IR sensor to the `GND` pin on the Arduino.
   - Connect the `Output` pin of the IR sensor to an analog input pin on the Arduino, e.g., `A0`.

### Code:

Here is the Arduino code to read the distance from the IR sensor and display it in the Serial Monitor:

```cpp
// Define the analog pin where the IR sensor is connected
const int irPin = A0;

void setup() {
  // Start the serial communication
  Serial.begin(9600);
}

void loop() {
  // Read the analog value from the sensor
  int analogValue = analogRead(irPin);

  // Convert the analog value to voltage
  float voltage = analogValue * (5.0 / 1023.0);

  // Convert the voltage to distance (this conversion will vary based on your sensor's datasheet)
  float distance = voltageToDistance(voltage);

  // Print the distance to the Serial Monitor
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  // Wait for 200 milliseconds before taking another reading
  delay(200);
}

// Function to convert voltage to distance
float voltageToDistance(float voltage) {
  // Conversion logic based on the sensor's datasheet
  // For Sharp GP2Y0A21YK0F: Distance (cm) = 27.86 / (voltage - 0.42)
  // Adjust the constants as per your specific IR sensor datasheet
  return 27.86 / (voltage - 0.42);
}
```

### Explanation:

- **`irPin`**: This is the analog pin where the IR sensor is connected (A0 in this case).
- **`setup()`**: Initializes serial communication at 9600 baud rate for displaying data in the Serial Monitor.
- **`loop()`**: Continuously reads the analog value from the IR sensor, converts it to voltage, then to distance based on the sensor's datasheet, and prints the distance to the Serial Monitor. It waits for 200 milliseconds before taking another reading.
- **`voltageToDistance()`**: This function converts the voltage output from the sensor to a distance value. The conversion formula will vary based on the specific IR sensor you are using, so refer to your sensor's datasheet for the appropriate formula.

### Steps to Simulate on Tinkercad:

1. Open [Tinkercad](https://www.tinkercad.com/).
2. Click on "Circuits" and then "Create new Circuit".
3. Add an Arduino Uno board to the workspace.
4. Add an IR sensor.
5. Connect the components as described in the hardware setup section.
6. Click on "Code" and switch to "Text" mode.
7. Copy and paste the provided code into the code editor.
8. Start the simulation and open the Serial Monitor to see the distance readings.

This setup will allow you to measure distance using an IR sensor and an Arduino board, displaying the results in centimeters in the Serial Monitor. Let me know if you need further assistance!