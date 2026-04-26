# Server Watchdog

A lightweight server monitoring tool that combines a Bash script for health checks and Discord alerts with a FastAPI web dashboard for live metrics.

## Features

- **System Metrics** – CPU model, total RAM, disk usage, RAM usage, CPU load.
- **Discord Alerts** – Sends notifications when disk, RAM, or CPU usage exceed a configurable threshold (default 80%).
- **Live Web Dashboard** – Auto‑refreshing page showing current metrics with colour‑coded warnings.
- **Flexible Deployment** – Run locally or in a Docker container.
- **JSON API** – Exposes metrics via a simple `/api/health` endpoint.

## Prerequisites

- **Bash** – The monitoring script is written in Bash.
- **jq** – Used for JSON construction in the Bash script.
- **curl** – Required for Discord webhook calls.
- **Python 3.9+** – For the FastAPI web server (if running locally).
- **FastAPI & Uvicorn** – Python dependencies (see below).

If using Docker, only Docker Engine is required on the host.

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/server-watchdog.git
cd server-watchdog
```

### 2. Local Installation

#### Install System Dependencies (Ubuntu/Debian example)

```bash
sudo apt update
sudo apt install bash jq curl python3 python3-pip
```

#### Install Python Packages

```bash
pip3 install fastapi uvicorn
```

#### Make the Bash Script Executable

```bash
chmod +x main.sh
```
