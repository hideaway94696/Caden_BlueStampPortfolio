# Knee Rehabilitation Device

The Knee Rehabilitation Device is a wearable system designed to assist patients recovering from knee injuries or surgeries by tracking joint movement and providing real-time feedback through the use of buzzers and LEDs. It has numerous integrated sensors, and can be used in both clinical settings and at home. One of the biggest challenges I faced during this project was ensuring the sensors were retrieving accurate data.
```
You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->

```
| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Caden Y | Mission San Jose High School | Mechanical Engineering | Incoming Sophomore
```
**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE


```
# Second Milestone
```
**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
```
# Code
Refer to Appendix (Milestone 2 Code)


# Schematics
![image](https://github.com/user-attachments/assets/e0ed54cf-292d-4fa4-9275-32e36ba7ce25)
Figure 2: Flex Sensor detached from breadboard but still connected. Accelerometer attached and wired to breadboard.
```
```
The goal of my second milestone was to attach all the major components onto the knee brace. Throughout the process, I encountered a number of technical challenges that required troubleshooting and iterative problem-solving.

I began by soldering the headers onto the accelerometer. During this process, I accidentally created several short circuits, which interfered with the functionality of the accelerometer. To fix this, I had to carefully desolder the connections and try again. After some difficulty, I successfully soldered the headers, allowing me to mount the accelerometer onto the breadboard.

I also learned how an accelerometer works. The Adafruit LSM6DS33 Accelerometer contains an extremely small mass and spring in order to determine acceleration in all three axes. Because F = m * a (Newton's Second Law) and F = k * x (Hooke's Law), we can find out acceleration by substituting F for F, making m * a = k * x. Since m (mass), k (spring constant), and x (displacement of the spring from equilibrium position) are all known, we can find out acceleration by rearranging the equation to become: a = (k * x)/(m). The damper effectively minimizes vibrations to ensure the entire accelerometer doesn't vibrate indefinitely.
![image](https://github.com/user-attachments/assets/bc02a42b-5f1c-45a7-a9d1-817c68676eaf)

Furthermore, I decided to analyze how a flex sensor functions (because Kevin told me to). A flex sensor functions as a variable resistor, meaning its electrical resistance changes in response to bending. When the sensor is straight, it maintains a lower resistance. As it bends, the resistance increases proportionally to the degree of flexion. This change occurs due to conductive ink particles embedded in the sensor; as the sensor bends, these particles move further apart, resulting in higher resistance. 
![image](https://github.com/user-attachments/assets/112043ec-faf5-45d9-b650-129286a9d6b8)


With the accelerometer working, I turned my attention to the flex sensor. I needed to detach it from the breadboard while maintaining a stable electrical connection. To achieve this, I soldered wires directly to the sensor and then reconnected it to the breadboard. I tested the setup to ensure the sensor could accurately retrieve and display data on the serial monitor, which it initially did.

However, after leaving the project for a week, the flex sensor stopped working properly and began displaying a constant value of “4095” in the serial monitor. To diagnose the issue, I first wrote a simple test script to verify whether the problem was related to code or hardware. Since the script still produced 4095 consistently, I determined it was a hardware issue.

I reviewed my circuit against the schematics and confirmed all the wiring was correct. I also used a multimeter to test my soldered connections — all of which were intact. Upon closer inspection, I noticed that a key metal contact on the flex sensor had become bent and detached from the plastic housing. I replaced the damaged sensor with a new one, which resolved the issue immediately.

For my third milestone, I plan to: 1) Tune the output values of the flex sensor and accelerometer for accuracy, 2) Attach the power bank to make the device portable. At this stage, I can't transfer the circuit on the breadboard to the PCB or sew the device onto the knee brace, as doing so would make the setup permanent. I need to leave room for further modifications before finalizing the build.

```
For your second milestone, explain what you've worked on since your previous milestone. You can highlight:
- Technical details of what you've accomplished and how they contribute to the final goal
- What has been surprising about the project so far
- Previous challenges you faced that you overcame
- What needs to be completed before your final milestone 
```
# First Milestone

```**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**```

<iframe width="736" height="414" src="https://www.youtube.com/embed/YUhANFDKLhA" title="Caden Y. Milestone 1" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

The goal of my first milestone was to get the flex sensor and accelerometer to successfully collect data and display it on the serial monitor. Throughout the process, I encountered several challenges related to both circuit building and coding.

I began by assembling the circuit for the flex sensor using the larger Arduino Elegoo microcontroller. I connected the appropriate wires to power and ground and used a 10K ohm resistor to prevent short circuits. I also implemented a voltage divider, learning along the way that the resistor values could be calculated using the formula:
Vout = (R2 / (R1 + R2)) * Vin.

Since I needed to read data from the flex sensor, I had to use analog pins on the Elegoo board, which range from A0 to A15. After carefully wiring everything, I successfully created a working circuit.

Once the flex sensor functioned properly on the Elegoo board, I transferred the circuit to the microcontroller intended for the final knee rehab device—the Arduino Wroom ESP32. However, I ran into several issues.

I first assumed the problem was in the code. Even though there were no compilation errors, I suspected I had incorrectly defined a port or missed an essential library. Because the ESP32 has different pin configurations than the Elegoo board, I consulted a pinout diagram to determine the ESP32 equivalent of A0. I found that pins labeled with a ‘D’ worked, but even after updating the code, the serial monitor only displayed constant values—either 0 or 4095—which indicated a problem with input readings.

After confirming that the code was not the issue, I re-examined the circuit. That’s when I realized I had made a simple but critical mistake: I had used a 220 ohm resistor instead of the required 10K ohm resistor. This insufficient resistance prevented the flex sensor from transmitting accurate data.

Next, I turned to the accelerometer. This time, I decided to connect it directly to the ESP32 instead of prototyping on the Elegoo board first. The hardware setup was easier—no resistors were needed—but I faced a small coding issue. One line of code was incorrectly signaling a data retrieval failure, even though the accelerometer was working. As a result, the program halted before the data could be transmitted to the serial monitor.

For my second milestone, I plan to: 1) Integrate Bluetooth functionality so data can be sent to a mobile app, 2) Add a power bank to eliminate the need to keep the device plugged into a computer, 3) Mount the device onto a knee brace to begin collecting accurate movement data in a real-world setup.
```  
For your first milestone, describe what your project is and how you plan to build it. You can include:
- An explanation about the different components of your project and how they will all integrate together
- Technical progress you've made so far
- Challenges you're facing and solving in your future milestones
- What your plan is to complete your project
```
# Schematics 
```Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. ```
<img width="508" alt="Screen Shot 2025-06-20 at 3 33 19 PM" src="https://github.com/user-attachments/assets/6695df6b-a969-4e7e-b170-94c6fcf848ff" />

Figure 1: Flex Sensor and Accelerometer wired/connected to breadboard and Arduino ESP32. 

# Code
Refer to Appendix (Milestone 1 Code) 

```
# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
```

# Starter Project

<iframe width="736" height="414" src="https://www.youtube.com/embed/LLyRvk59FLk?list=PLe-u_DjFx7eui8dmPGji-0-slT8KydYv_" title="Caden Y. Starter Project" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Description - 
For my BlueStamp starter project, I chose to build RGB sliders. RGB sliders allow you to mix the colors red, green, and blue to create virtually any color within the RGB spectrum. For example, if I want to create a shade of purple, I can increase the saturation levels of red and blue while lowering the green. I chose this project because I thought it would be really interesting to create a device that visually demonstrates how different colors are formed from just three primary components. Additionally, I saw this as a great opportunity to improve my soldering skills and get comfortable with assembling circuits. Practicing on this project will help me avoid making major mistakes when I move on to my more intensive main project. 

Challenges - 
I encountered several challenges while building the RGB sliders, even though the project was relatively simple compared to other starter options. One issue I faced was ensuring the correct polarity of the LED lights. Typically, the longer leg of an LED indicates the positive side, but in this case, it corresponded to the negative. I had to be very careful not to get it wrong, since a mistake would require me to de-solder and reattach the LED entirely. Another obstacle was accidentally melting the plastic while soldering. Since it was my first time using a soldering iron, I had trouble applying it efficiently, which led to the plastic being exposed to high temperatures for too long. This weakened the structure of the project slightly, but thankfully it didn’t cause any major functional problems.

Next Steps - 
After finishing my starter project, I intend on refining my Arduino skills to ensure that building my intensive project will be easier. I also hope to finish my first milestone by the next few days. 

# Appendix
Milestone 1 Code
```cpp
#include <Adafruit_LSM6DS33.h>
#include <BleSerial.h>
// For SPI mode, we need a CS pin
#include <Wire.h>

Adafruit_LSM6DS33 lsm6ds33 {};
BleSerial ble;

void setup(void) {
  Serial.begin(115200);
  ble.begin("Values");
  while (!Serial)
    delay(10); // will pause Zero, Leonardo, etc until serial console opens

  Serial.println("Adafruit LSM6DS33 test!");

  //Wire.begin(21, 22);
  /*for(int i = 0; i <= 127; i ++) {
    Wire.beginTransmission(i);
    if(!Wire.endTransmission()){
      Serial.print("device found");
      Serial.print(i);
      Serial.println();
    }
  }
  */

  if (lsm6ds33.begin_I2C()) {
    // if (!lsm6ds33.begin_SPI(LSM_CS)) {
    // if (!lsm6ds33.begin_SPI(LSM_CS, LSM_SCK, LSM_MISO, LSM_MOSI)) {
    Serial.println("Failed to find LSM6DS33 chip");
    while (1) {
      delay(10);
    }
  }

  Serial.println("LSM6DS33 Found!");

  // lsm6ds33.setAccelRange(LSM6DS_ACCEL_RANGE_2_G);
  Serial.print("Accelerometer range set to: ");
  lsm6ds33.setAccelRange(LSM6DS_ACCEL_RANGE_16_G);
  switch (lsm6ds33.getAccelRange()) {
  case LSM6DS_ACCEL_RANGE_2_G:
    Serial.println("+-2G");
    break;
  case LSM6DS_ACCEL_RANGE_4_G:
    Serial.println("+-4G");
    break;
  case LSM6DS_ACCEL_RANGE_8_G:
    Serial.println("+-8G");
    break;
  case LSM6DS_ACCEL_RANGE_16_G:
    Serial.println("+-16G");
    break;
  }

  // lsm6ds33.setGyroRange(LSM6DS_GYRO_RANGE_250_DPS);
  Serial.print("Gyro range set to: ");
  lsm6ds33.setGyroRange(LSM6DS_GYRO_RANGE_2000_DPS);
  switch (lsm6ds33.getGyroRange()) {
  case LSM6DS_GYRO_RANGE_125_DPS:
    Serial.println("125 degrees/s");
    break;
  case LSM6DS_GYRO_RANGE_250_DPS:
    Serial.println("250 degrees/s");
    break;
  case LSM6DS_GYRO_RANGE_500_DPS:
    Serial.println("500 degrees/s");
    break;
  case LSM6DS_GYRO_RANGE_1000_DPS:
    Serial.println("1000 degrees/s");
    break;
  case LSM6DS_GYRO_RANGE_2000_DPS:
    Serial.println("2000 degrees/s");
    break;
  case ISM330DHCX_GYRO_RANGE_4000_DPS:
    break; // unsupported range for the DS33
  }

  // lsm6ds33.setAccelDataRate(LSM6DS_RATE_12_5_HZ);
  Serial.print("Accelerometer data rate set to: ");
  lsm6ds33.setAccelDataRate(LSM6DS_RATE_52_HZ);
  switch (lsm6ds33.getAccelDataRate()) {
  case LSM6DS_RATE_SHUTDOWN:
    Serial.println("0 Hz");
    break;
  case LSM6DS_RATE_12_5_HZ:
    Serial.println("12.5 Hz");
    break;
  case LSM6DS_RATE_26_HZ:
    Serial.println("26 Hz");
    break;
  case LSM6DS_RATE_52_HZ:
    Serial.println("52 Hz");
    break;
  case LSM6DS_RATE_104_HZ:
    Serial.println("104 Hz");
    break;
  case LSM6DS_RATE_208_HZ:
    Serial.println("208 Hz");
    break;
  case LSM6DS_RATE_416_HZ:
    Serial.println("416 Hz");
    break;
  case LSM6DS_RATE_833_HZ:
    Serial.println("833 Hz");
    break;
  case LSM6DS_RATE_1_66K_HZ:
    Serial.println("1.66 KHz");
    break;
  case LSM6DS_RATE_3_33K_HZ:
    Serial.println("3.33 KHz");
    break;
  case LSM6DS_RATE_6_66K_HZ:
    Serial.println("6.66 KHz");
    break;
  }

  // lsm6ds33.setGyroDataRate(LSM6DS_RATE_12_5_HZ);
  Serial.print("Gyro data rate set to: ");
  lsm6ds33.setGyroDataRate(LSM6DS_RATE_6_66K_HZ);
  switch (lsm6ds33.getGyroDataRate()) {
  case LSM6DS_RATE_SHUTDOWN:
    Serial.println("0 Hz");
    break;
  case LSM6DS_RATE_12_5_HZ:
    Serial.println("12.5 Hz");
    break;
  case LSM6DS_RATE_26_HZ:
    Serial.println("26 Hz");
    break;
  case LSM6DS_RATE_52_HZ:
    Serial.println("52 Hz");
    break;
  case LSM6DS_RATE_104_HZ:
    Serial.println("104 Hz");
    break;
  case LSM6DS_RATE_208_HZ:
    Serial.println("208 Hz");
    break;
  case LSM6DS_RATE_416_HZ:
    Serial.println("416 Hz");
    break;
  case LSM6DS_RATE_833_HZ:
    Serial.println("833 Hz");
    break;
  case LSM6DS_RATE_1_66K_HZ:
    Serial.println("1.66 KHz");
    break;
  case LSM6DS_RATE_3_33K_HZ:
    Serial.println("3.33 KHz");
    break;
  case LSM6DS_RATE_6_66K_HZ:
    Serial.println("6.66 KHz");
    break;
  }

  lsm6ds33.configInt1(false, false, true); // accelerometer DRDY on INT1
  lsm6ds33.configInt2(false, true, false); // gyro DRDY on INT2
}

void loop() {
  //  /* Get a new normalized sensor event */
  FlexValue = analogRead(FlexPin);
  Serial.print("Flex Sensor Value: ");
  Serial.println(FlexValue);
  ble.println("Flex Sensor Value: ");
  ble.println(FlexValue);


  Serial.print("hello");
  sensors_event_t accel;
  sensors_event_t gyro;
  sensors_event_t temp;
  lsm6ds33.getEvent(&accel, &gyro, &temp);

  Serial.print("\t\tTemperature ");
  Serial.print(temp.temperature);
  Serial.println(" deg C");

  /* Display the results (acceleration is measured in m/s^2) */
  Serial.print("\t\tAccel X: ");
  Serial.print(accel.acceleration.x);
  Serial.print(" \tY: ");
  Serial.print(accel.acceleration.y);
  Serial.print(" \tZ: ");
  Serial.print(accel.acceleration.z);
  Serial.println(" m/s^2 ");

  /* Display the results (rotation is measured in rad/s) */
  Serial.print("\t\tGyro X: ");
  Serial.print(gyro.gyro.x);
  Serial.print(" \tY: ");
  Serial.print(gyro.gyro.y);
  Serial.print(" \tZ: ");
  Serial.print(gyro.gyro.z);
  Serial.println(" radians/s ");
  Serial.println();

  ble.print("\t\tAccel X: ");
  ble.print(accel.acceleration.x);
  ble.print(" \tY: ");
  ble.print(accel.acceleration.y);
  ble.print(" \tZ: ");
  ble.print(accel.acceleration.z);
  ble.println(" m/s^2 ");

  delay(1000);

  //  // serial plotter friendly format

  //  Serial.print(temp.temperature);
  //  Serial.print(",");

  //  Serial.print(accel.acceleration.x);
  //  Serial.print(","); Serial.print(accel.acceleration.y);
  //  Serial.print(","); Serial.print(accel.acceleration.z);
  //  Serial.print(",");

  // Serial.print(gyro.gyro.x);
  // Serial.print(","); Serial.print(gyro.gyro.y);
  // Serial.print(","); Serial.print(gyro.gyro.z);
  // Serial.println();
  //  delayMicroseconds(10000);
}
```

Milestone 2 Code
```cpp
// Include required libraries for IMU, BLE, and I2C communication
#include <Adafruit_LSM6DS33.h>        // Library for LSM6DS33 accelerometer + gyroscope
#include <BleSerial.h>                // BLE communication over Serial
#include <Adafruit_Sensor.h>          // Unified sensor interface
#include <Wire.h>                     // I2C communication library

// Create LSM6DS33 IMU and BLE objects
Adafruit_LSM6DS33 lsm6ds33 {};
BleSerial ble;

// Define hardware pin constants
const int FlexPin = 35;   // Analog pin connected to the flex sensor
const int Buzzer = 23;    // Digital output pin connected to the buzzer
int FlexValue = 0;        // Variable to store analog value from flex sensor

void setup(void) {
  Serial.begin(115200);       // Start serial communication at 115200 baud
  ble.begin("Values");        // Initialize BLE with device name "Values"
  pinMode(FlexPin, INPUT);    // Set the flex sensor pin as input
  pinMode(Buzzer, OUTPUT);    // Set the buzzer pin as output

  while (!Serial) delay(10);  // Wait for Serial to be available (for boards like Leonardo)

  Serial.println("Adafruit LSM6DS33 test!");

  // Attempt to initialize the LSM6DS33 over I2C
  if (lsm6ds33.begin_I2C()) {
    Serial.println("Failed to find LSM6DS33 chip");
    while (1) delay(10);  // Stay in loop if initialization fails
  }

  Serial.println("LSM6DS33 Found!");

  // Set and confirm accelerometer range
  Serial.print("Accelerometer range set to: ");
  lsm6ds33.setAccelRange(LSM6DS_ACCEL_RANGE_16_G);
  switch (lsm6ds33.getAccelRange()) {
    case LSM6DS_ACCEL_RANGE_2_G: Serial.println("+-2G"); break;
    case LSM6DS_ACCEL_RANGE_4_G: Serial.println("+-4G"); break;
    case LSM6DS_ACCEL_RANGE_8_G: Serial.println("+-8G"); break;
    case LSM6DS_ACCEL_RANGE_16_G: Serial.println("+-16G"); break;
  }

  // Set and confirm gyroscope range
  Serial.print("Gyro range set to: ");
  lsm6ds33.setGyroRange(LSM6DS_GYRO_RANGE_2000_DPS);
  switch (lsm6ds33.getGyroRange()) {
    case LSM6DS_GYRO_RANGE_125_DPS: Serial.println("125 degrees/s"); break;
    case LSM6DS_GYRO_RANGE_250_DPS: Serial.println("250 degrees/s"); break;
    case LSM6DS_GYRO_RANGE_500_DPS: Serial.println("500 degrees/s"); break;
    case LSM6DS_GYRO_RANGE_1000_DPS: Serial.println("1000 degrees/s"); break;
    case LSM6DS_GYRO_RANGE_2000_DPS: Serial.println("2000 degrees/s"); break;
    case ISM330DHCX_GYRO_RANGE_4000_DPS: break; // Unsupported range for this chip
  }

  // Set and confirm accelerometer data rate
  Serial.print("Accelerometer data rate set to: ");
  lsm6ds33.setAccelDataRate(LSM6DS_RATE_52_HZ);
  switch (lsm6ds33.getAccelDataRate()) {
    case LSM6DS_RATE_SHUTDOWN: Serial.println("0 Hz"); break;
    case LSM6DS_RATE_12_5_HZ:   Serial.println("12.5 Hz"); break;
    case LSM6DS_RATE_26_HZ:     Serial.println("26 Hz"); break;
    case LSM6DS_RATE_52_HZ:     Serial.println("52 Hz"); break;
    case LSM6DS_RATE_104_HZ:    Serial.println("104 Hz"); break;
    case LSM6DS_RATE_208_HZ:    Serial.println("208 Hz"); break;
    case LSM6DS_RATE_416_HZ:    Serial.println("416 Hz"); break;
    case LSM6DS_RATE_833_HZ:    Serial.println("833 Hz"); break;
    case LSM6DS_RATE_1_66K_HZ:  Serial.println("1.66 KHz"); break;
    case LSM6DS_RATE_3_33K_HZ:  Serial.println("3.33 KHz"); break;
    case LSM6DS_RATE_6_66K_HZ:  Serial.println("6.66 KHz"); break;
  }

  // Set and confirm gyroscope data rate
  Serial.print("Gyro data rate set to: ");
  lsm6ds33.setGyroDataRate(LSM6DS_RATE_6_66K_HZ);
  switch (lsm6ds33.getGyroDataRate()) {
    case LSM6DS_RATE_SHUTDOWN: Serial.println("0 Hz"); break;
    case LSM6DS_RATE_12_5_HZ:   Serial.println("12.5 Hz"); break;
    case LSM6DS_RATE_26_HZ:     Serial.println("26 Hz"); break;
    case LSM6DS_RATE_52_HZ:     Serial.println("52 Hz"); break;
    case LSM6DS_RATE_104_HZ:    Serial.println("104 Hz"); break;
    case LSM6DS_RATE_208_HZ:    Serial.println("208 Hz"); break;
    case LSM6DS_RATE_416_HZ:    Serial.println("416 Hz"); break;
    case LSM6DS_RATE_833_HZ:    Serial.println("833 Hz"); break;
    case LSM6DS_RATE_1_66K_HZ:  Serial.println("1.66 KHz"); break;
    case LSM6DS_RATE_3_33K_HZ:  Serial.println("3.33 KHz"); break;
    case LSM6DS_RATE_6_66K_HZ:  Serial.println("6.66 KHz"); break;
  }

  // Configure data-ready interrupts on IMU
  lsm6ds33.configInt1(false, false, true);  // Accelerometer DRDY on INT1
  lsm6ds33.configInt2(false, true, false);  // Gyro DRDY on INT2
}

void loop() {
  // Read flex sensor value (analog input)
  FlexValue = analogRead(FlexPin);
  Serial.print("Flex Sensor Value: ");
  Serial.println(FlexValue);
  ble.println("Flex Sensor Value: ");
  ble.println(FlexValue);

  // Output simple debug string
  Serial.print("hello");

  // Read sensor event data from LSM6DS33
  sensors_event_t accel;
  sensors_event_t gyro;
  sensors_event_t temp;
  lsm6ds33.getEvent(&accel, &gyro, &temp);

  // Display temperature reading
  Serial.print("\t\tTemperature ");
  Serial.print(temp.temperature);
  Serial.println(" deg C");

  // Display accelerometer readings (X, Y, Z in m/s^2)
  Serial.print("\t\tAccel X: ");
  Serial.print(accel.acceleration.x);
  Serial.print(" \tY: ");
  Serial.print(accel.acceleration.y);
  Serial.print(" \tZ: ");
  Serial.print(accel.acceleration.z);
  Serial.println(" m/s^2 ");

  // Display gyroscope readings (X, Y, Z in radians/s)
  Serial.print("\t\tGyro X: ");
  Serial.print(gyro.gyro.x);
  Serial.print(" \tY: ");
  Serial.print(gyro.gyro.y);
  Serial.print(" \tZ: ");
  Serial.print(gyro.gyro.z);
  Serial.println(" radians/s ");
  Serial.println();

  // Send acceleration data over BLE
  ble.print("\t\tAccel X: ");
  ble.print(accel.acceleration.x);
  ble.print(" \tY: ");
  ble.print(accel.acceleration.y);
  ble.print(" \tZ: ");
  ble.print(accel.acceleration.z);
  ble.println(" m/s^2 ");

  // Trigger buzzer based on sensor conditions:
  // Case 1: If Z-acceleration is negative (e.g., device flipped)
  if (accel.acceleration.z < 0) {
    digitalWrite(Buzzer, HIGH);
  }
  // Case 2: If flex sensor exceeds threshold (e.g., finger bent strongly)
  else if (FlexValue > 3000) {
    digitalWrite(Buzzer, HIGH);
    delay(200);
    digitalWrite(Buzzer, LOW);
  }
  // Otherwise, keep buzzer off
  else {
    digitalWrite(Buzzer, LOW);
  }

  delay(1000);  // Wait 1 second before next reading

  // Optional: Serial Plotter friendly format
  // (commented out)
  /*
  Serial.print(temp.temperature);
  Serial.print(",");

  Serial.print(accel.acceleration.x);
  Serial.print(","); Serial.print(accel.acceleration.y);
  Serial.print(","); Serial.print(accel.acceleration.z);
  Serial.print(",");

  Serial.print(gyro.gyro.x);
  Serial.print(","); Serial.print(gyro.gyro.y);
  Serial
  */
}
```
