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
## Configuration

### Discord Webhook

Edit `main.sh` and replace the placeholder `WEBHOOK_URL` with your actual Discord webhook URL:

```bash
WEBHOOK_URL="https://discord.com/api/webhooks/your_webhook_id/your_webhook_token"
```

**Optional:** For security, you can modify the script to read the webhook from an environment variable (see Advanced Configuration below).

### Threshold

The alert threshold is set to `80` in the script. Change it by editing the `THRESHOLD` variable at the top of `main.sh`:

```bash
THRESHOLD=80   # Change to desired percentage
```

## Usage

### Running Locally

1. **Start the FastAPI server**

```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```
## API Endpoints

| Endpoint       | Method | Description                          |
|----------------|--------|--------------------------------------|
| `/`            | GET    | Serves the HTML dashboard.           |
| `/api/health`  | GET    | Returns JSON with current metrics.   |

Example `/api/health` response:

```json
{
  "cpu_model": "Intel(R) Core(TM) i7-10750H",
  "total_ram": "15Gi",
  "disk_usage": 45,
  "ram_usage": 30,
  "cpu_load": 10,
  "threshold": 80,
  "hostname": "my-server"
}
```

## Dashboard

The dashboard auto‑refreshes every 5 seconds. Metrics that exceed the threshold are highlighted in red.

## Advanced Configuration

### Using Environment Variables for Discord Webhook

Modify the Bash script to read the webhook from an environment variable:

```bash
WEBHOOK_URL="${DISCORD_WEBHOOK_URL:-}"
```
Common causes:
- **Wrong script path** – Ensure `SCRIPT_PATH` in `main.py` points to the correct location inside the container (`/app/main.sh`).
- **Missing `jq`** – The Bash script requires `jq`. If running locally, install it. In Docker, the `Dockerfile` should install it.
- **Script not executable** – Run `chmod +x main.sh` and rebuild.

### 2. Dashboard shows "Error loading data"

Open browser developer tools (F12) and check the network tab for the `/api/health` request. The response should contain an error message.

### 3. Discord alerts not sent

- Verify the webhook URL is correct.
- Ensure `curl` is installed.
- If using the environment variable, confirm it is passed correctly.

---

Enjoy monitoring your server!
chmod +x main.sh
```
