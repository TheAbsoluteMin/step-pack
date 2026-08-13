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
