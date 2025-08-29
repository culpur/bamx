# BamX  
[![Python](https://img.shields.io/badge/python-3.11-blue.svg)](https://www.python.org/downloads/release/python-3110/)  
[![Docker](https://img.shields.io/badge/docker-ready-brightgreen.svg)](https://www.docker.com/)  
[![Flask](https://img.shields.io/badge/flask-2.3-lightgrey.svg)](https://flask.palletsprojects.com/)  
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)  
[![Status](https://img.shields.io/badge/status-active-success.svg)]()  

---

## 🚀 Overview  
**BamX** is a **Dashboard + Backend API** for managing 3D print jobs, printers, and filament usage.  

It is designed to **connect to [Bambu Connect (beta)](https://bambulab.com/)** — which runs on the host (macOS/Windows) — while BamX itself runs in Docker. BamX provides:  

- A **backend API** for jobs, printers, filament, and metrics.  
- A **Dashboard UI** for live monitoring of printers, jobs, and usage.  
- Persistent state using JSON files under `/data`.  
- Integration layer to communicate with **Bambu Connect**.  

> 🔹 **Important**: At present, Bambu Connect only supports **Windows/macOS**, so BamX runs in Docker and relays to the host’s Bambu Connect daemon until a Linux version is released.  

---

## 📁 Project Structure
```bash
BamX/
├── app.py                  # Main application entrypoint
├── routes/                 # Flask Blueprints
│   ├── job_routes.py       # Job endpoints
│   ├── printer_routes.py   # Printer endpoints
│   ├── filament_routes.py  # Filament endpoints
│   └── dashboard_routes.py # Dashboard UI
├── services/               # Business logic
│   ├── job_service.py
│   ├── printer_service.py
│   └── filament_service.py
├── templates/              # HTML templates
│   └── dashboard.html
├── data/                   # Persistent JSON storage
│   ├── jobs.json
│   ├── failed_jobs.json
│   ├── printers.json
│   └── filament_stats.json
├── Dockerfile              # Docker image
├── docker-compose.yml      # Compose setup
├── requirements.txt        # Python dependencies
└── README.md
```

---

## 🖥️ Dashboard
- Web-based dashboard at `/dashboard` (HTML/JS frontend).  
- Displays:  
  - **Jobs summary** (total, failed, success rate).  
  - **Printer list**.  
  - **Filament stats**.  
  - **System metrics**.  
- Job history table with `job_id`, `name`, `status`, `timestamp`.  
- Future: Navigation pane with printer/filament/job management actions.  

---

## 🧪 Setup & Run

### 1. Clone the repo
```bash
git clone https://github.com/culpur/bamx.git
cd bamx
```

### 2. Build with Docker
```bash
docker compose build --no-cache
docker compose up -d
```

### 3. Access the Dashboard
Open: [http://localhost:5005/dashboard](http://localhost:5005/dashboard)  

---

## 📡 Example Endpoints
- `POST /printers/register` → Register a printer  
- `POST /jobs/submit` → Submit a job  
- `GET /jobs/summary` → Get job stats  
- `GET /filament/stats` → Get filament usage stats  
- `GET /metrics` → App metrics  

---

## 📌 Integration with Bambu Connect
- **BamX does not replace Bambu Connect** — instead, it provides an API and dashboard to interact with it.  
- Bambu Connect runs on the **host (macOS/Windows)**.  
- BamX runs in **Docker** and communicates with the host Bambu Connect process.  
- This allows:  
  - Centralized metrics, jobs, and filament tracking.  
  - A unified dashboard for monitoring.  
  - Persistence across container restarts.  

---

## 📜 License
MIT License © 2025 [Culpur Defense Inc.](https://culpur.net)  
