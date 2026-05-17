# 🛡️ n8n SOC Threat Detection Automation

An automated SOC (Security Operations Center) workflow built using **n8n** that analyzes suspicious IP activity using **VirusTotal intelligence** and sends automated email alerts based on calculated risk scores.

---
<img width="1365" height="684" alt="Screenshot 2026-05-17 044821" src="https://github.com/user-attachments/assets/a69db1c2-8840-45c8-81d8-921ef5c1689a" />
----------------------
# 🚀 Features

* ✅ Webhook-based event ingestion
* ✅ VirusTotal IP reputation lookup
* ✅ Automated risk scoring engine
* ✅ Safe vs Critical threat classification
* ✅ Gmail alert automation
* ✅ SOC-style workflow design
* ✅ Lightweight SIEM enrichment pipeline

---

# 🧠 Workflow Overview

```text
Webhook
   ↓
Parse Event Data
   ↓
VirusTotal API Lookup
   ↓
Risk Scoring Engine
   ↓
Switch Decision Logic
   ↓
SAFE or CRITICAL Email Alert
```

---

# ⚙️ Technologies Used

* n8n
* VirusTotal API
* Gmail API
* JavaScript
* Webhooks
* SOC Automation Concepts

---

# 📦 Risk Score Logic

```javascript
let score = 0;

if (vt.malicious > 0) score += 50;
if (vt.suspicious > 0) score += 20;

if (count > 20) score += 20;
```

---

# 🚦 Alert Classification

| Score   | Classification |
| ------- | -------------- |
| `< 70`  | SAFE 🟢        |
| `>= 70` | CRITICAL 🚨    |

---

# 🔌 Example Incoming Payload

```json
{
  "ip": "8.8.8.8",
  "user": "test_user",
  "event": "failed_login",
  "count": 30
}
```

---

# 📬 Email Alerts

## 🟢 SAFE Alert

Sent when activity appears non-malicious.

## 🚨 CRITICAL Alert

Sent when VirusTotal and event data indicate potentially malicious activity.

---

# 🧪 How to Test

## 1. Start n8n

```bash
n8n start
```

---

## 2. Activate Workflow

Enable the workflow inside n8n.

---

## 3. Send Test Request

### PowerShell

```powershell for safe alert
Invoke-WebRequest -Uri "http://localhost:5678/webhook-test/splunk-alert" `
-Method POST `
-Body '{"ip":"8.8.8.8","user":"test_user","event":"failed_login","count":30}' `
-ContentType "application/json"
```
```powershell for critical alert
Invoke-RestMethod -Method POST `
  -Uri "http://localhost:5678/webhook-test/splunk-alert" `
  -ContentType "application/json" `
  -Body '{
    "ip": "1.2.3.4",
    "user": "attacker",
    "event": "sql_injection_attempt",
    "count": 200
  }'
```

---

# 📁 Recommended Project Structure

```text
n8n-soc-threat-detection/
│
├── workflow.json
├── README.md
├── LICENSE
├── screenshots/
│   ├── workflow.png
│   ├── critical-alert.png
│   └── safe-alert.png
```

---

# 📸 Screenshots

Add screenshots inside the `/screenshots` folder.

Recommended screenshots:

* Workflow design
* SAFE email alert
* CRITICAL email alert

---

# 🔐 Security Notes

⚠️ Never expose:

* VirusTotal API keys
* Gmail credentials
* OAuth tokens

Use environment variables or n8n credentials instead.

---

# 📈 Future Improvements

* Slack / Discord alerting
* GeoIP enrichment
* Threat intelligence feeds
* Splunk HEC integration
* Automatic firewall blocking
* Elasticsearch logging
* Dashboard visualization

---

# 👨‍💻 Author

Built using **n8n automation + SOC threat detection logic**

---

# ⭐ Support

If you like this project, give it a star ⭐
