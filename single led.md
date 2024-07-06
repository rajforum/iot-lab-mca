To use an Arduino IoT Cloud project to control a single LED remotely, follow these steps:

### Hardware Setup:

1. **Components:**
   - Arduino board with Wi-Fi capability (e.g., Arduino MKR WiFi 1010, Arduino Nano 33 IoT)
   - LED
   - 220-ohm resistor
   - Breadboard
   - Jumper wires

2. **Connections:**
   - Connect the longer leg (anode) of the LED to a digital pin on the Arduino, e.g., `D5`.
   - Connect the shorter leg (cathode) of the LED to one end of the 220-ohm resistor.
   - Connect the other end of the 220-ohm resistor to the `GND` pin on the Arduino.

### Setting Up Arduino IoT Cloud:

1. **Sign up and Create a Thing:**
   - Sign up for an account on [Arduino IoT Cloud](https://create.arduino.cc/iot/things).
   - Click on "Create Thing" to create a new project.
   - Name your Thing and add a property to control the LED.

2. **Configure the Thing Property:**
   - Add a property for the LED:
     - Name: LED
     - Type: boolean
     - Update: on change

3. **Generate and Download the Sketch:**
   - After adding the property, click on "Setup" to configure the device.
   - Select your board type (e.g., Arduino MKR WiFi 1010).
   - Follow the instructions to set up the device and connect it to your Wi-Fi network.
   - Download the generated sketch to your computer.

### Code:

Here is a modified version of the generated sketch to include control of the LED:

```cpp
#include "thingProperties.h"

#define LED_PIN 5  // Pin where the LED is connected

void setup() {
  // Initialize serial and wait for port to open:
  Serial.begin(9600);
  delay(1500); 

  // Set the LED pin as an output
  pinMode(LED_PIN, OUTPUT);

  // Defined in thingProperties.h
  initProperties();

  // Connect to Arduino IoT Cloud
  ArduinoCloud.begin(ArduinoIoTPreferredConnection);

  // Wait to ensure connection
  delay(1500); 
}

void loop() {
  ArduinoCloud.update();
}

// This function gets called whenever the value of LED changes in Arduino IoT Cloud
void onLEDChange() {
  if (LED) {
    digitalWrite(LED_PIN, HIGH);  // Turn the LED on
    Serial.println("LED is ON");
  } else {
    digitalWrite(LED_PIN, LOW);   // Turn the LED off
    Serial.println("LED is OFF");
  }
}
```

### Explanation:

- **`LED_PIN`**: This is the digital pin where the LED is connected (D5 in this case).
- **`setup()`**: Initializes serial communication, sets the LED pin as an output, and connects to the Arduino IoT Cloud.
- **`loop()`**: Calls `ArduinoCloud.update()` to keep the cloud connection alive and handle any changes.
- **`onLEDChange()`**: This function is called whenever the value of the LED property changes. It turns the LED on or off based on the property value.

### Steps to Upload the Sketch:

1. Open the modified sketch in the Arduino IDE.
2. Select your board and the correct COM port from the Tools menu.
3. Click the Upload button to upload the sketch to your Arduino board.
4. Open the Serial Monitor to check if the LED status is being printed.

### Controlling the LED:

- After successfully uploading the sketch, go to the Arduino IoT Cloud dashboard.
- Add a switch widget to control the LED property.
- Toggle the switch to turn the LED on and off remotely.

This setup allows you to control an LED using the Arduino IoT Cloud. Let me know if you need further assistance!