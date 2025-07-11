# Knee Rehabilitation Device

The Knee Rehabilitation Device is a wearable system designed to assist patients recovering from knee injuries or surgeries by tracking joint movement and providing real-time feedback through the use of buzzers and LEDs. It has numerous integrated sensors, and can be used in both clinical settings and at home. One of the biggest challenges I faced during this project was ensuring the sensors were retrieving accurate data.

| **Name** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Caden Y | Mission San Jose High School | Mechanical Engineering | Incoming Sophomore |

<img width="845" height="1148" alt="image" src="https://github.com/user-attachments/assets/cf1669dc-503e-4fa8-9225-8a1b2ea448a2" />

# Modifications
<iframe width="806" height="453" src="https://www.youtube.com/embed/Xnd7YUXufAk" title="Caden Y.  Modification" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## Descriptions
When the user is standing, the LED strip should display yellow, indicating an idle state. When the user is bending down, the LED should turn red, signaling that they haven't yet reached the proper squat angle. Finally, when the user reaches a perfect squat, the LED strip will progressively fill with green, pixel by pixel. This acts as a quick 1-second timer to help the user maintain the squat position for the correct duration.

## Challenges
One of the main issues I faced while working with the LED strips was getting the green lights to progressively fill the entire strip. After some research, I found that I needed two key functions to make this work: one to turn on the green lights progressively, and another to reset the strip. To light the LEDs progressively, I used the millis() function, which returns the number of milliseconds since the program started. I stored this value in an unsigned long variable (which holds only nonnegative values). Then, I created an if statement that checked two conditions: 1) At least 50 milliseconds had passed since the last update (lastGreenUpdate), and 2) The number of green pixels lit (greenPixelCount) was still less than the total number of pixels (NUM_PIXELS). If both conditions were met, the function would light the next pixel green. I did this by assigning it an RGB value (0, 255, 0), calling strip.show() to update the strip, and then incrementing the counter so the next pixel could be lit on the next pass. To reset the green lights, I first reset the greenPixelCount variable back to zero. Then, I used a for loop to go through each pixel and turn it off by setting its color to black (which is equivalent to RGB = 0, 0, 0). I ended this function with a call to strip.show(), which effectively cleared all the LEDs on the strip. 

While tuning my modifications, I also learned how an LED strip works. First, imagine a strip with 18 NeoPixels. Each pixel has 3 tiny LEDs inside, with the colors red, green, and blue. Each pixel also has its own controller chip which is able to receive data from the Arduino and passes the remaining data along to the next pixel. When I upload my code, the Arduino will send a digital signal that contains the color and brightness data for each pixel in order. Pixel 1 will take the first 3 bytes (R, G, and B), Pixel 2 will take the next 3 bytes, and so on. Each byte contains the information necessary to project a certain color, and contains 8 bits (refer to Figure 3G). A bit is the smallest unit of data in computing, representing a single binary digit (0 or 1).

<img width="999" height="339" alt="image" src="https://github.com/user-attachments/assets/c97042d9-33cc-4e22-a058-d77581d6b088" />
Figure 4A: 3 Pixels and 8 Bits per Pixel


# Final Milestone
<iframe width="806" height="453" src="https://www.youtube.com/embed/kT8-kyL3Cao" title="Caden Y.  Milestone 3" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
 
## Schematics (With Modifications)
<img width="1225" height="984" alt="image" src="https://github.com/user-attachments/assets/c1e8b089-3bf5-429e-8dc1-95c0abda0f1d" />

Figure 3: Schematics with Modifications (LED Strip)

## Description
For my final milestone, the device must function properly, meaning it is able to track incorrect squat form and beep when it is detected. If the user reaches the proper angle of a squat, the buzzer should also be able to beep. I also added my modifications in the final milestone, which is an 18 pixel LED Strip containing three modes. Because of these specific conditions, I met numerous challenges while finishing the project.

## Challenges
One major obstacle I had to overcome was the placement of the accelerometer. I realized that placing the accelerometer on the breadboard was not the best idea, since the accelerometer provided little to no data. This is because I placed the breadboard on an area (on the knee brace) that moves very little, meaning the accelerometer is exposed to little to no movement as well. To solve this issue, I had to remove the accelerometer from the breadboard and figure out an optimal placement for the accelerometer. The first step to overcoming this obstacle was to desolder the headers from the accelerometer. However, because the desoldering pump could not fully remove all the solder from the accelerometer, I was left with no option but to snip the headers off the accelerometer. The next step was to determine an optimal placement for the accelerometer. After doing some research, I realized that placing the accelerometer near the upper thigh would be most helpful for my project (refer to Figure 3A to see the positions of accelerometers on a knee rehab device). The reason why I chose to place the accelerometer on the upper thigh was primarily because the knee brace did not extend all the way to the calf. The final step was learning how to sew. An amazing instructor taught me the basics of a running stitch, which was necessary to sew the accelerometer on the knee brace.

To tune the values for the device, I needed to analyze the graphs of numerous proper squats (refer to Figure 3B to see a chart displaying values for 'good' squats) and do the same for improper squats (refer to Figure 3C to see a chart displaying values for 'bad' squats). 

![image](https://github.com/user-attachments/assets/df5b3892-76a6-4d6e-a23a-15c9766d811c)

Figure 3A: Possible placements of accelerometers on a knee rehab device (thigh and calf). 

![image](https://github.com/user-attachments/assets/fbe8d34a-06c9-424f-a469-a362e45388d8)

Figure 3B: Graph displaying data values for 6 'proper' squats. 'PRY' represents 'Pitch, Roll, and Yaw', and is the Y-axis. Time represents the x-axis, and is measured in tenths of a second.

![image](https://github.com/user-attachments/assets/d4c6071c-d202-43de-8f02-92ae1495725d)

Figure 3C: Graph displaying data values for an 'improper' vs 'proper' squat. Note that the green value experiences the greatest change, and therefore it would be best to add thresholds to the green value. 

Another important aspect of my project was understanding how pitch, roll, and yaw work. Pitch, yaw, and roll are terms describing rotations of an object around three perpendicular axes: the longitudinal (roll), lateral (pitch), and vertical (yaw) axes. To visualize pitch, think of an airplane tilting its nose up and down. To visualize roll, think of an airplane banking/tilting sideways. To visualize yaw, think of an airplane turning left/right (refer to Figure 3D to see pitch, roll, and yaw).

![image](https://github.com/user-attachments/assets/ae34449f-cf00-406b-aedd-4c9e05483e71)

Figure 3D: Pitch, Roll, and Yaw on an airplane. 

I also needed to export data from the Arduino serial monitor into a Google Sheet for proper analysis. However, the Arduino serial monitor doesn’t format the values correctly, so I had to find an alternative solution. To address this, I downloaded CoolTerm, an application that facilitates communication with devices connected via serial ports. In order for CoolTerm to export the data into a Google Sheet, I had to format it as CSV (Comma Separated Values). Once formatted, I was able to import the data into the Google Sheet and analyze it effectively (refer to Figure 3E for image of organized data).

![image](https://github.com/user-attachments/assets/2736e4d1-b35c-4eaa-a15b-371582ebcbbc)
Figure 3E: Properly Organized Data in a Google Sheet

<!-- **Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE -->
One more major obstacle I encountered involved an issue with the Arduino ESP32. I noticed that whenever I bent my knee slightly, the Serial Monitor displayed a "Hardware NACK" error. At that point, the accelerometer values would freeze, and the system would become unresponsive until I manually reset the ESP32. To troubleshoot, I started by isolating the accelerometer. I wrote a minimal script with the sole purpose of printing out its values, but the same error persisted. I then observed that the error consistently appeared whenever the piezoelectric buzzer was activated. This led me to suspect the buzzer, so I carefully reviewed its connections and confirmed the schematic was correct. With the buzzer and accelerometer ruled out, I had no choice but to investigate the microcontroller itself. After replacing the ESP32 with a new one, the code was able to work. 

Unfortunately, due to the changes I made, the accelerometer data I had previously logged was no longer accurate. I needed to re-analyze the data by repeatedly performing both proper and improper squats while adjusting the update frequency. After making several minor modifications, I was able to generate the following graph:
![image](https://github.com/user-attachments/assets/e5c96121-69aa-43aa-82fd-ae7619a27cfc)
Figure 3F: New Graph of Squat Values 

Upon examining the graph, I noticed that the difference between proper and improper squats was minimal (see Figure 3F). To improve accuracy, I decided to isolate a single variable, pitch, yaw, or roll, that showed the most variation. In my case, I chose to focus on roll, since bending the knees inward caused the roll value to change significantly (every improper squat had a difference of around 15-20 degrees). This made it a strong candidate for meaningful analysis. Based on the graph, I set thresholds at its minimums, and after implementing those changes, the system began functioning correctly again. 

After finally tuning my device, I had to solder everything together. However, during the process, I encountered a surprisingly difficult obstacle that took me eight hours to resolve. Back in my first milestone, while building the circuit that included both the flex sensor and the accelerometer, I mistakenly believed a 220-ohm resistor was required for the flex sensor. When assembling the circuit, I accidentally grabbed a 10k-ohm resistor instead, and ironically, it turned out to be the perfect match for the circuit to function properly. But later, when soldering everything together, I reverted to my original (incorrect) assumption and used a 220-ohm resistor. This caused the data from the flex sensor to behave erratically. Initially, I suspected the sensor itself was faulty. To verify, I built a simple test circuit and wrote a basic script to check the sensor’s performance. Strangely enough, it worked, mainly because I again coincidentally used a 10k-ohm resistor, thinking it was 220 ohms. With the sensor appearing functional, I shifted focus to the microcontroller. I tried swapping multiple microcontrollers, even using an Arduino Uno, but the flex sensor continued to read data properly. This ruled out the microcontroller as the issue. I then suspected my soldering. I thought perhaps I had shorted something on the PCB. However, after extensive multimeter testing, everything checked out fine. Finally, while taking a break and drinking some water, it occurred to me to double-check the resistor I had used on the breadboard during prototyping. To my surprise, it was a 10k-ohm resistor—not 220 ohms. After experimenting a bit more, I discovered that a 47k-ohm resistor gave even smoother data readings. Replacing the 220-ohm resistor with the 47k-ohm one solved the problem, and the flex sensor finally worked correctly.


# Second Milestone

<iframe width="743" height="418" src="https://www.youtube.com/embed/2_FaPk_xcjo" title="Caden Y. Milestone 2" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## Schematics
![image](https://github.com/user-attachments/assets/e0ed54cf-292d-4fa4-9275-32e36ba7ce25)

Figure 2: Flex Sensor detached from breadboard but still connected. Accelerometer attached and wired to breadboard.


## Description
The goal of my second milestone was to attach all the major components onto the knee brace and add a buzzer that beeps when certain values are detected (refer to Figure 2 for a schematic of all the components). As of now, when flex sensor values reach over 3200, the buzzer will release short beeps that indicate the desired squat angle has been reached. Additionally, when the acceleration (in the x-axis) is under zero, the buzzer will release a long beep until acceleration is nonnegative. None of these values are properly tuned, though, so I'll need to spend some time enhancing the accuracy of the device. I also worked on connecting the Arduino ESP32 to Bluetooth. The Arduino ESP32 supports the use of BLE (otherwise known as Bluetooth Low Energy). BLE enables short-range communication using low power consumption. It works by using the 2.4 GHz ISM band, which is a globally allocated radio frequency band used for various applications like Bluetooth, Wi-Fi, and microwave ovens. The Arduino ESP32 acts as a peripheral, which broadcasts data and can be connected to by a central, and in this scenario, is my phone. In general, the BLE Communication Flow can be described in 4 steps: 1) Advertising (peripheral makes its presence known), 2) Scanning (the central scans for nearby peripherals), 3) Connection (central connects to peripheral), and 4) Data Exchange. Throughout the process of finishing my second milestone, I encountered a number of technical challenges that required troubleshooting and iterative problem-solving.

## Challenges
I began by soldering the headers onto the accelerometer. During this process, I accidentally created several short circuits, which interfered with the functionality of the accelerometer. To fix this, I had to carefully desolder the connections and try again. After some difficulty, I successfully soldered the headers, allowing me to mount the accelerometer onto the breadboard.

I also learned how an accelerometer works. The Adafruit LSM6DS33 Accelerometer contains an extremely small mass and spring in order to determine acceleration in all three axes (refer to Figure 2A). Because F = m * a (Newton's Second Law) and F = k * x (Hooke's Law), we can find out acceleration by substituting F for F, making m * a = k * x. Since m (mass), k (spring constant), and x (displacement of the spring from equilibrium position) are all known, we can find out acceleration by rearranging the equation to become: a = (k * x)/(m). The damper effectively minimizes vibrations to ensure the entire accelerometer doesn't vibrate indefinitely. 
![image](https://github.com/user-attachments/assets/bc02a42b-5f1c-45a7-a9d1-817c68676eaf)
Figure 2A: Adafruit LSM6DS33 Accelerometer Schematic

Furthermore, I decided to analyze how a flex sensor functions. A flex sensor functions as a variable resistor, meaning its electrical resistance changes in response to bending. When the sensor is straight, it maintains a lower resistance. As it bends, the resistance increases proportionally to the degree of flexion (refer to Figure 2B). This change occurs due to conductive ink particles embedded in the sensor; as the sensor bends, these particles move further apart, resulting in higher resistance. 
![image](https://github.com/user-attachments/assets/112043ec-faf5-45d9-b650-129286a9d6b8)
Figure 2B: How a Flex Sensor Functions

Because the buzzer was a necessary part of my second milestone, I needed to understand how a piezo buzzer functioned. After doing some research, I was able to figure out that the piezo buzzer works by using the piezoelectric effect, where a piezoelectric material, like a small ceramic disc (refer to Figure 2C), deforms when a voltage is applied to it. This deformation causes a vibration in the material, and these small vibrations create sound waves. 
![image](https://github.com/user-attachments/assets/c32c6df0-d5db-43b7-91d0-ca813f9093fc)
Figure 2C: How a Piezoelectric Buzzer Functions

With the accelerometer working, I turned my attention to the flex sensor. I needed to detach it from the breadboard while maintaining a stable electrical connection. To achieve this, I soldered wires directly to the sensor and then reconnected it to the breadboard. I tested the setup to ensure the sensor could accurately retrieve and display data on the serial monitor, which it initially did.

However, after leaving the project for a week, the flex sensor stopped working properly and began displaying a constant value of “4095” in the serial monitor. To diagnose the issue, I first wrote a simple test script to verify whether the problem was related to code or hardware. Since the script still produced 4095 consistently, I determined it was a hardware issue.

I reviewed my circuit against the schematics and confirmed all the wiring was correct. I also used a multimeter to test my soldered connections — all of which were intact. Upon closer inspection, I noticed that a key metal contact on the flex sensor had become bent and detached from the plastic housing. I replaced the damaged sensor with a new one, which resolved the issue immediately.

Another part of my second milestone was to incorporate a buzzer that will beep when a certain value from the accelerometer or flex sensor is detected. Refer to the Appendix (Milestone 2 Code) to see my implementation of an if-else statement that activated the buzzer when necessary.

## Next Steps
For my third milestone, I plan to: 1) Tune the output values of the flex sensor and accelerometer for accuracy, 2) Attach the power bank to make the device portable. At this stage, I can't transfer the circuit on the breadboard to the PCB or sew the device onto the knee brace, as doing so would make the setup permanent. I need to leave room for further modifications before finalizing the build.


# First Milestone

<iframe width="736" height="414" src="https://www.youtube.com/embed/YUhANFDKLhA" title="Caden Y. Milestone 1" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## Schematics 
<img width="508" alt="Screen Shot 2025-06-20 at 3 33 19 PM" src="https://github.com/user-attachments/assets/6695df6b-a969-4e7e-b170-94c6fcf848ff" />

Figure 1: Flex Sensor and Accelerometer wired/connected to breadboard and Arduino ESP32. 


## Description
The goal of my first milestone was to get the flex sensor and accelerometer to successfully collect data and display it on the serial monitor. As of now, whenever the flex sensor detects bending/resistance, it will display the corresponding values in the serial monitor under "Flex Sensor Values". Additionally, whenever the accelerometer detects acceleration along the x, y, or z axes, it will display the corresponding values of acceleration in the serial monitor under "Acceleration x: --  y: --  z: --". Throughout the process of finishing my first milestone, I encountered several challenges related to both circuit building and coding.

## Challenges
I began by assembling the circuit for the flex sensor using the larger Arduino Elegoo microcontroller. I connected the appropriate wires to power and ground and used a 10K ohm resistor to prevent short circuits. I also implemented a voltage divider, learning along the way that the resistor values could be calculated using the formula:
Vout = (R2 / (R1 + R2)) * Vin.

Since I needed to read data from the flex sensor, I had to use analog pins on the Elegoo board, which range from A0 to A15. After carefully wiring everything, I successfully created a working circuit.

Once the flex sensor functioned properly on the Elegoo board, I transferred the circuit to the microcontroller intended for the final knee rehab device—the Arduino Wroom ESP32. However, I ran into several issues.

I first assumed the problem was in the code. Even though there were no compilation errors, I suspected I had incorrectly defined a port or missed an essential library. Because the ESP32 has different pin configurations than the Elegoo board, I consulted a pinout diagram to determine the ESP32 equivalent of A0. I found that pins labeled with a ‘D’ worked, but even after updating the code, the serial monitor only displayed constant values—either 0 or 4095—which indicated a problem with input readings.

After confirming that the code was not the issue, I re-examined the circuit. That’s when I realized I had made a simple but critical mistake: I had used a 220 ohm resistor instead of the required 10K ohm resistor (refer to Figure 1 for a schematic of all the components). This insufficient resistance prevented the flex sensor from transmitting accurate data.

Next, I turned to the accelerometer. This time, I decided to connect it directly to the ESP32 instead of prototyping on the Elegoo board first. The hardware setup was easier since no resistors were needed, but I faced a small coding issue. One line of code was incorrectly signaling a data retrieval failure, even though the accelerometer was working. As a result, the program halted before the data could be transmitted to the serial monitor. Refer to the Appendix (Milestone 1 Code) to see how I resolved this issue.

## Next Steps
For my second milestone, I plan to: 1) Integrate Bluetooth functionality so data can be sent to a mobile app, 2) Add a power bank to eliminate the need to keep the device plugged into a computer, 3) Mount the device onto a knee brace to begin collecting accurate movement data in a real-world setup.


# Bill of Materials

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| **Arduino ESP32S** | **Microcontroller** | **$13** | <a href ="https://www.amazon.com/Teyleten-Robot-ESP-WROOM-32-Development-Microcontroller/dp/B08246MCL5/ref=sr_1_10?crid=2D7JWTV607DLJ&dib=eyJ2IjoiMSJ9.muXyANMuy8-oE8Y74H25ZmbeUH4QVoqL4p3vOP7PNHiBTcD3JF0f6YN8ckv2KkCEOtjdM6pcU0Zd_eBIr7_sHSmSaozJEn_rDNaMAMh2QyJKdVaUYd-7KufZomvs7MwoBqc18GN4M95rCLYntJ485_MPH3aN3ksSaCAkH1stHUrgqq8ASKqi2s5Xjg1l75sKwzfVeLzZnyxOK1JrIkbL8Npos_fdM1NpA__gRTq6kdXxYmj0mxAwh5BRkrR_VIFc_-eJR1XljSUyVyT_LzFsC_ZAboFgOV0wgP2vWe0FNQI.qmVWK2VUk1ZviU20HVRBNOdTnmbUm3B8zNGwGf7xcwc&dib_tag=se&keywords=arduino%2Besp32&qid=1751557896&s=electronics&sprefix=arduino%2Besp32%2Celectronics%2C228&sr=1-10&th=1"> Link </a> |
| **BodyProx Knee Sleeve** | **Keeps Components on Knee** | **$15** | <a href ="https://www.amazon.com/gp/aw/d/B0987XN6QH/?_encoding=UTF8&pd_rd_plhdr=t&aaxitk=5aed513eac49a60526c6d9777d9d93db&hsa_cr_id=7875900910501&qid=1719864251&sr=1-1-9e67e56a-6f64-441f-a281+df67fc737124&ref_=sbx_be_s_sparkle_mcd_asin_0_mariomsg&pd_rd_w=qsSVr&content-id=amzn1.sym.8591358d-1345-4efd-9d50-5bd4e69cd942%3Aamzn1.sym.8591358d-1345-4efd-9d50-5bd4e69cd942&pf_rd_p=8591358d-1345-4efd-9d50-5bd4e69cd942&pf_rd_r=PA56EJATP874WHNCNE6H&pd_rd_wg=ihoKq&pd_rd_r=388c0a8d-3fca-4ec1-a970-cdcf8c7489c9&th=1"> Link </a> |
| **Adafruit Flex Sensor** | **Measures Bend of Knee** | **$18** | <a href ="https://www.amazon.com/Adafruit-Long-Flex-sensor-ADA182/dp/B01BNNNS5Q/ref=sr_1_3?crid=1GEOF65S7SCLW&dib=eyJ2IjoiMSJ9.lhZF8xWpz39rDzMy73v%20TT23Ss_RjBfj1RB7kEAbJ9D0yBHgcKw1YMgsMIaCD6oj4egLyFTXzJPJROjBXBNuLyvP3hfVG8V9B_gtFq3L7mxpoS6d2cm8cA453b16MvFuDDX9kD9oJbk3173icFBHyeg2y1Vvlqp7qWjWgna1VVPTA_OUwnV1JetfY2OnlDWNX90LumgmwPODB1DZMXj6Kx2Tzoz5_4Zp1N0XQmSndWHGVCr9QXxmgB0P2268U5jbYeGzZgUcZSGgiQ8JObtVoiz5yTr6MRas9v0iQbuOp6U.q-rFWTMu_qQemed_1UjkLOc3NMOPC5JBJq03fSe7z5M&dib_tag=se&keywords=flex+sensor&qid=1719864423&s=industrial&sprefix=flex+sensor%2Cindustrial%2C138&sr=1-3"> Link </a> |
| **Adafruit LSM6DS3TR Accelerometer** | **Detects Acceleration along 3 Axes** | **$20** | <a href = "https://www.adafruit.com/product/5543"> Link </a> |
| **Piezo Buzzer** | **Beeps when Incorrect Form Detected** | **$6** | <a href = "https://www.amazon.com/Cylewet-Terminals-Electronic-Electromagnetic-Impedance/dp/B01NCOXB2Q/ref=sr_1_6?crid=2LHY512NYTX03&dib=eyJ2IjoiMSJ9.v9xp9jV7C-sQT7j4p0UIV_xVKzU8DDa55Zy7nzfVmYaimJdByrZMfNvEm2fHDR0za4DaPd8brwiVZEi-IHCgo2sBg8k3EJMcmg-sVR90kJcP9oOf8zSFh1iWZlw1PJrUObynF7hsFTlUl4Mjw1yLhEb5aveIgXUMHiN2P2TdYaKK_yFtrf95J7L5mXjX1oEvZH1Cnvc-xk1Nel5twsTKJkHHc66-oivwv6bs2SLxMd-EUIVOKxL7DltKGCHB1GZoH1BXVwGU2Y8otebOLO8e3y7KD-K5CpOcO4zjO47owcg.r5O90tcYn3TNrCpGtKRJVSosnV60zYqj_ue96Klj1DU&dib_tag=se&keywords=piezo+buzzer&qid=1719864686&s=industrial&sprefix=piezo+buzzer%2Cindustrial%2C134&sr=1-6"> Link </a>|
| **220 Ohm Resistor** | **Provides Resistance for Flex Sensor** | **$4** | <a href = "https://www.amazon.com/California-JOS-Resistance-CJ50-004-220/dp/B0BDKQSZHM/ref=sr_1_3?crid=3SFKVJ53VBE4D&dib=eyJ2IjoiMSJ9.pq8IXZtwkjU13efAoUQ01zBUlR2f2Y7f-E16x07ioTKL_3aH4OzxTsM5DaSXBRXLlhDD4Gfyi6ew3fKoaYqDPwQ4kz8UMw4sIKhxX-mOOGXbZIFugasSgq4TqktqYo7m41HoP4MVxl_vrYBUGouW0ZyPQiwjtRqm_j2j1oW8gVs3M8LZa4qfKynQtLAt3V-H_CPBIVkZFBnXwfPXZ-BMyF7bm3BwZMNd3BbPyqMudHuDm3yiBdBZN6r88lAHwf28Ma-If8go4xBKPFicl4GUYWOkP1WMeg0FNymbBulr6Nw.lBNwSGJBYkbV8P0Gi4agY0AZL4zps2b2C3jlE63S4yU&dib_tag=se&keywords=220%2Bohm%2Bresistor&qid=1751558407&s=industrial&sprefix=220%2Bohm%2Bresisto%2Cindustrial%2C128&sr=1-3&th=1"> Link </a> |
| **Assorted Single-Core Wires** | **Connections for Components** | **$15** | <a href = "https://www.amazon.com/Electrical-7colors-spools-UL1007-breadboard/dp/B083DN5R61/ref=asc_df_B083DN5R61/?tag=hyprod-20&linkCode=df0&hvadid=692875362841&hvpos=&hvnetw=g&hvrand=8530834579962313816&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9032183&hvtargid=pla-2281435179978&psc=1&mcid=8b897963727d312e9a95e09793193a56&hvocijid=8530834579962313816-B083DN5R61-&hvexpln=73&gad_source=1"> Link </a> | 
| **PCB Board** | **Holds all Parts** | **$10** | <a href = "https://www.amazon.com/ELEGOO-Prototype-Soldering-Compatible-Arduino/dp/B072Z7Y19F/ref=sr_1_fkmr0_1?crid=18FRQ5Z77CLN3&dib=eyJ2IjoiMSJ9.cFO3IbuqDHBg13mO-bkEuDZt4D5ArS6wMFfqDWRiL40.8EixwzeL0N95GaD5v3ouxOydzFTpfyCVcRnI53u4MqE&dib_tag=se&keywords=proto+board+10xX&qid=1720637134&sprefix=proto+board+10xx%2Caps%2C126&sr=8-1-fkmr0"> Link </a> |
| **LED Strip** | **Displays Colors and serves as an Alternative 'Buzzer' | **$9** | <a href = "https://www.amazon.com/BTF-LIGHTING-WS2812B1M60LB30-BTF-LIGHTING-WS2812B-IC-RGB-5050SMD-Pure-Gold-Individual-Addressable-LED-Strip-High-Quality-3-28FT-60LED-60LED-m-Flexible-Full-Color-IP30-DC5V-for-DIY-Chasing-Color-Project-No-Adapter-or-Controller/dp/B01CDTED80/ref=asc_df_B01CDTED80?mcid=aab6f3a36a97389abee1397380f9f389&hvocijid=16232621854761171541-B01CDTED80-&hvexpln=73&tag=hyprod-20&linkCode=df0&hvadid=721245378154&hvpos=&hvnetw=g&hvrand=16232621854761171541&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9032171&hvtargid=pla-2281435178298&th=1"> Link </a> |


# Starter Project

<iframe width="743" height="418" src="https://www.youtube.com/embed/LLyRvk59FLk" title="Caden Y. Starter Project" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## Description
For my BlueStamp starter project, I chose to build RGB sliders. RGB sliders allow you to mix the colors red, green, and blue to create virtually any color within the RGB spectrum. For example, if I want to create a shade of purple, I can increase the saturation levels of red and blue while lowering the green. I chose this project because I thought it would be really interesting to create a device that visually demonstrates how different colors are formed from just three primary components. Additionally, I saw this as a great opportunity to improve my soldering skills and get comfortable with assembling circuits. Practicing on this project will help me avoid making major mistakes when I move on to my more intensive main project. 

## Challenges
I encountered several challenges while building the RGB sliders, even though the project was relatively simple compared to other starter options. One issue I faced was ensuring the correct polarity of the LED lights. Typically, the longer leg of an LED indicates the positive side, but in this case, it corresponded to the negative. I had to be very careful not to get it wrong, since a mistake would require me to de-solder and reattach the LED entirely. Another obstacle was accidentally melting the plastic while soldering. Since it was my first time using a soldering iron, I had trouble applying it efficiently, which led to the plastic being exposed to high temperatures for too long. This weakened the structure of the project slightly, but thankfully it didn’t cause any major functional problems.

## Next Steps 
After finishing my starter project, I intend on refining my Arduino skills to ensure that building my intensive project will be easier. I also hope to finish my first milestone by the next few days. 

# References
Flex Sensor: [https://www.instructables.com/How-to-Make-FLEX-Sensor-at-Home-DIY-Flex-Sensor/](https://content.instructables.com/FBK/WEOU/KKQ0ZIXS/FBKWEOUKKQ0ZIXS.png?auto=webp&frame=1&width=1024&fit=bounds&md=MjAyMS0wMi0wNCAwMTozNzo1NS4w&_gl=1*8o72m2*_ga*MjQwNDI0NzY1LjE3NTAxODY2MTA.*_ga_NZSJ72N6RX*czE3NTE1NTczOTUkbzUkZzEkdDE3NTE1NTc0ODkkajYwJGwwJGgw)

Accelerometer Schematic: https://www.mdpi.com/applsci/applsci-12-03994/article_deploy/html/images/applsci-12-03994-g001.png


# Appendix
## Milestone 1 Code
```cpp
#include <Adafruit_LSM6DS33.h>
#include <BleSerial.h>
#include <Wire.h>

Adafruit_LSM6DS33 lsm6ds33 {};
BleSerial ble;

void setup(void) {
  Serial.begin(115200);
  ble.begin("Values");
  while (!Serial)
    delay(10); 

  Serial.println("Adafruit LSM6DS33 test!");

  if (lsm6ds33.begin_I2C()) {
    Serial.println("Failed to find LSM6DS33 chip");
    while (1) {
      delay(10);
    }
  }

  Serial.println("LSM6DS33 Found!");

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
}
```

## Milestone 2 Code
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
} 
```

## Milestone 3 Code
```cpp
// Include necessary libraries
#include <Adafruit_LSM6DS33.h>        // For interfacing with LSM6DS33 IMU
#include <BleSerial.h>                // For Bluetooth serial communication
#include <Adafruit_Sensor.h>          // Common sensor interface library
#include <Wire.h>                     // I2C communication
#include <MadgwickAHRS.h>             // Sensor fusion algorithm
#include <math.h>                     // Math operations like fabs

// Utility function to compare floats within a tolerance
bool approxEqual(float a, float b, float tol = 0.5) {
  return fabs(a - b) < tol;
}

// Create instances for IMU, Bluetooth, and Madgwick filter
Adafruit_LSM6DS33 lsm6ds33 {};     // LSM6DS33 sensor object
BleSerial ble;                     // BLE Serial communication object
Madgwick filter;                   // Sensor fusion filter

// Define hardware pin connections
const int FlexPin = 35;            // Analog pin for flex sensor
const int Buzzer = 23;             // Digital pin for buzzer output

// Variables for sensor readings and timing
int FlexValue = 0;
unsigned long lastUpdate = 0;      // Stores last update timestamp
unsigned long timeStep = 0;        // Incremental step counter for output

void setup(void) {
  // Start serial communication
  Serial.begin(115200);

  // Initialize BLE serial with device name
  ble.begin("Values");

  // Set pin modes
  pinMode(FlexPin, INPUT);
  pinMode(Buzzer, OUTPUT);

  // Wait for Serial monitor to be available
  while (!Serial)
    delay(10);

  Serial.println("Adafruit LSM6DS33 test!");

  // Begin I2C communication with custom SDA/SCL pins
  Wire.begin(21, 22);

  // Scan for I2C devices on the bus
  for (int i = 0; i <= 127; i++) {
    Wire.beginTransmission(i);
    if (!Wire.endTransmission()) {
      Serial.print("device found: ");
      Serial.println(i);
    }
  }

  // Initialize the LSM6DS33 sensor
  if (!lsm6ds33.begin_I2C()) {
    Serial.println("Failed to find LSM6DS33 chip");
    while (1) delay(10);  // Halt program if initialization fails
  }

  Serial.println("LSM6DS33 Found!");

  // Set accelerometer range to ±16G
  Serial.print("Accelerometer range set to: ");
  lsm6ds33.setAccelRange(LSM6DS_ACCEL_RANGE_16_G);
  switch (lsm6ds33.getAccelRange()) {
    case LSM6DS_ACCEL_RANGE_2_G: Serial.println("+-2G"); break;
    case LSM6DS_ACCEL_RANGE_4_G: Serial.println("+-4G"); break;
    case LSM6DS_ACCEL_RANGE_8_G: Serial.println("+-8G"); break;
    case LSM6DS_ACCEL_RANGE_16_G: Serial.println("+-16G"); break;
  }

  // Set gyroscope range to ±2000 degrees/s
  Serial.print("Gyro range set to: ");
  lsm6ds33.setGyroRange(LSM6DS_GYRO_RANGE_2000_DPS);
  switch (lsm6ds33.getGyroRange()) {
    case LSM6DS_GYRO_RANGE_125_DPS: Serial.println("125 degrees/s"); break;
    case LSM6DS_GYRO_RANGE_250_DPS: Serial.println("250 degrees/s"); break;
    case LSM6DS_GYRO_RANGE_500_DPS: Serial.println("500 degrees/s"); break;
    case LSM6DS_GYRO_RANGE_1000_DPS: Serial.println("1000 degrees/s"); break;
    case LSM6DS_GYRO_RANGE_2000_DPS: Serial.println("2000 degrees/s"); break;
    case ISM330DHCX_GYRO_RANGE_4000_DPS: break; // Not supported on DS33
  }

  // Set accelerometer data rate to 52 Hz
  Serial.print("Accelerometer data rate set to: ");
  lsm6ds33.setAccelDataRate(LSM6DS_RATE_52_HZ);
  switch (lsm6ds33.getAccelDataRate()) {
    case LSM6DS_RATE_SHUTDOWN: Serial.println("0 Hz"); break;
    case LSM6DS_RATE_12_5_HZ: Serial.println("12.5 Hz"); break;
    case LSM6DS_RATE_26_HZ: Serial.println("26 Hz"); break;
    case LSM6DS_RATE_52_HZ: Serial.println("52 Hz"); break;
    case LSM6DS_RATE_104_HZ: Serial.println("104 Hz"); break;
    case LSM6DS_RATE_208_HZ: Serial.println("208 Hz"); break;
    case LSM6DS_RATE_416_HZ: Serial.println("416 Hz"); break;
    case LSM6DS_RATE_833_HZ: Serial.println("833 Hz"); break;
    case LSM6DS_RATE_1_66K_HZ: Serial.println("1.66 KHz"); break;
    case LSM6DS_RATE_3_33K_HZ: Serial.println("3.33 KHz"); break;
    case LSM6DS_RATE_6_66K_HZ: Serial.println("6.66 KHz"); break;
  }

  // Set gyroscope data rate to 6.66 KHz
  Serial.print("Gyro data rate set to: ");
  lsm6ds33.setGyroDataRate(LSM6DS_RATE_6_66K_HZ);
  switch (lsm6ds33.getGyroDataRate()) {
    case LSM6DS_RATE_SHUTDOWN: Serial.println("0 Hz"); break;
    case LSM6DS_RATE_12_5_HZ: Serial.println("12.5 Hz"); break;
    case LSM6DS_RATE_26_HZ: Serial.println("26 Hz"); break;
    case LSM6DS_RATE_52_HZ: Serial.println("52 Hz"); break;
    case LSM6DS_RATE_104_HZ: Serial.println("104 Hz"); break;
    case LSM6DS_RATE_208_HZ: Serial.println("208 Hz"); break;
    case LSM6DS_RATE_416_HZ: Serial.println("416 Hz"); break;
    case LSM6DS_RATE_833_HZ: Serial.println("833 Hz"); break;
    case LSM6DS_RATE_1_66K_HZ: Serial.println("1.66 KHz"); break;
    case LSM6DS_RATE_3_33K_HZ: Serial.println("3.33 KHz"); break;
    case LSM6DS_RATE_6_66K_HZ: Serial.println("6.66 KHz"); break;
  }

  // Enable data-ready interrupts
  lsm6ds33.configInt1(false, false, true); // Accelerometer DRDY on INT1
  lsm6ds33.configInt2(false, true, false); // Gyroscope DRDY on INT2

  // Initialize Madgwick filter (sensor fusion) at 10 Hz
  filter.begin(10);
}

void loop() {
  // Time delta in seconds for sensor fusion
  unsigned long currentMicros = micros();
  float deltaTime = (currentMicros - lastUpdate) / 1000000.0f;
  lastUpdate = currentMicros;

  // Read flex sensor value
  FlexValue = analogRead(FlexPin);

  // Variables for storing sensor events
  sensors_event_t accel;
  sensors_event_t gyro;
  sensors_event_t temp;

  // Get the latest sensor readings
  lsm6ds33.getEvent(&accel, &gyro, &temp);

  // Extract raw gyro values
  float gx = gyro.gyro.x;
  float gy = gyro.gyro.y;
  float gz = gyro.gyro.z;

  // Update the Madgwick filter with gyro and accel values
  filter.updateIMU(gx, gy, gz,
                   accel.acceleration.x,
                   accel.acceleration.y,
                   accel.acceleration.z);

  // Retrieve orientation values
  float roll = filter.getRoll();     // In degrees
  float pitch = filter.getPitch();   // In degrees
  float yaw = filter.getYaw();       // In degrees

  // Send orientation over Bluetooth
  ble.print(roll); ble.print(", ");
  ble.print(pitch); ble.print(", ");
  ble.print(yaw); ble.println();

  // Print values to Serial Monitor
  Serial.print(roll); Serial.print(", ");
  Serial.print(pitch); Serial.print(", ");
  Serial.print(yaw); Serial.print(", ");
  Serial.println(timeStep);
  Serial.println();

  // Step counter
  timeStep++;

  // -------- Buzzer Alert Logic --------
  // Sound the buzzer if:
  // - Roll is NOT between -75 and -60 degrees, OR
  // - Yaw is within forward-facing warning range (0–30 OR 330–360)
  bool rollInRange = (roll >= -75 && roll <= -60);
  bool yawInBeepRange = (yaw >= 0 && yaw <= 30) || (
```

## Modifications Code
```cpp
// --- Library Includes ---
#include <Adafruit_LSM6DS33.h>        // IMU sensor (accelerometer + gyroscope)
#include <BleSerial.h>                // Bluetooth communication via serial
#include <Adafruit_Sensor.h>          // Base class for sensors
#include <Wire.h>                     // I2C communication
#include <MadgwickAHRS.h>             // Sensor fusion algorithm for orientation
#include <math.h>                     // Math functions
#include <Adafruit_NeoPixel.h>        // LED strip control

// --- LED Strip Configuration ---
#define LED_PIN        12             // Pin for NeoPixel data line
#define NUM_PIXELS     18             // Number of pixels in the LED strip
Adafruit_NeoPixel strip(NUM_PIXELS, LED_PIN, NEO_GRB + NEO_KHZ800);

// --- Utility Function: Floating Point Comparison ---
bool approxEqual(float a, float b, float tol=0.5) {
  return fabs(a - b) < tol;           // Returns true if values are within tolerance
}

// --- Sensor & Communication Objects ---
Adafruit_LSM6DS33 lsm6ds33 {};       // LSM6DS33 IMU instance
BleSerial ble;                        // Bluetooth Serial instance
Madgwick filter;                      // Sensor fusion filter

// --- Pin Definitions ---
const int FlexPin = 35;               // Analog pin for flex sensor
const int Buzzer = 23;                // Digital output for buzzer

// --- State Variables ---
int FlexValue = 0;                    // Latest value from flex sensor
unsigned long lastUpdate = 0;        // Last timestamp for IMU update
unsigned long timeStep = 0;          // Loop iteration counter
unsigned long lastGreenUpdate = 0;   // Time since last green LED update
int greenPixelCount = NUM_PIXELS;    // Counter for progressive green LED effect

// --- LED Control Functions ---

// Set all LEDs to the same RGB color (inefficient hard-coded version)
void setLEDColor(uint8_t r, uint8_t g, uint8_t b) {
  for (int i = 0; i < NUM_PIXELS; i++) {
    strip.setPixelColor(i, strip.Color(r, g, b));
  }
  strip.show();
}

// Efficiently sets all pixels to the specified RGB color
void setAllPixelsColor(uint8_t r, uint8_t g, uint8_t b) {
  for (int i = 0; i < NUM_PIXELS; i++) {
    strip.setPixelColor(i, strip.Color(r, g, b));
  }
  strip.show();
}

// Light up LEDs one-by-one in green, simulating a progressive effect
void setGreenProgressively() {
  unsigned long now = millis();
  if (now - lastGreenUpdate >= 50 && greenPixelCount < NUM_PIXELS) {
    strip.setPixelColor(greenPixelCount, strip.Color(0, 255, 0));
    strip.show();
    greenPixelCount++;
    lastGreenUpdate = now;
  }
}

// Reset all LEDs to off and restart green animation
void resetGreenPixels() {
  greenPixelCount = 0;
  for (int i = 0; i < NUM_PIXELS; i++) {
    strip.setPixelColor(i, 0); // turn off
  }
  strip.show();
}

// --- Setup Function ---
void setup(void) {
  Serial.begin(115200);
  ble.begin("Values");                // Start BLE with name "Values"
  pinMode(FlexPin, INPUT);
  pinMode(Buzzer, OUTPUT);

  strip.begin();
  strip.setBrightness(50);           // Set LED brightness (0–255)
  setLEDColor(0, 255, 0);            // Start with green LEDs

  // Wait for serial connection (useful on boards like Leonardo)
  while (!Serial)
    delay(10);                       

  Serial.println("Adafruit LSM6DS33 test!");

  // Initialize I2C with custom SDA/SCL pins (e.g., on ESP32)
  Wire.begin(21, 22);

  // Scan I2C bus for connected devices
  for(int i = 0; i <= 127; i ++) {
    Wire.beginTransmission(i);
    if(!Wire.endTransmission()){
      Serial.print("Device found at address: ");
      Serial.println(i);
    }
  }

  // Initialize IMU sensor over I2C
  if (!lsm6ds33.begin_I2C()) {
    Serial.println("Failed to find LSM6DS33 chip");
    while (1) delay(10);
  }
  Serial.println("LSM6DS33 Found!");

  // Configure accelerometer range
  lsm6ds33.setAccelRange(LSM6DS_ACCEL_RANGE_16_G);
  Serial.print("Accelerometer range set to: ");
  switch (lsm6ds33.getAccelRange()) {
    case LSM6DS_ACCEL_RANGE_2_G: Serial.println("±2G"); break;
    case LSM6DS_ACCEL_RANGE_4_G: Serial.println("±4G"); break;
    case LSM6DS_ACCEL_RANGE_8_G: Serial.println("±8G"); break;
    case LSM6DS_ACCEL_RANGE_16_G: Serial.println("±16G"); break;
  }

  // Configure gyroscope range
  lsm6ds33.setGyroRange(LSM6DS_GYRO_RANGE_2000_DPS);
  Serial.print("Gyro range set to: ");
  switch (lsm6ds33.getGyroRange()) {
    case LSM6DS_GYRO_RANGE_125_DPS: Serial.println("125 dps"); break;
    case LSM6DS_GYRO_RANGE_250_DPS: Serial.println("250 dps"); break;
    case LSM6DS_GYRO_RANGE_500_DPS: Serial.println("500 dps"); break;
    case LSM6DS_GYRO_RANGE_1000_DPS: Serial.println("1000 dps"); break;
    case LSM6DS_GYRO_RANGE_2000_DPS: Serial.println("2000 dps"); break;
  }

  // Configure accelerometer data rate
  lsm6ds33.setAccelDataRate(LSM6DS_RATE_52_HZ);
  Serial.print("Accelerometer data rate set to: ");
  // Print readable data rate
  switch (lsm6ds33.getAccelDataRate()) {
    case LSM6DS_RATE_52_HZ: Serial.println("52 Hz"); break;
    // Add other cases if needed
  }

  // Configure gyroscope data rate
  lsm6ds33.setGyroDataRate(LSM6DS_RATE_6_66K_HZ);
  Serial.print("Gyro data rate set to: ");
  switch (lsm6ds33.getGyroDataRate()) {
    case LSM6DS_RATE_6_66K_HZ: Serial.println("6.66 KHz"); break;
    // Add other cases if needed
  }

  // Enable interrupt data ready lines
  lsm6ds33.configInt1(false, false, true); // Accelerometer DRDY
  lsm6ds33.configInt2(false, true, false); // Gyroscope DRDY

  // Initialize Madgwick filter with update frequency (Hz)
  filter.begin(10); 
}

// --- Main Loop ---
void loop() {
  // Calculate time difference since last IMU update
  unsigned long currentMicros = micros();
  float deltaTime = (currentMicros - lastUpdate) / 1000000.0f;
  lastUpdate = currentMicros;

  // Read flex sensor
  FlexValue = analogRead(FlexPin);
  Serial.print(FlexValue);
  Serial.print(", ");

  // Read IMU sensor data
  sensors_event_t accel, gyro, temp;
  lsm6ds33.getEvent(&accel, &gyro, &temp);

  // Get raw gyro values
  float gx = gyro.gyro.x;
  float gy = gyro.gyro.y;
  float gz = gyro.gyro.z;

  // Sensor fusion update
  filter.updateIMU(gx, gy, gz,
                   accel.acceleration.x,
                   accel.acceleration.y,
                   accel.acceleration.z);

  // Get orientation angles
  float roll = filter.getRoll();
  float pitch = filter.getPitch();
  float yaw = filter.getYaw();

  // Send orientation via Bluetooth
  ble.print(roll); ble.print(", ");
  ble.print(pitch); ble.print(", ");
  ble.print(yaw); ble.println();

  // Print debug info to serial
  Serial.print(roll); Serial.print(", ");
  Serial.print(pitch); Serial.print(", ");
  Serial.print(yaw); Serial.print(", ");
  Serial.println(timeStep); Serial.println();
  timeStep++;

  // --- Buzzer + LED Feedback Logic ---
  bool shouldBuzz = false;

  if (FlexValue >= 1800 && FlexValue <= 2100) {
    // Mid flex: yellow LED, no buzzer
    shouldBuzz = false;
    setAllPixelsColor(255, 255, 0); // Yellow
    resetGreenPixels();
  } 
  else if (FlexValue > 3100) {
    // High flex value
    if (roll < -95 || pitch < -20) {
      shouldBuzz = true;
      setAllPixelsColor(255, 0, 0); // Red
      resetGreenPixels();
    } else if (roll > -95 && roll < -75 && pitch > -20) {
      // Valid range: progressive green LEDs
      shouldBuzz = false;
      setGreenProgressively();
    }
  }

  // Activate or deactivate buzzer
  digitalWrite(Buzzer, shouldBuzz ? HIGH : LOW);
}

```
