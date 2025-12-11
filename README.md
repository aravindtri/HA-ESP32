# HA-ESP32 Display & Bluetooth Proxy Project

This project configures ESP32 devices to act as **Bluetooth Proxies** for Home Assistant while displaying sensor data on **OLED screens**.

There are two main configurations depending on the screen size you are using.

## Configurations

### 1. 0.96" OLED (128x64)
**File:** `oled_128x64.yml`

This configuration is designed for the larger 0.96" screens. It features a carousel that cycles through 5 pages:
1.  **Temperature:** Shows current temp from a Govee sensor with a trend indicator (Rising/Falling/Stable).
2.  **Humidity:** Shows current humidity.
3.  **Weather:** Displays current condition (Sunny, Cloudy, etc.) and outside temperature.
4.  **Clock:** Large digital clock with date.
5.  **Status:** System uptime and WiFi signal strength.

**Features:**
*   **Trend Logic:** Calculates temperature trends locally on the ESP32.
*   **Carousel:** Automatically switches pages every 5 seconds.
*   **Bluetooth Proxy:** Active scanning for HA.

### 2. 0.91" OLED (128x32)
**File:** `oled_128x32.yml`

This configuration is optimized for the slim 0.91" screens.
*   **Simplified Layout:** Fits essential data into the 32-pixel height.
*   **Visual Indicators:** Uses arrows (↑/↓) for trends instead of text to save space.
*   **Bluetooth Proxy:** Active scanning for HA.

## Hardware Required
*   **ESP32 Board:** ESP32 DevKit V1 (or similar).
*   **Display:** SSD1306 I2C OLED Display (0.96" or 0.91").
*   **Connection:**
    *   **SDA:** GPIO 21
    *   **SCL:** GPIO 22
    *   **VCC:** 3.3V
    *   **GND:** GND

## How to Flash

1.  **Install ESPHome:** Ensure you have ESPHome installed.
2.  **Connect ESP32:** Plug your ESP32 into the computer via USB.
3.  **Run Command:**
    
    For the 128x64 screen:
    ```bash
    esphome run oled_128x64.yml
    ```

    For the 128x32 screen:
    ```bash
    esphome run oled_128x32.yml
    ```

## Home Assistant Integration
*   The device will be automatically discovered by Home Assistant.
*   It acts as a Bluetooth Proxy, extending the range for your Bluetooth sensors (like Govee).
*   It pulls Weather and Sensor data *from* Home Assistant to display on the screen.

## Customization
*   **WiFi:** Update the `ssid` and `password` in the `wifi` section of the YAML files.
*   **Sensors:** Change the `entity_id` in the `sensor` and `text_sensor` sections to match your specific Home Assistant entities.
