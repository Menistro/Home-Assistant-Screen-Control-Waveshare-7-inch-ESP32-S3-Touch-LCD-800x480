# Home-Assistant-Screen-Control-Waveshare-7-inch-ESP32-S3-Touch-LCD-800x480
Custom ESPHome firmware to transform a Waveshare 7-inch ESP32-S3 touch panel into a Home Assistant dashboard. It features a dark-mode LVGL UI controlling four lighting zones via synced sliders. Advanced logic includes zero-latency screen dimming, auto-sleep power management, and network debouncing for flawless two-way synchronization.

# Waveshare 7" ESP32-S3 Home Assistant Dashboard (ESPHome + LVGL)

A highly optimized, dark-mode smart home dashboard for the **Waveshare 7-inch ESP32-S3 Touch LCD (800x480)**. Built completely in ESPHome using the LVGL graphics engine, this configuration provides a premium, lag-free interface to control Home Assistant entities.

![Dashboard Preview](assets/Waveshare-screen-on.jpg)

## ⚠️ Disclaimer regarding Support and Issues
**Please note:** This entire configuration was created with the assistance of **Gemini 3.1 Pro**, as I do not have extensive personal knowledge or background in ESPHome C++ coding. 

Because of this, **I will not be actively monitoring, troubleshooting, or resolving issues/tickets** opened on this repository. This code is provided completely "as-is" in the hopes that it helps others who are stuck trying to get these beautiful panels working. You are highly encouraged to fork this repository and modify it to fit your exact needs!

---

## ✨ Key Features

This isn't just a visual layout; it includes advanced C++ and YAML logic to solve the most common issues with DIY smart displays:

* **Zero-Latency Screen Dimming:** The master screen brightness slider bypasses Home Assistant entirely, communicating directly with the ESP32's hardware PWM for buttery-smooth, iPad-like dimming.
* **Smart Power Management (Auto-Sleep):** After 1 minute of inactivity, the screen dims to 15%. After 5 minutes, it completely shuts off the backlight and temporarily freezes the LVGL touch engine to save CPU and prevent "ghost touches."
* **Network Debouncing:** Dragging sliders normally floods the ESP32 with Wi-Fi requests, causing crashes. This config includes a custom 250ms debouncer that waits for your finger to stop moving before sending a single, clean API call to Home Assistant.
* **Infinite Echo Protection ("Sync Lock"):** A custom global lock prevents the screen from bouncing commands back and forth with Home Assistant, ensuring perfect two-way synchronization without flickering or ghosting.
* **Premium UI Aesthetics:** Features a pitch-black dark mode, perfectly symmetrical cards, and Color Temperature sliders with dynamic Amber-to-Blue horizontal gradients.

## 🛠️ Hardware Requirements

* **Board:** [Waveshare ESP32-S3-Touch-LCD-7](https://www.waveshare.com/esp32-s3-touch-lcd-7.htm) (800x480 resolution)
* **Power:** A high-quality USB-C power supply (the screen and ESP32-S3 draw significant current when at 100% brightness).

## 🚀 Installation & Setup

1. **Copy the YAML:** Copy the contents of `waveshare-panel.yaml` into a new ESPHome node.
2. **Update Secrets:** Ensure your Wi-Fi credentials are set correctly (`!secret wifi_ssid`, etc.).
3. **Map Your Entities:** Do a standard `CTRL+F` (Find and Replace) to swap out my placeholder lights (e.g., `light.led_strip_kitchen_sink`) with your actual Home Assistant entity IDs.
4. **Compile & Upload:** The first compile will take a few minutes as ESPHome downloads the LVGL library and fetches the Material Design Icons directly from Google's Font API.
5. **Enjoy:** Once flashed, the screen will boot up, turn on the LCD circuit via the I2C expander, and instantly sync with your Home Assistant states!

## 🖌️ Fonts & Icons
This project uses the official Google Roboto font and Material Design Icons. You do not need to download them manually; the ESPHome `font:` block is configured to fetch the exact glyphs via the Google Fonts API during compilation.

## 🤝 Contributing
Even though I won't be actively maintaining issues, the community is welcome to submit pull requests if you find a way to optimize the LVGL code, add new widget styles, or build upon this foundation!
