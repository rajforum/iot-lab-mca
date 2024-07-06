Using a PIR (Passive Infrared) sensor with an Arduino allows you to detect motion. PIR sensors are commonly used for motion detection in security systems, lighting control, and similar applications.

### Hardware Setup:

1. **Components:**
   - Arduino board (e.g., Arduino Uno)
   - PIR sensor
   - Breadboard
   - Jumper wires
   - LED (optional, for visual indication)
   - Resistor (220 ohm, optional, for LED)

2. **Connections:**
   - Connect the `Vcc` pin of the PIR sensor to the `5V` pin on the Arduino.
   - Connect the `GND` pin of the PIR sensor to the `GND` pin on the Arduino.
   - Connect the `Output` pin of the PIR sensor to a digital input pin on the Arduino, e.g., `D2`.
   - (Optional) Connect an LED with a 220-ohm resistor to another digital pin, e.g., `D13`.

### Code:

Here is the Arduino code to read the output from the PIR sensor and print the motion status in the Serial Monitor. Additionally, it turns on an LED when motion is detected.

```cpp
// Define the pins for the PIR sensor and LED
const int pirPin = 2;     // PIR sensor output pin
const int ledPin = 13;    // LED pin (optional)

void setup() {
  // Start the serial communication
  Serial.begin(9600);
  
  // Set the PIR sensor pin as input
  pinMode(pirPin, INPUT);
  
  // Set the LED pin as output
  pinMode(ledPin, OUTPUT);
}

void loop() {
  // Read the value from the PIR sensor
  int pirValue = digitalRead(pirPin);
  
  // Check if motion is detected
  if (pirValue == HIGH) {
    // Motion detected
    Serial.println("Motion detected!");
    
    // Turn on the LED
    digitalWrite(ledPin, HIGH);
  } else {
    // No motion
    Serial.println("No motion");
    
    // Turn off the LED
    digitalWrite(ledPin, LOW);
  }
  
  // Wait for 500 milliseconds before taking another reading
  delay(500);
}
```

### Explanation:

- **`pirPin`**: This is the digital pin where the PIR sensor is connected (D2 in this case).
- **`ledPin`**: This is the digital pin where the LED is connected (D13 in this case).
- **`setup()`**: Initializes serial communication at 9600 baud rate, sets the PIR sensor pin as input, and the LED pin as output.
- **`loop()`**: Continuously reads the digital value from the PIR sensor, checks if motion is detected (if the sensor's output is HIGH), and prints the motion status to the Serial Monitor. It also turns the LED on or off based on the motion status. It waits for 500 milliseconds before taking another reading.

### Steps to Simulate on Tinkercad:

1. Open [Tinkercad](https://www.tinkercad.com/).
2. Click on "Circuits" and then "Create new Circuit".
3. Add an Arduino Uno board to the workspace.
4. Add a PIR sensor.
5. (Optional) Add an LED and a 220-ohm resistor.
6. Connect the components as described in the hardware setup section.
7. Click on "Code" and switch to "Text" mode.
8. Copy and paste the provided code into the code editor.
9. Start the simulation and open the Serial Monitor to see the motion status.

This setup will allow you to detect motion using a PIR sensor and an Arduino board, displaying the results in the Serial Monitor and optionally turning on an LED when motion is detected. Let me know if you need further assistance!