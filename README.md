# SecuFlow


SecuFlow is an **AI-powered security automation workflow** built with [n8n](https://n8n.io).  
It monitors SSH login attempts in real time, detects suspicious patterns,
and allows a **human-in-the-loop** Telegram approval before blocking attackers.

## 🚀 Features
- 🔍 **Real-Time SSH Monitoring**  
  Pulls live SSH logs via secure SSH commands.
- 🤖 **AI Threat Analysis**  
  Uses Groq LLM to generate a 2–3 line risk summary of detected IPs.
- 📊 **Automated Threshold Detection**  
  Counts failed attempts per IP and flags any IP with >3 failures.
- 👨‍💻 **Human Approval**  
  Sends a Telegram alert with YES/NO options before executing firewall rules.
- 🔒 **Active Defense**  
  Executes `ufw` commands via SSH to block malicious IPs instantly.

## 🛠️ Tech Stack
- **n8n** – Workflow automation engine
- **Groq LLM (Llama 3.1)** – AI risk analysis
- **Telegram Bot API** – Human-in-the-loop decision making
- **SSH (UFW)** – Remote firewall command execution

## ⚡ Workflow Overview
1. Fetch SSH logs (`journalctl`) from target server.
2. Parse logs (Python node) → Extract timestamp, user, IP, status.
3. Count failed attempts per IP (JavaScript node).
4. If failures > 3 → pass IP to Groq LLM for a brief attack summary.
5. Send Telegram alert → Admin replies **YES** or **NO**.
6. On **YES**, run `sudo ufw deny from <ip>` to block the attacker.

## 📸 Screenshots
Below are key screenshots showing SecuFlow in action.  
*(Place all images inside a `screenshots/` folder in this repository)*

### n8n Workflow
<img width="1821" height="777" alt="Screenshot 2025-09-30 163753" src="https://github.com/user-attachments/assets/01fe369c-f901-4fe0-8156-7971bf2556a8" />


### Telegram Alert
<img width="1707" height="783" alt="Screenshot 2025-09-30 163815" src="https://github.com/user-attachments/assets/5b44e15e-1297-4f5a-b852-aea55ad9af48" />


## 🔧 Setup
1. Import `workflow.json` into n8n.
2. Add credentials:
   - **SSH Private Key** (to access the target server)
   - **Groq API Key**
   - **Telegram Bot Token + Chat ID**
3. Deploy n8n and activate the workflow.

## 📜 License
[MIT License](LICENSE)
