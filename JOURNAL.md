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
