# 🧠 SOC Home Lab from Zero — Catching Real Attackers

## **Introduction**

This project demonstrates how to build a **cloud-based Security Operations Center (SOC)** using free **Microsoft Azure** resources.  
It provides a **hands-on cybersecurity experience** by deploying a honeypot, collecting and analyzing real attack logs, and visualizing threats on a live global map.

By completing this lab, you’ll gain **practical skills** in SOC architecture, cloud security, SIEM operations, and attack detection — all while building an impressive **portfolio project**.

---

## **🏗️ Home SOC Architecture Overview**

| Component | Description |
|------------|--------------|
| **Azure Free Subscription** | Uses Azure’s free tier to stay cost-effective and accessible. |
| **Honeypot VM** | A deliberately vulnerable Windows 10 virtual machine exposed to real-world attackers. |
| **Log Analytics Workspace (LAW)** | Central log repository for event collection. |
| **Microsoft Sentinel (SIEM)** | Analyzes security events, generates alerts, and visualizes attack data. |
| **Live Attack Map** | Real-time visualization of attack sources worldwide. |

---

## **🎯 Why This Project Matters**

Building this SOC lab provides both **technical and career value**:

- Demonstrates **cloud computing skills** (Azure setup, VM configuration, and networking).
- Shows **security monitoring and SIEM integration** in action.
- Produces **real attack data and visualizations** for your cybersecurity portfolio.
- Easy to **recreate, explain, and demo** in interviews.

---

## **1️⃣ Setting Up Azure Environment**

### Steps:
1. **Create an Azure Free Subscription:**  
   [👉 Azure Free Account](https://azure.microsoft.com/en-us/pricing/purchase-options/azure-account)  
   *(If unavailable, use a paid subscription but delete resources afterward to avoid costs.)*

2. **Login:**  
   Go to [https://portal.azure.com](https://portal.azure.com)

3. **Create:**
   - A **Resource Group** to organize assets.
   - A **Virtual Network (VNet)** to isolate the honeypot VM securely.

---

## **2️⃣ Creating the Honeypot Virtual Machine**

### Objective:
Deploy a vulnerable Windows 10 VM to **attract and record real cyberattacks**.

### Steps:
1. In Azure Portal → Search for **Virtual Machines** → **Create New VM**  
   - OS: *Windows 10*
   - Size: *Smallest available for cost-efficiency*
   - Credentials: *Save your username/password securely.*

2. **Network Configuration:**
   - Open **Network Security Group (NSG)** settings.
   - **Delete** existing RDP rule.
   - **Add new rule** named `DangerAllowAnyCustomAnyInbound` allowing all inbound traffic.

3. **Inside VM:**
   - Connect via **RDP**.
   - Disable the **Windows Firewall** (`wf.msc → Properties → Turn Off for all profiles`).

💡 *This step intentionally exposes your VM — proceed only in controlled lab environments!*

---

## **3️⃣ Observing Initial Attacks**

Once deployed, your VM will attract automated attacks within minutes.

### Steps to Monitor:
1. Log into VM and open **Event Viewer**  
   - `Win + R → eventvwr.msc`
2. Navigate to:  
   **Windows Logs → Security**
3. Look for **Event ID 4625** → *Failed Login Attempts*
4. Observe details such as:
   - Username tried (e.g., `employee`)
   - Source IP address
   - Failure reason (bad password, etc.)

💡 *You can simulate attacks by entering incorrect credentials to generate logs.*

---

## **4️⃣ Log Forwarding & KQL Queries**

### Step 1: Create a Log Analytics Workspace (LAW)
1. Azure Portal → **Log Analytics Workspaces**
2. Click **Create** → Choose Resource Group, Region, and Name
3. Note the **Workspace ID** and **Key**

### Step 2: Enable Microsoft Sentinel
1. Navigate to **Microsoft Sentinel**
2. Click **+ Add** → Select your LAW → Click **Add Microsoft Sentinel**

### Step 3: Install Azure Monitor Agent (AMA)
1. Go to your **VM → Extensions + Applications**
2. Add **Azure Monitor Agent**
3. Create **Data Collection Rule (DCR)** to collect:
   - `SecurityEvent` logs (Event ID 4625)
   - Optionally: `Sysmon` or `Application` logs

### Step 4: Query the Logs (KQL)
```kql
SecurityEvent
| where EventID == 4625
| project TimeGenerated, Account, Computer,
          IpAddress = tostring(parse_json(AdditionalFields)["IpAddress"]),
          FailureReason
| sort by TimeGenerated desc
```

✅ This filters for failed logins, extracts IPs and reasons, and sorts by recent attempts.

---

## **5️⃣ Enriching Logs with Geographic Data**

To visualize **where attacks originate**, enrich logs using **GeoIP data**.

### Steps:
1. Download:  
   [`geoip-summarized.csv`](https://raw.githubusercontent.com/joshmadakor1/lognpacific-public/refs/heads/main/misc/geoip-summarized.csv)
2. In Sentinel → **Watchlists → Add New**
   - Name: `geoip`
   - Source: Local file
   - Search key: `network`
   - Rows: ~54,000 entries (IPv4 blocks → location)
3. Join this data to SecurityEvent logs:
```kql
let GeoIPDB_FULL = _GetWatchlist("geoip");
let WindowsEvents = SecurityEvent
    | where EventID == 4625
    | evaluate ipv4_lookup(GeoIPDB_FULL, IpAddress, network);
WindowsEvents
```
This adds **country, region, and coordinates** for visualization.

---

## **6️⃣ Attack Map Creation (Sentinel Workbook)**

### Build a Real-Time Global Map:
1. In **Sentinel → Workbooks → New Workbook**
2. Delete defaults → Add a **Query** element
3. Switch to **Advanced Editor** and paste JSON from [`map.json`](/map.json)
4. Save and view live **Attack Map** with geo-located events.

---

## **✅ Conclusion**

You’ve successfully built a **fully functional mini SOC**:
- Attracted real attackers.
- Captured and analyzed attack logs.
- Integrated logs into Sentinel.
- Enriched data with geolocation.
- Created a live global attack dashboard.

This project showcases your ability to **design, deploy, and operate a SOC pipeline** from scratch — a highly valuable demonstration for cybersecurity portfolios and interviews.

---

### **💡 Recommended Next Steps**
- Add **Sysmon** for deeper event visibility.
- Use **Azure Logic Apps** for automated alerts.
- Expand to **multi-cloud SOC (AWS, GCP)** comparison.
- Publish results on your **GitHub Pages** or **LinkedIn portfolio**.
