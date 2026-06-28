<p align="center">
  <img src="assets/vorix.png" alt="VORIX Logo" width="400">
</p>

> [!NOTE]
> **VORIX is under active development.**
>
> New features, performance improvements, and bug fixes are added regularly. If you encounter an issue or have an idea for improving VORIX, feel free to open an Issue or submit a Pull Request.

VORIX is an open-source real-time ADS-B radar built for the M5StickC Plus2. It transforms a compact ESP32-powered device into a portable aircraft radar capable of tracking nearby aircraft with smooth animations, live flight information, onboard Wi-Fi setup, and a lightweight web portal.

Unlike traditional hobby projects, VORIX is designed with performance and efficiency in mind. The firmware uses a dual-mode architecture that separates radar tracking from aircraft detail viewing, reducing unnecessary network traffic while keeping the interface responsive on constrained hardware.

## Features

- Live ADS-B aircraft tracking
- Smooth interpolated aircraft movement
- Interactive radar interface
- Real-time aircraft detail pages
- Resource-efficient dual-mode scheduler
- Built-in Wi-Fi provisioning portal
- Lightweight onboard web dashboard
- Configurable latitude, longitude, scan radius, and brightness
- Emergency squawk highlighting
- Flight route lookup for selected aircraft
- Optimized for ESP32 and M5StickC Plus2
- Modern animated onboard UI

## How It Works

VORIX runs the UI on the main Arduino loop while aircraft fetching runs in a background FreeRTOS task. This keeps button input, radar animation, and display rendering responsive even while network requests are active.

In **Radar Mode**, VORIX periodically fetches nearby aircraft from the ADSB.lol API, keeps the aircraft list sorted by distance, and interpolates position and heading between updates for smoother movement on the radar screen. The current firmware uses a 15-second radar scan interval to reduce API pressure and preserve device resources.

When an aircraft is selected, VORIX switches into **Aircraft Detail Mode**. Nearby scanning pauses, and only the selected aircraft is refreshed every 2 seconds. Route data is fetched lazily once for that aircraft, keeping CPU, memory, and network usage lower while still showing current flight information.

## Hardware

- M5StickC Plus2
- Wi-Fi connection

No external SDR or ADS-B receiver is required. Aircraft data is retrieved over Wi-Fi.

## Data Sources

- Live aircraft data: [ADSB.lol](https://adsb.lol/)
- Route lookup data: [ADSBdb](https://www.adsbdb.com/)

## Installation

1. Clone this repository.
2. Open `VORIX.ino` in the Arduino IDE.
3. Select the M5StickC Plus2 board.
4. Install the required libraries:
   - `M5Unified`
   - `ArduinoJson`
5. Compile and upload the firmware.
6. On first boot, connect to the `VORIX-SETUP` Wi-Fi network.
7. Open `192.168.4.1`, enter Wi-Fi and location details, then save.

A precompiled firmware build and ESP Web Tools installer may be provided through future project releases.

## Controls

- `BtnA`: select aircraft or cycle detail pages
- `BtnA hold`: open settings
- `BtnB`: next item
- `BtnB hold`: return to radar
- `BtnPWR`: previous item
- `BtnPWR hold`: exit settings

## Web Portal

VORIX includes an onboard web interface for setup and live configuration.

The setup portal appears automatically when no Wi-Fi credentials are saved. After Wi-Fi is configured, the normal dashboard lets you view device status, update scan location, adjust radius, and change Wi-Fi credentials.

## Project Structure

```text
VORIX.ino          Main sketch entry point
VORIX_impl.cpp     Static definitions and web handler implementation
Core/              Display, storage, networking, boot screens, web UI
Data/              Aircraft model, fetcher, locking, scheduler
UI/                On-device radar, list, detail, and settings screens
```

## Roadmap

- Airport overlays
- Runway visualization
- Expanded flight route visualization
- Weather integration
- Nearby airport detection
- Additional UI improvements
- Performance optimizations
- Release-ready precompiled firmware
- ESP Web Tools installer

## Contributing

VORIX is an open-source project, and contributions from the community are always welcome.

Whether you want to add features, improve the UI, optimize performance, fix bugs, refactor code, improve documentation, or suggest new ideas, feel free to contribute.

If you have an idea or enhancement, open an Issue to discuss it first. When you are ready, fork the repository, make your changes, and submit a Pull Request.

Every contribution, big or small, helps make VORIX better for everyone.

Let's build the ultimate handheld ADS-B radar together.

## Credits

VORIX by **n3tm4t3**.

Live aircraft data is provided by ADSB.lol. Route data is provided by ADSBdb.

## License

This project is licensed under the MIT License.
