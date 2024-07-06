    To control multiple LEDs using the Arduino IoT Cloud, you can set up multiple properties, each corresponding to an LED. Here’s a guide on how to do it:

### Hardware Setup:

1. **Components:**
   - Arduino board with Wi-Fi capability (e.g., Arduino MKR WiFi 1010, Arduino Nano 33 IoT)
   - Multiple LEDs (e.g., 3 LEDs)
   - 220-ohm resistors (one for each LED)
   - Breadboard
   - Jumper wires

2. **Connections:**
   - Connect the longer leg (anode) of each LED to a different digital pin on the Arduino (e.g., `D5`, `D6`, and `D7`).
   - Connect the shorter leg (cathode) of each LED to one end of a 220-ohm resistor.
   - Connect the other end of each 220-ohm resistor to the `GND` pin on the Arduino.

### Setting Up Arduino IoT Cloud:

1. **Sign up and Create a Thing:**
   - Sign up for an account on [Arduino IoT Cloud](https://create.arduino.cc/iot/things).
   - Click on "Create Thing" to create a new project.
   - Name your Thing and add properties for each LED.

2. **Configure the Thing Properties:**
   - Add a property for each LED:
     - Name: LED1, LED2, LED3 (or similar)
     - Type: boolean
     - Update: on change

3. **Generate and Download the Sketch:**
   - After adding the properties, click on "Setup" to configure the device.
   - Select your board type (e.g., Arduino MKR WiFi 1010).
   - Follow the instructions to set up the device and connect it to your Wi-Fi network.
   - Download the generated sketch to your computer.

### Code:

Here is a modified version of the generated sketch to control multiple LEDs:

```cpp
#include "thingProperties.h"

#define LED1_PIN 5  // Pin where LED1 is connected
#define LED2_PIN 6  // Pin where LED2 is connected
#define LED3_PIN 7  // Pin where LED3 is connected

void setup() {
  // Initialize serial and wait for port to open:
  Serial.begin(9600);
  delay(1500); 

  // Set the LED pins as outputs
  pinMode(LED1_PIN, OUTPUT);
  pinMode(LED2_PIN, OUTPUT);
  pinMode(LED3_PIN, OUTPUT);

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

// This function gets called whenever the value of LED1 changes in Arduino IoT Cloud
void onLED1Change() {
  if (LED1) {
    digitalWrite(LED1_PIN, HIGH);  // Turn LED1 on
    Serial.println("LED1 is ON");
  } else {
    digitalWrite(LED1_PIN, LOW);   // Turn LED1 off
    Serial.println("LED1 is OFF");
  }
}

// This function gets called whenever the value of LED2 changes in Arduino IoT Cloud
void onLED2Change() {
  if (LED2) {
    digitalWrite(LED2_PIN, HIGH);  // Turn LED2 on
    Serial.println("LED2 is ON");
  } else {
    digitalWrite(LED2_PIN, LOW);   // Turn LED2 off
    Serial.println("LED2 is OFF");
  }
}

// This function gets called whenever the value of LED3 changes in Arduino IoT Cloud
void onLED3Change() {
  if (LED3) {
    digitalWrite(LED3_PIN, HIGH);  // Turn LED3 on
    Serial.println("LED3 is ON");
  } else {
    digitalWrite(LED3_PIN, LOW);   // Turn LED3 off
    Serial.println("LED3 is OFF");
  }
}
```

### Explanation:

- **`LED1_PIN`, `LED2_PIN`, `LED3_PIN`**: These are the digital pins where the LEDs are connected (`D5`, `D6`, `D7`).
- **`setup()`**: Initializes serial communication, sets the LED pins as outputs, and connects to the Arduino IoT Cloud.
- **`loop()`**: Calls `ArduinoCloud.update()` to keep the cloud connection alive and handle any changes.
- **`onLED1Change()`, `onLED2Change()`, `onLED3Change()`**: These functions are called whenever the value of the respective LED property changes. They turn the corresponding LED on or off based on the property value.

### Steps to Upload the Sketch:

1. Open the modified sketch in the Arduino IDE.
2. Select your board and the correct COM port from the Tools menu.
3. Click the Upload button to upload the sketch to your Arduino board.
4. Open the Serial Monitor to check if the LED statuses are being printed.

### Controlling the LEDs:

- After successfully uploading the sketch, go to the Arduino IoT Cloud dashboard.
- Add switch widgets to control each LED property.
- Toggle the switches to turn the LEDs on and off remotely.

This setup allows you to control multiple LEDs using the Arduino IoT Cloud. Let me know if you need further assistance!