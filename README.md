# Developer/Builder

## Stuff I'm Building
- **Ephemeral email addresses:** [MinusMail](http://www.minusmail.com/) <br/>
    - Code and architecture found in the [repo](https://github.com/bcwaters/minusmail)  

- **Command-line OPENAI-API Terminal:** [ai_cmd](https://github.com/bcwaters/ai_cmd)
  - I use this every day!  
  - Test the terminal in your browser: [xterm browser access](http://minusmail.com/xterm)
 
- **National Fire Incident Graphs:** [repo](https://github.com/bcwaters/fire_project)  [Website](https://www.wildfiregraphs.com)
   - Parsing a pdf containing National Fire Incident data to generate graphs.  This is a work around due to gated apis which cannot be easily accessed.
 
- **Command-line unixtip:** [unixtip](https://github.com/bcwaters/unixtip)
   - I use this sometimes to get command suggestions for CHATGPT in the terminal and execute them. 

# Custom Tamagotchi Virtual Pet

A handheld, networked virtual pet built around an ESP32, with support for local interaction, WiFi/Bluetooth features, expandable storage, and secure private networking.

## Hardware Components

The device is built on a custom **double-sided PCB** milled on a Genmitsu 3018 Pro CNC router from FR4 copper-clad material.

### Core Components
- **ESP32-S3 Development Board** — Main microcontroller with built-in WiFi and Bluetooth
- **0.96" SSD1306 OLED Display (128x64, I2C)** — Monochrome screen for pet animations, stats, and menus
- **microSD Card Breakout Module (SPI)** — Removable storage for pet saves, images, logs, and uploaded assets
- **Tactile Push Buttons (4–6)** — User input for feeding, playing, navigating menus, and triggering actions
- **Passive Buzzer** — Simple audio feedback for sounds and alerts
- **TP4056 LiPo Charger Module** — Battery charging with basic protection
- **3.7V LiPo Battery (500–1000 mAh)** — Rechargeable power source
- **Custom Double-Sided PCB** — Milled on Genmitsu 3018 Pro; provides all interconnections with ground plane for clean routing
- **Miscellaneous** — Pin headers, decoupling capacitors, wires, and optional power switch

The PCB is designed to be compact (~6–8 cm) for handheld use, with clear antenna clearance for the ESP32.

## Software Architecture

The firmware runs on the ESP32-S3 and is structured around modular, concurrent tasks for responsiveness and low power use.

### High-Level Layers
- **Pet Logic Core** — Manages virtual pet state (hunger, happiness, health, age, mood), animations, and evolution rules. Handles button inputs and updates the OLED display.
- **Storage Layer** — Uses the microSD card for persistent saves, image assets, logs, and uploaded files (e.g., new sprites or pet data).
- **Networking Layer** — 
  - WiFi station mode with mDNS support (allows access via `http://tama-pet.local` on the local network)
  - Bluetooth (Classic and/or BLE) for optional phone pairing or control
  - Local web server for browsing/downloading/uploading files from the SD card
- **Network Scanning & Discovery** — Scans nearby WiFi networks and can map active devices on the local LAN.
- **Remote Connectivity** — Integrates a Tailscale-compatible client (such as MicroLink) to join a self-hosted Headscale tailnet. This provides secure, private access from anywhere using stable Tailscale IPs or MagicDNS names.
- **Bidirectional Communication** — Supports sending scan results or logs to other tailnet devices and receiving remote commands (e.g., to trigger pet actions or animations).

### Key Design Principles
- **Local-first interaction** — Buttons and OLED work independently of networking.
- **Privacy-focused networking** — Tailscale/Headscale keeps remote access secure within your private tailnet. Local mDNS provides simple access on the current WiFi without exposing the device publicly.
- **Modular & extensible** — Storage on microSD allows easy addition of new images or assets. The web server makes files discoverable to authorized tailnet members.
- **Power aware** — Uses deep sleep modes where possible while maintaining connectivity features on demand.

The system combines real-time pet care with modern networked capabilities while keeping the core experience simple and fun.

---

Built as a DIY project using a Genmitsu 3018 Pro for the custom PCB.


