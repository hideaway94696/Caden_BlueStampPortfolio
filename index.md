<img width="508" alt="Screen Shot 2025-06-20 at 3 26 48 PM" src="https://github.com/user-attachments/assets/6b443033-006c-4b56-9564-ca08f3832369" /># Knee Rehabilitation Device

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



# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your second milestone, explain what you've worked on since your previous milestone. You can highlight:
- Technical details of what you've accomplished and how they contribute to the final goal
- What has been surprising about the project so far
- Previous challenges you faced that you overcame
- What needs to be completed before your final milestone 
```
# First Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/CaCazFBhYKs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

  The goal of my first milestone was to allow the flex sensor and accelerometer to retrieve data, and display it on the serial monitor. I encountered numerous issues while building and coding my first milestone.
  I started by building the circuit for my flex sensor. I used the big Arduino Elegoo microprocessor to begin with. I plugged the corresponding wires into power and ground, and also used a 10K ohm resistor to make sure the circuit didn't explode. I also had to use voltage dividers, and I learned that you can find out which ohm resistor to use using the formula Vout = (R2 / (R1 + R2)) * Vin. Becuase I need to analyze and print data from the flex sensor, there was a specific range of pins I could use. On the Arduino Elegoo microprocessor, these pins ranged only from A0 --> A15. I plugged all the corresponding wires and created a working circuit.
  After testing it on the Arduino Elegoo microprocessor with a code, I decided to transfer the circuit onto the actual microprocessor I would be using for the knee rehab device, which was the Arduino Wroom ESP32. However, when I did that, I encountered numerous issues. 
  I started by trying to fix my code. Although there were no errors, I thought that I may have defined a port incorrectly, or forgot to include certain libraries. Also, because the Arduino Wroom ESP32 has different pin numbers than the Arduino Elegoo, I had to use a pinout to determine which pin A0 corresponded to in the Arduino Wroom ESP32. I figured out that the pins containing the letter 'D' worked. However, even after changing the pin number on the code, the sensor was still unable to detect values. The only numbers in the serial monitor were either 0s or 4095s. Therefore, after determining that the code was not incorrect, I decided to change my approach and examine my circuit. Upon my examination, I realized that I had made a frivolous blunder; instead of using the 10K ohm resistor, I accidently used a 220 ohm resistor instead! Because there was not enough resistance, the flex sensor could not send any data to the serial monitor. 
  My next mini-goal was to detect and send values into the serial monitor from the accelerometer. Instead of hooking of the circuits on the Arduino Elegoo microprocessor, I decided to directly wire the circuits onto the Arduino Wroom ESP32. Getting the circuit to work was relatively simple, since no resistors were necessary. I had some trouble with the code, however. On one of the lines, I was telling the computer it was failing to retreive data when in reality, it was actually succeeding. Therefore, despite the fact that the acceleromter was working, the computer was stopping the program before the accelerometer could send data. \
  For my second milestone, I intend on adding bluetooth so an app on a phone can retrieve data values. I also intend on adding a power bank, so I don't need to continously plug my device into my computer for it to work. Finally, I need to attach the device onto a knee brace so i can accuratley detect values
  
For your first milestone, describe what your project is and how you plan to build it. You can include:
- An explanation about the different components of your project and how they will all integrate together
- Technical progress you've made so far
- Challenges you're facing and solving in your future milestones
- What your plan is to complete your project

# Schematics 
```Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. ```
<img width="508" alt="Screen Shot 2025-06-20 at 3 33 19 PM" src="https://github.com/user-attachments/assets/6695df6b-a969-4e7e-b170-94c6fcf848ff" />

# Code

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
