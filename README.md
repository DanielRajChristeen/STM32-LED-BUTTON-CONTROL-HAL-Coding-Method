# **STM32 LED & Button Control — HAL Coding Method**

A beginner-friendly STM32 firmware project that demonstrates **LED blink delay control using two push buttons**, implemented using **STM32 HAL libraries**.

This project teaches how to use HAL APIs to interact with GPIO and manage timing — all with clear, maintainable code.

---

## 🎯 What This Project Does

This firmware implements:

🔹 **LED toggling** on **PA5**
🔹 **Button 1 (PA6)** — increase blink delay by **100 ms**
🔹 **Button 2 (PA7)** — decrease blink delay by **100 ms**
🔹 **Delay clamped** between **0 ms and 1000 ms**
🔹 LED blink speed updates immediately based on button feedback

This behavior models **user-driven timing control**, a common pattern in embedded UI logic.

---

## 🧠 Why HAL Coding?

Using the **STM32 HAL (Hardware Abstraction Layer)** gives you:

✔ Consistent peripheral APIs
✔ Readable, maintainable code
✔ Easier transition to advanced features
✔ Less low-level verbosity compared to raw registers

But you still maintain full control over timing logic and GPIO behavior.

---

## 🗂 Repository Structure

```
STM32-LED-BUTTON-CONTROL-HAL-Coding-Method/
├── Core/
│   ├── Inc/
│   │   └── main.h            # Project headers
│   └── Src/
│       └── main.c            # HAL logic for LED + buttons
├── Drivers/
│   └── CMSIS/                # MCU startup & HAL headers
├── LED_BUTTON_CTRL_HAL.ioc   # Optional CubeMX project
├── .cproject                  # IDE config
├── .project                   # IDE config
├── STM32F446RETX_FLASH.ld     # Linker script
├── STM32F446RETX_RAM.ld       # Linker script
├── LICENSE.txt
└── README.md
```

---

## 🛠 Hardware Setup

| Component | MCU Pin | Label |
| --------- | ------- | ----- |
| LED       | PA5     | D13   |
| Button 1  | PA6     | D12   |
| Button 2  | PA7     | D11   |

❗ Ensure the buttons are wired with proper **pull-up or pull-down resistors**. Internal pull-ups or pull-downs can be configured in code.

---

## 🚀 Getting Started

### 1. Clone the Repo

```bash
git clone https://github.com/DanielRajChristeen/STM32-LED-BUTTON-CONTROL-HAL-Coding-Method.git
```

---

### 2. Open in STM32CubeIDE

* **File → Import → Existing Projects**
* Select the cloned repository
* Allow IDE to index and resolve HAL dependencies

---

### 3. Build & Flash

* Click **Build**
* Connect your STM32 board via **ST-LINK**
* Click **Debug / Run**

The LED will start blinking at the default delay value.

---

## 💡 How the Logic Works

### Delay Control

We start with a default blink delay, e.g.:

```c
uint32_t blinkDelay = 500; // ms
```

Button logic:

```c
if (HAL_GPIO_ReadPin(BUTTON1_GPIO_Port, BUTTON1_Pin) == GPIO_PIN_SET) {
    blinkDelay += 100;
}

if (HAL_GPIO_ReadPin(BUTTON2_GPIO_Port, BUTTON2_Pin) == GPIO_PIN_SET) {
    blinkDelay -= 100;
}
```

### Range Protection

```c
if (blinkDelay > 1000) blinkDelay = 1000;
if (blinkDelay < 0)    blinkDelay = 0;
```

### LED Toggling

```c
HAL_GPIO_TogglePin(LED_GPIO_Port, LED_Pin);
HAL_Delay(blinkDelay);
```

This loop continuously blinks the LED with the current delay value, reflecting real-time control from the buttons.

---

## 📘 Code Snippet — HAL Logic (Conceptual)

Here’s what the core logic might look like in `main.c`:

```c
while (1)
{
    if (HAL_GPIO_ReadPin(GPIOA, GPIO_PIN_6) == GPIO_PIN_SET) {
        blinkDelay += 100;
    }

    if (HAL_GPIO_ReadPin(GPIOA, GPIO_PIN_7) == GPIO_PIN_SET) {
        blinkDelay -= 100;
    }

    if (blinkDelay > 1000) blinkDelay = 1000;
    if (blinkDelay < 0)    blinkDelay = 0;

    HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
    HAL_Delay(blinkDelay);
}
```

This simple loop pumps out continuous toggling with user-controlled speed. HAL functions make it easy to read pins and toggle outputs.

---

## 📚 What You’ll Learn

By working with this project you will:

✔ Use HAL GPIO input/output APIs
✔ Handle user input for dynamic behavior
✔ Control timing with `HAL_Delay()`
✔ Implement range-protected values
✔ Build maintainable, middleware-friendly firmware

---

## 🧩 Common Enhancements

Take this demo to the next level:

* Software debouncing for buttons
* Interrupt-driven button logic instead of polling
* LCD display showing current delay
* Store delay in EEPROM/Flash
* Add state machine for menu navigation

HAL provides the building blocks for professional embedded features.

---

## 📜 License — MIT

```
MIT License

Copyright (c) 2025 Daniel Raj Christeen

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND.
```

---
