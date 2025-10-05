# 🧠 SOC Home Lab from Zero — Catching Real Attackers

> **Author:** Dr. Hazem A. Elbaz  
> [GitHub Profile](https://github.com/elbazhazem) | [Personal Website](https://elbazhazem.github.io) | [LinkedIn](https://www.linkedin.com/in/hazem-elbaz/)

---

## 🚀 Overview

This repository demonstrates how to **build a functional Security Operations Center (SOC) from scratch** using **Microsoft Azure**, **Microsoft Sentinel**, and open-source tools — entirely **for free**.

It provides a **step-by-step practical guide** for cybersecurity learners, professionals, and educators who want to understand **how real-world SOCs detect and analyze attacks**.

You’ll learn how to:
- Deploy and expose a **honeypot virtual machine**.
- Collect and forward **security logs**.
- Integrate **Azure Log Analytics** and **Microsoft Sentinel** for SIEM operations.
- Enrich logs with **GeoIP location data**.
- Build a **live global attack visualization map**.

---

## 🧩 Repository Structure

| Folder/File | Description |
|--------------|-------------|
| `SOC_Home_Lab_from_ZERO.md` | Full detailed guide for building the SOC environment. |
| `map.json` | JSON file used to create the real-time attack map in Sentinel Workbooks. |
| `geoip-summarized.csv` | GeoIP dataset used to enrich log data with geolocation details. |
| `images/` | Screenshots and visual diagrams of the SOC setup. |
| `README.md` | This introduction file. |

---

## 📖 Read the Full Article

For a detailed explanation, visual walkthrough, and lessons learned, check out my full Medium post:

👉 [**Building a SOC Home Lab from Zero — Catching Real Attackers on Azure**](https://medium.com/@hazemelbaz/soc-home-lab-from-zero-catching-attackers) *(Replace with your actual post link)*

---

## ⚙️ Key Skills Demonstrated

- **Cloud Security:** Azure setup, resource management, and cost control  
- **SOC Operations:** Log collection, event correlation, KQL querying  
- **SIEM Configuration:** Microsoft Sentinel integration and visualization  
- **Threat Intelligence:** Attack pattern recognition and geo-mapping  
- **Portfolio Development:** Creating a real, replicable lab for job interviews and training

---

## 🧠 Lessons Learned

- Exposing a system to the internet yields **immediate real-world attack data**.  
- Understanding **Event ID 4625 (failed logins)** is critical in brute-force detection.  
- **KQL (Kusto Query Language)** is an essential SOC analyst skill.  
- Visualizing threats geographically helps communicate security posture effectively.  

---

## 🧭 Next Steps

- Integrate **Sysmon** for deeper process visibility.  
- Add **Logic Apps** to automate alerts and response.  
- Expand the lab to **AWS or GCP** for multi-cloud monitoring.  
- Incorporate **LLM-based log summarization** for faster threat triage.

---

## 📬 Connect

If you find this useful or want to collaborate on AI-Driven SOC Automation research, feel free to connect or reach out:

- 🌐 [hazemelbaz.github.io](https://hazemelbaz.github.io)  
- 💼 [LinkedIn](https://www.linkedin.com/in/hazem-elbaz/)  
- ✉️ hazem_baz@alaqsa.edu.ps

---

### 🏁 License
This project is released under the **MIT License** — free to use, modify, and share for educational purposes.

---

*“Every attack is a lesson — the key is building systems that learn faster than attackers do.”*
