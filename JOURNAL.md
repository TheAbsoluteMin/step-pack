---
title: "StepPack"
author: "TheAbsoluteMin"
description: "A smart, wireless enabling backpack for stepper motors."
created_at: "2026-08-12"
---

# Log 1: August 12, 2026 - Initial Schematics - 2.1 hours
Timelapse <a href="https://lapse.hackclub.com/timelapse/6FzYQxMGaGmf">link</a>.

I had recently worked with stepper motors for a conveyor belt I had built, and I was astonished at the incredible number of wires needed solely to run a single NEMA 17 stepper motor! Each stepper motor needs about 4 wires and many more for each driver! Using multiple can quickly become a mess, especially in robotics applications. Thus, I wondered if there was a way to reduce all that clutter, and as my eyes were looking at an ESP32 sitting on a shelf in front of me, I came up with an idea. 

With the fast, wireless data transfers of the ESP32's ESP-NOW technology, I could send movement signals to each connected stepper motor with their own driver PCB, drastically reducing the overall wire count between each stepper motor to only 2 wires. Even better, you could add more and more stepper motors, and still only use 2 wires, power and ground, to connect them all! I hope as this project progresses, I can create a comprehensive "backpack" with more essential features that can make using stepper motors easier and smarter!

As I began my research, I began compiling certain components for the PCB backpack, and I had to choose wisely as I had to fit everything in a small 42mm by 42mm back. I began with the ESP32-S3 MINI 1, and I hope to integrate the TMC2209 driver and the AS5600 magnetic encoder later for a true smart, closed looped design. 

<img width="1913" height="855" alt="image" src="https://github.com/user-attachments/assets/145e7831-e5f3-4466-a9bf-d123a9a33806" />

Right now, my schematic is quite a mess as I am still optimizing my parts for my project.

<img width="1207" height="827" alt="image" src="https://github.com/user-attachments/assets/fc97b1e2-733c-4f57-9f89-7fd468c7d9c7" />

However, with the help of the Espressif Systems datasheet, I was able to begin wiring the ESP32-S3 MINI 1!
<img width="899" height="852" alt="image" src="https://github.com/user-attachments/assets/beedb7fb-2f7c-44df-9af9-d85fcfe833e1" />

**Total time spent: 2.1 hours**

---

# Log 2: August 13, 2026 - Power Design Schematics - 2.2 hours
Timelapse <a href="https://lapse.hackclub.com/timelapse/Z9I2UxFSzDmm">link</a>.

Today, I began working on the power management system. Starting with the USB-C receptacle, I wired it with the USBLC6-2SC6 ESD protection chip. Initially, I wanted to avoid doing so because of a past difficulty of maintaining equal lengths of data lines in a past project. However, I realized a way to avoid my past challenge as it turns out that pins 1 and 6 are practically identical to pins 3 and 4, meaning I could wire either D+ or D- into them! I had thought D+ was only supposed to go in pins 1 and 6 before, which complicated wiring!

<img width="736" height="478" alt="image" src="https://github.com/user-attachments/assets/ee238bbc-186c-4ccd-8103-226b1202bb42" />

When I got to the VBUS 5V line of the USB-C, I realized that I would need to somehow power the ESP32-S3 MINI 1 when I flash the code. The problem is that I initially planned to step down 24V to power the MCU during normal operation. This meant I had to include the AP2112K-3.3 to step down the voltage for the MCU. 

<img width="979" height="763" alt="image" src="https://github.com/user-attachments/assets/01d45459-91ae-4e51-ae07-d6257165aef2" />

In order to safely handle both the USB-C 5V power and buck converter's stepped down power of 24V to 5V, I implemented the BAT54C in order to connect the two power sources, which would then be stepped down to a clean 3.3V. With this, I also can safely use one power source or even both at the same time!

<img width="1711" height="894" alt="image" src="https://github.com/user-attachments/assets/738a773b-80a5-4253-8c15-f368b413b8dd" />

Unlike the AP2112K-3.3, the LMR16006YQ5 buck regulator was much more complicated to wire.

<img width="1923" height="573" alt="image" src="https://github.com/user-attachments/assets/e2b318de-5f92-425a-8736-d806e8c69769" />

**Total time spent: 2.2 hours**

---

# Log 3: August 14, 2026 - Schematics Continued - 1.6 hours
Timelapse <a href="https://lapse.hackclub.com/timelapse/vkxOGXVv4BmJ">link</a>.

After realizing that the ESP32-S3 MINI 1 could draw up to 500mA, I had to change the BAT54C as it could only handle up to 200mA. Thus, I chose the PMEG2010EA diodes, and I made my own diode OR gate in order to keep the same capability to handle both the USB-C and buck regulator power sources.

<img width="990" height="741" alt="image" src="https://github.com/user-attachments/assets/1216366f-378a-45b0-b3d0-a037f0c1e889" />

Then, I started wiring the TMC2209 stepper motor driver. Wow, it was quite some work to get all the parts wired, especially the capacitors. Fortunately, I was able to reference the official schematics of the SilentStepStick module.

<img width="1836" height="1188" alt="image" src="https://github.com/user-attachments/assets/2eb3d742-b097-4521-aecc-9bc1af18c92e" />

<img width="2424" height="1267" alt="image" src="https://github.com/user-attachments/assets/fa014679-36a7-45a4-aa20-6576ca1e4ac5" />

**Total time spent: 1.6 hours**

---

# Log 4: August 15, 2026 - Tiny Edits Schematics - 0.3 hours
Timelapse <a href="https://lapse.hackclub.com/timelapse/_rkijpWBezsx">link</a>.

Today, I did not have much time to work on my project, so I made some tiny edits to the TMC2209 module. After recreating the schematic from the official reference, I had to adapt it.

Specifically, I had to make sure that the ESP32-S3 MINI 1 could safely interact with the stepper motor driver on 3.3V logic.

<img width="876" height="485" alt="image" src="https://github.com/user-attachments/assets/828d0fbb-bf38-4053-a2b3-5afe4a676bf1" />
<img width="2241" height="1029" alt="image" src="https://github.com/user-attachments/assets/1000c9b2-43e6-4d40-915f-12964c9ce927" />

It was strange that the official schematics wired the bigger capacitors a bit isolated from the others on the VM line, so I changed it to be a little more intuitive.

<img width="1156" height="356" alt="image" src="https://github.com/user-attachments/assets/01ede0f0-876f-424a-a3b3-2bf12cc14f23" />
<img width="1691" height="500" alt="image" src="https://github.com/user-attachments/assets/145845e6-d5d3-4d5c-b5a4-fe0f8ef8101a" />

**Total time spent: 0.3 hours**

---

# Log 5: August 16, 2026 - Schematics Completion - 3.1 hours
Timelapse <a href="https://lapse.hackclub.com/timelapse/vb9HLf_P8bR-">link</a>.

Today was a big day! I began by continuing to optimize the TMC2209 module. Since I chose the Bourns potentiometer, turning the potentiometer's screw counterclockwise would increase the reference voltage. 

<img width="893" height="372" alt="image" src="https://github.com/user-attachments/assets/42cf1e9e-a785-4a53-b866-47d71c8ca174" />

However, since this is a custom board and not another stepper motor driver for a printer, I could make it more intuitive by readjusting the pins to allow clockwise motion to increase the reference voltage instead.

<img width="410" height="172" alt="image" src="https://github.com/user-attachments/assets/21a85202-4802-4c69-b2d2-69d8a962f905" />
<img width="690" height="398" alt="image" src="https://github.com/user-attachments/assets/d37abecd-569f-4891-ac9c-ca3c2ac53a94" />

Then, as I was enabling UART between the MCU and stepper motor driver, I realized that I did not need that external potentiometer to control current! I could have it all done in software, so I deleted it and left VREF floating.

<img width="369" height="277" alt="image" src="https://github.com/user-attachments/assets/554716d0-8c58-4134-931b-261caf3727d9" />

I also moved the LED down the power line after the diode OR gate, so that I could also have a physical status LED during normal operation instead of solely when I flash code via USB-C. 

<img width="1552" height="1136" alt="image" src="https://github.com/user-attachments/assets/d6279a3c-c7cb-4305-b7a1-2770703de21e" />

In order to protect against back EMF generated by the stepper motor, I added a TVS diode and a 470uF capacitor.

<img width="1536" height="390" alt="image" src="https://github.com/user-attachments/assets/a9db7196-c6dd-40cf-992b-aeb95f1b789d" />

For easy configuration when using multiple StepPack modules together with multiple stepper motors, I included a dip switch so that each stepper motor could be quickly assigned a hardware address that would be handled in the firmware.

<img width="802" height="620" alt="image" src="https://github.com/user-attachments/assets/38dc807a-a894-46d6-a723-d6a5b63c9819" />

To make my project versatile, I included an I2C port so that sensors could be added to the PCB.

<img width="915" height="520" alt="image" src="https://github.com/user-attachments/assets/88a8a8a8-bd36-4473-816c-9c17250d35cf" />

Finally, I wired the AS5600 encoder.

<img width="914" height="343" alt="image" src="https://github.com/user-attachments/assets/ed10ee21-7c9f-49df-9eec-40c21f3b3774" />

With that, the schematics is finished for now!

**Total time spent: 3.1 hours**

---
