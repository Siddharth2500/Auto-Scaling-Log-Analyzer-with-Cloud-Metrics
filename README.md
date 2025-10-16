# ⚡ Auto-Scaling Log Analyzer (Colab Edition)

![Auto Scaling](https://media.tenor.com/CJyTCZrZ_9kAAAAM/adobe-photoshop-pen-tool.gif)

This project simulates a **cloud auto-scaling engine** that reads **system metrics (CPU usage)**, analyzes trends, and **automatically scales services up or down** based on thresholds, just like AWS Auto Scaling or Kubernetes HPA, but running locally in Colab.


---

## 🚀 Overview

Every few seconds:
1. The system generates CPU metrics for each running instance 
2. The analyzer logs performance to `system_metrics.log` 🪵  
3. If average CPU > 75 %, a new instance is added ⚙️  
4. If average CPU < 25 %, one instance is removed ⚖️  
5. Logs and state updates are written for each decision 🗂️  

It’s a self-contained, observable simulation of **real cloud scaling logic**.

---

## 🧱 Architecture

┌─────────────┐
│ Metrics Gen │ → produces CPU% values
└──────┬──────┘
│
▼
┌────────────────────┐
│ Auto-Scaler Logic │ → decides scale up/down
└──────┬─────────────┘
│
▼
┌────────────────────┐
│ system_metrics.log │ ← log events
└──────┬─────────────┘
│
▼
┌────────────────────┐
│ auto_scale_state.json │ ← current cluster size
└────────────────────┘

yaml
Copy code

---

## 🧰 Tech Stack

| Component | Implementation |
|------------|----------------|
| Language | Python 3 |
| Runtime | Google Colab / Local |
| Cloud Concept | Auto-Scaling (like AWS ASG / K8s HPA) |
| Storage | Local JSON + log file |
| Visualization | Console log output |

---

## 🧪 Run in Colab

1️⃣ Copy the Python code into a Colab cell  
2️⃣ Run it — logs will stream in real time  
3️⃣ The simulation runs ~25 seconds by default  
4️⃣ Stop anytime with the **Stop (■)** button  

---

## 🧾 Sample Log Output

[14:20:02] 🚀 Starting Auto-Scaling Log Analyzer Simulation
[14:20:02] Initial state: 3 instances
[14:20:03] 📊 CPU Metrics: [67, 81, 75]
[14:20:03] 📈 High CPU (74.3%) → scale UP to 4 instances
...
[14:20:20] 📉 Low CPU (22.5%) → scale DOWN to 2 instances

yaml
Copy code

---

## ⚙️ Configuration

| Setting | Default | Description |
|----------|----------|-------------|
| `CPU_SCALE_UP` | 75 | % threshold to add instance |
| `CPU_SCALE_DOWN` | 25 | % threshold to remove instance |
| `MAX_INSTANCES` | 10 | upper scaling limit |
| `MIN_INSTANCES` | 1 | lower scaling limit |
| `METRIC_INTERVAL` | 1 s | sampling interval |

Change any of these at the top of the script.

---

## 🧹 Cleanup

Delete simulation files:
```bash
!rm -f system_metrics.log auto_scale_state.json
💡 Extend This Project
📊 Integrate a Matplotlib dashboard for CPU trends

☁️ Hook into AWS CloudWatch or GCP Stackdriver metrics

 Add predictive scaling using a simple regression model

🔄 Use threading to simulate multiple services in parallel

🪪 License
MIT License © 2025

💬 Author Notes:
This Colab project mimics real-world auto-scaling behavior in a lightweight, local way.
It’s perfect for learning how metric-driven decisions translate into scaling actions, without deploying any real infrastructure.
Experiment with thresholds, visualize trends, and see how intelligent scaling works! ⚙️📈
