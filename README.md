# **STM32 LED & Button Control — HAL Coding Method**

A practical STM32F4 project that demonstrates how to **control an LED with a button press using STM32 HAL libraries** and **bare bones HAL-centric code**.

This repo is about **real embedded interaction**, leveraging the **Hardware Abstraction Layer (HAL)** to make GPIO control intuitive, robust, and ready for industrial-grade development.

---

## 🎯 Project Vision

In embedded engineering, the simplest user interface often tells you *everything* about your system’s health: **LED Feedback + Button Interaction**.

This project demonstrates tried-and-true HAL techniques to:

* Read digital inputs (button presses)
* Write digital outputs (LED on/off)
* Use HAL peripherals with clean, readable code

It’s perfect for developers transitioning from tutorials into real firmware design.

---

## 🧠 What the Code Does

This project uses STM32 HAL libraries to:

✔ Initialize system and peripherals
✔ Configure LEDs and push-button GPIO pins
✔ Read button state via `HAL_GPIO_ReadPin()`
✔ Toggle LED status using `HAL_GPIO_WritePin()` and `HAL_GPIO_TogglePin()`
✔ Use debounced logic to handle push-button inputs reliably

HAL simplifies hardware control by wrapping low-level operations into consistent APIs, making maintenance and collaboration easier. ([DeepBlue][1])

---

## 🗂 Repository Structure

```
STM32-LED-BUTTON-CONTROL-HAL-Coding-Method/
├── Core/
│   ├── Inc/
│   │   └── main.h            # Project headers
│   └── Src/
│       └── main.c            # HAL code for LED + button logic
├── Drivers/
│   └── CMSIS/                # Core support files
├── .cproject                 # IDE config
├── .project                  # IDE config
├── .mxproject                # HAL software package config
├── LED_BUTTON_CTRL_HAL_project.ioc  # Optional CubeMX config
├── STM32F446RETX_FLASH.ld    # Linker script
├── STM32F446RETX_RAM.ld      # Linker script
├── LICENSE.txt               # MIT License
└── README.md
```

The presence of HAL and CubeIDE project metadata makes this repo **IDE-ready** while preserving control over HAL usage. ([GitHub][2])

---

## 🛠 Prerequisites

Before you begin:

1. **STM32CubeIDE** installed (includes HAL libraries and build tools)
2. **ST-LINK debug probe** (integrated on most Nucleo boards)
3. Target board with:

   * One LED connected to a GPIO
   * One push-button wired to a GPIO

STM32 HAL is part of the STM32Cube software ecosystem that standardizes peripheral usage across STM32 families. ([Wikipedia][3])

---

## 🚀 Quick Start

### 1) Clone the Repo

```bash
git clone https://github.com/DanielRajChristeen/STM32-LED-BUTTON-CONTROL-HAL-Coding-Method.git
```

---

### 2) Open with STM32CubeIDE

* `File → Import → Existing Projects`
* Select this directory
* Project will load with HAL support

---

### 3) Build & Flash

* Click **Build**
* Connect your board via ST-LINK
* Click **Debug / Run**

---

### 4) Run the Demo

Press the button:

* **LED turns ON**
  Release the button:
* **LED turns OFF or toggles** (based on implementation)

Inside `main.c`, typical HAL patterns will include:

```c
HAL_GPIO_WritePin(LED_GPIO_Port, LED_Pin, GPIO_PIN_RESET);
if(HAL_GPIO_ReadPin(BUTTON_GPIO_Port, BUTTON_Pin) == GPIO_PIN_SET) {
    HAL_GPIO_TogglePin(LED_GPIO_Port, LED_Pin);
}
```

The HAL functions:

* `HAL_GPIO_ReadPin()` — read digital input (button)
* `HAL_GPIO_WritePin()` — set LED state
* `HAL_GPIO_TogglePin()` — flip LED state

This reduces the need for manual register fiddling while preserving determinism. ([DeepBlue][1])

---

## 📚 Learning Outcomes

By diving into this project you will:

✔ Understand HAL GPIO init & handling
✔ Learn real button debounce patterns
✔ Master HAL API usage in practical scenarios
✔ Scale this base pattern to real user interface logic

This is the foundation for interactive embedded applications.

---

## 💡 Next Steps (Strategic)

To take this project further:

✨ Add **software debouncing**
✨ Implement **interrupt-based button control**
✨ Add a **state machine** for advanced UI logic
✨ Integrate a **timer** for blinking patterns

HAL sets you up for scalable features without rewriting core logic.

---

## 📜 License — MIT

```
MIT License

Copyright (c) 2025 Daniel Raj Christeen

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY.
```

---
