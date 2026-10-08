# ⚡ IoT Device Control Panel (NodeMCU & WAMP Server)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Microcontroller](https://img.shields.io/badge/Hardware-ESP8266%20%7C%20NodeMCU-orange.svg)](https://www.espressif.com/)
[![Backend](https://img.shields.io/badge/Server-WAMP%20%7C%20LAMP%20%7C%20PHP-777bb4.svg)](https://www.wampserver.com/)
[![Frontend](https://img.shields.io/badge/Frontend-HTML5%20%7C%20Vanilla%20JS-yellow.svg)](https://github.com/tripathiswastik/mine1)
[![Author](https://img.shields.io/badge/Author-Swastik%20Tripathi-blueviolet.svg)](https://github.com/tripathiswastik)

A responsive Web-based IoT Control Panel designed to trigger and monitor hardware relays and LEDs connected to an **ESP8266 / NodeMCU** microcontroller via a local **WAMP / LAMP** server or cloud REST API gateway.

---

## 🌟 Key Features

- **💡 Dual Relay / LED Control**: Toggle separate channels (e.g. `Device 1 / D1` and `Device 2 / D2`) mapped directly to NodeMCU GPIO pins.
- **🌐 Configurable API Gateway**: Supports switching between a local WAMP server (e.g., `http://192.168.1.100/api/led`) and remote cloud endpoints directly in the UI.
- **✨ Sleek Glassmorphic Dashboard**: Modern dark-mode UI with live glowing bulb visualizers, status badges, and telemetry feed.
- **⚡ Optimistic UI & Zero Heavy Dependencies**: Built using modern Vanilla JavaScript (`fetch` API), removing outdated external jQuery dependencies.
- **🔄 Real-time Polling**: Background state polling synchronizes the dashboard with external hardware switches or remote database changes.

---

## 🏗️ System Architecture

```text
+-----------------------+           HTTP GET / JSON           +-----------------------+
|  Web Dashboard        | ----------------------------------> |  WAMP Server / Cloud  |
|  (index.html)         | <---------------------------------- |  (PHP REST API + DB)  |
+-----------------------+           Status Updates            +-----------------------+
                                                                          ^
                                                                          |
                                                                   Wi-Fi Polling
                                                                          |
                                                                          v
                                                              +-----------------------+
                                                              |  NodeMCU (ESP8266)    |
                                                              |  GPIO D1 / D2 Relays  |
                                                              +-----------------------+
```

---

## 📂 Project Structure

```text
mine1/
├── index.html       # Modern, responsive IoT dashboard (GitHub Pages ready)
├── utopia.html      # Legacy prototype control page
└── README.md        # Documentation and hardware setup guide
```

---

## 🔌 Hardware Setup (NodeMCU ESP8266)

| NodeMCU Pin | GPIO Number | Function / Device |
| :---: | :---: | :---: |
| **D1** | GPIO 5 | Relay / LED 1 |
| **D2** | GPIO 4 | Relay / LED 2 |
| **3V3 / VIN** | — | VCC Power Supply |
| **GND** | — | Common Ground |

---

## 📡 REST API Contract

The web client communicates with the backend via simple REST endpoints:

### 1. Update Device State
```http
GET /api/led/update.php?id={id}&status={on|off}
```
**Response:**
```json
{
  "message": "Status updated successfully",
  "id": "1",
  "status": "on"
}
```

### 2. Read All Device States
```http
GET /api/led/read_all1.php
```
**Response:**
```json
{
  "led": [
    { "id": "1", "status": "on" },
    { "id": "2", "status": "off" }
  ]
}
```

---

## 🚀 Running Locally

You can open `index.html` directly in your browser, or serve it via Python:

```bash
# Serve locally
python -m http.server 8080
```
Then visit `http://localhost:8080`.

To connect to your local WAMP server, simply update the **API Gateway** input box at the top of the page (e.g. `http://localhost/api/led` or `http://192.168.x.x/api/led`) and click **Save**.

---

## 👤 Author

- **Swastik Tripathi** — [GitHub (@tripathiswastik)](https://github.com/tripathiswastik)

---

## 📄 License

Open-source and distributed under the [MIT License](LICENSE).
