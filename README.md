<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0F2027,50:2C5364,100:1e3c72&height=220&section=header&text=Wazuh%20SOC%20Home%20Lab&fontSize=48&fontColor=ffffff&animation=fadeIn&fontAlignY=38&desc=Security%20Operations%20Center%20%7C%20SIEM%20Monitoring%20%7C%20Threat%20Detection&descAlignY=58&descSize=18" alt="Wazuh SOC Home Lab banner"/>
</p>

<p align="center">
  <img src="https://readme-typing-svg.demolab.com/?font=Fira+Code&weight=500&size=22&duration=3000&pause=1000&color=2C5364&center=true&vCenter=true&width=750&lines=Hands-on+SOC+Analyst+Home+Lab;Monitoring+Windows+Endpoints+with+Wazuh+SIEM;Investigating+Successful+%26+Failed+Logons;Building+Practical+Blue+Team+Skills" alt="Typing SVG"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/status-in%20progress-yellow?style=for-the-badge" alt="status"/>
  <img src="https://img.shields.io/badge/focus-Blue%20Team%20%7C%20SOC-2C5364?style=for-the-badge" alt="focus"/>
  <img src="https://img.shields.io/badge/type-Home%20Lab-blueviolet?style=for-the-badge" alt="type"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Wazuh-005571?style=for-the-badge&logo=wazuh&logoColor=white" alt="Wazuh"/>
  <img src="https://img.shields.io/badge/Ubuntu%20Server-E95420?style=for-the-badge&logo=ubuntu&logoColor=white" alt="Ubuntu Server"/>
  <img src="https://img.shields.io/badge/Windows%2010-0078D6?style=for-the-badge&logo=windows&logoColor=white" alt="Windows 10"/>
  <img src="https://img.shields.io/badge/VMware-607078?style=for-the-badge&logo=vmware&logoColor=white" alt="VMware"/>
  <img src="https://img.shields.io/badge/Kali%20Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white" alt="Kali Linux"/>
  <img src="https://img.shields.io/badge/SIEM-4B0082?style=for-the-badge" alt="SIEM"/>
</p>

<p align="center">
  A hands-on <b>Security Operations Center (SOC)</b> home lab built to practice SIEM monitoring, Windows event analysis, endpoint monitoring, threat detection, and incident investigation.
</p>

---

## 📑 Table of Contents

- [📖 Overview](#-overview)
- [🏗️ Lab Architecture](#-lab-architecture)
- [🧰 Technologies Used](#-technologies-used)
- [🧩 Lab Components](#-lab-components)
- [🔍 Security Event Investigation](#-security-event-investigation)
- [🧭 Investigation Methodology](#-investigation-methodology)
- [🎓 SOC Skills Practiced](#-soc-skills-practiced)
- [⚔️ Future Attack Simulation Plan](#-future-attack-simulation-plan)
- [🚦 Future SOC Development](#-future-soc-development)
- [🔄 Learning Methodology](#-learning-methodology)
- [🗺️ Project Roadmap](#-project-roadmap)
- [📁 Repository Structure](#-repository-structure)
- [🎓 Learning Goals](#-learning-goals)
- [⚠️ Disclaimer](#-disclaimer)
- [👤 Author](#-author)

---

## 📖 Overview

The lab consists of a centralized **Wazuh SOC Server** and a monitored **Windows 10 endpoint**. The current environment allows security events generated on the Windows endpoint to be collected and analyzed through the Wazuh platform.

The project will later be expanded with a **Kali Linux** virtual machine for authorized security testing and attack simulation inside an isolated lab environment.

<table>
<tr>
<td valign="top" width="50%">

**🎯 Current Objectives**
- Build a functional SOC lab
- Deploy and configure Wazuh
- Monitor Windows endpoints
- Collect Windows Event Logs
- Investigate authentication events
- Analyze successful and failed logons
- Practice SIEM queries and filtering
- Learn event correlation
- Develop SOC investigation skills

</td>
<td valign="top" width="50%">

**🔮 Future Objectives**
- Integrate Kali Linux
- Perform authorized attack simulations
- Generate suspicious activity
- Detect attacks using Wazuh
- Investigate security alerts
- Create custom detection rules
- Map activity to MITRE ATT&CK
- Practice incident response
- Build threat hunting skills

</td>
</tr>
</table>

### 📌 Quick Facts

| Item | Detail |
|---|---|
| Agent ID | `002` |
| Agent Name | `MSEDGEWIN10` |
| Agent Status | 🟢 Active |
| Manager | `wazuh-soc-server` |
| Primary Events Investigated | `4624` (Success) · `4625` (Failure) |
| Investigation Window | Aug 1 – Aug 31, 2026 |

---

## 🏗️ Lab Architecture

### Current Environment

```mermaid
flowchart BT
    subgraph EP["🖥️ Windows 10 Endpoint"]
        WA["Wazuh Agent"]
        WEL["Windows Event Logs"]
    end
    subgraph SRV["🛡️ Wazuh SOC Server — Ubuntu Server"]
        WM["Wazuh Manager"]
        WD["Wazuh Dashboard"]
    end
    EP -- "Security Events" --> SRV
```

### Future Authorized Security Testing Environment

```mermaid
flowchart LR
    K["🐉 Kali Linux VM<br/>Authorized Security Testing"] -- "Simulated Activity" --> W["🖥️ Windows 10 Endpoint<br/>Wazuh Agent · Event Generation"]
    W -- "Security Events" --> S["🛡️ Wazuh SOC Server<br/>Detection & Investigation"]
```

> All simulated activity stays inside an isolated, authorized home-lab network. See [Disclaimer](#-disclaimer).

---

## 🧰 Technologies Used

| Technology | Role in the Lab |
|---|---|
| 🛡️ **Wazuh** | Core SIEM platform — manager, dashboard, agent |
| 🐧 **Ubuntu Server** | Host OS for the Wazuh SOC Server |
| 🪟 **Windows 10** | Monitored endpoint generating security events |
| 🔌 **Wazuh Agent** | Forwards Windows Event Logs to the manager |
| 💻 **VMware Workstation Player** | Virtualization platform for the lab |
| 📄 **Windows Event Logs** | Source of authentication & system events |
| 📊 **SIEM** | Security monitoring, correlation & alerting |
| 🐉 **Kali Linux** | Planned — authorized attack simulation |
| 🐙 **GitHub** | Documentation & version control |

---

## 🧩 Lab Components

### 1️⃣ Wazuh SOC Server
Running on **Ubuntu Server**, the Wazuh SOC Server provides centralized security monitoring and is responsible for:

- Receiving endpoint logs
- Processing security events
- Monitoring agents
- Detecting suspicious activity
- Generating alerts
- Supporting log investigations
- Providing centralized security visibility

> The Wazuh Dashboard is accessed through a web browser from the Windows machine.

### 2️⃣ Windows 10 Endpoint
A Windows 10 virtual machine configured as the monitored endpoint, used to generate and monitor:

- Windows Security Events
- Authentication events (successful & failed logons)
- System events
- Endpoint activity

### 3️⃣ Wazuh Agent

The Wazuh Agent was successfully installed and connected to the Wazuh SOC Server, forwarding Windows Event Logs to the platform for analysis.

| Field | Value |
|---|---|
| Agent ID | `002` |
| Agent Name | `MSEDGEWIN10` |
| Status | 🟢 Active |
| Manager | `wazuh-soc-server` |

---

## 🔍 Security Event Investigation

The **Wazuh Discover** interface was used to investigate Windows authentication events, focused on two key Windows Security Event IDs.

### 🟢 Event ID 4624 — Successful Logon

Windows Event ID `4624` indicates that a logon attempt was successful.

```
agent.id:002 AND data.win.system.eventID:4624
```

**Fields reviewed:** Agent ID · Agent Name · Event ID · Target Username · Source IP Address · Logon Type · Authentication Package · Process Name · Workstation Name · Timestamp

The investigation identified multiple successful logon events, reviewed to understand normal authentication activity on the endpoint.

### 🔴 Event ID 4625 — Failed Logon

Windows Event ID `4625` indicates that a logon attempt failed.

```
agent.id:002 AND data.win.system.eventID:4625
```

**Fields reviewed:** Agent ID · Agent Name · Event ID · Target Username · Failure Reason · Status Code · Sub-status Code · Logon Type · Source IP Address · Authentication Package · Process Name · Workstation Name · Timestamp

| Field | Observed Value |
|---|---|
| Event ID | `4625` |
| Target Username | `IEUser` |
| Source IP Address | `127.0.0.1` |
| Logon Type | `2` |
| Authentication Package | `Negotiate` |
| Process Name | `C:\Windows\System32\svchost.exe` |
| Failure Reason | `Unknown user name or bad password` |

Multiple failed authentication events were identified and reviewed.

### 👤 Specific User Investigation — `IEUser`

```
# Failed logons
agent.id:002 AND data.win.system.eventID:4625 AND data.win.eventdata.targetUserName:"IEUser"

# Successful logons
agent.id:002 AND data.win.system.eventID:4624 AND data.win.eventdata.targetUserName:"IEUser"
```

### 🧾 Initial Investigation Findings

- Event ID `4625` represented failed logon attempts; `4624` represented successful logons
- Both event types originated from **Agent ID 002** (`MSEDGEWIN10`)
- The investigated username was **`IEUser`**, source IP **`127.0.0.1`**
- Activity appeared to originate locally from the endpoint
- No immediate evidence of an external source was identified during the initial review
- This investigation was limited to currently available events — an **initial** analysis of authentication activity

> Future attack simulations will allow more advanced detection and correlation exercises.

---

## 🧭 Investigation Methodology

<details open>
<summary><b>Click to expand the 7-step investigation process</b></summary>
<br/>

| Step | Action | Detail |
|---|---|---|
| 1 | **Access Wazuh Dashboard** | Opened from the Windows machine via web browser; the Wazuh SOC Server ran on the Ubuntu Server VM |
| 2 | **Verify Agent Status** | Confirmed Agent `002` (`MSEDGEWIN10`) was Active |
| 3 | **Select Investigation Time Range** | Configured Wazuh Discover for `Aug 1 – Aug 31, 2026` |
| 4 | **Investigate Failed Logons** | `agent.id:002 AND data.win.system.eventID:4625` |
| 5 | **Investigate Successful Logons** | `agent.id:002 AND data.win.system.eventID:4624` |
| 6 | **Investigate Specific Username** | Filtered both event types on `targetUserName:"IEUser"` |
| 7 | **Compare Events** | Compared username, agent, source IP, logon type, process name, timestamp, auth package & failure reason to assess whether activity was expected or suspicious |

</details>

---

## 🎓 SOC Skills Practiced

<p align="left">
<img src="https://img.shields.io/badge/-SIEM%20Monitoring-1B3B6F?style=flat-square"/> <img src="https://img.shields.io/badge/-Wazuh%20Administration-005571?style=flat-square"/> <img src="https://img.shields.io/badge/-Endpoint%20Monitoring-2C5364?style=flat-square"/> <img src="https://img.shields.io/badge/-Windows%20Event%20Log%20Analysis-0078D6?style=flat-square"/> <img src="https://img.shields.io/badge/-Authentication%20Monitoring-4B0082?style=flat-square"/> <img src="https://img.shields.io/badge/-Failed%20Logon%20Investigation-8B0000?style=flat-square"/> <img src="https://img.shields.io/badge/-Successful%20Logon%20Investigation-2E8B57?style=flat-square"/> <img src="https://img.shields.io/badge/-Security%20Event%20Filtering-557C94?style=flat-square"/> <img src="https://img.shields.io/badge/-SIEM%20Query%20Creation-1B3B6F?style=flat-square"/> <img src="https://img.shields.io/badge/-Alert%20Investigation-005571?style=flat-square"/> <img src="https://img.shields.io/badge/-Log%20Correlation-2C5364?style=flat-square"/> <img src="https://img.shields.io/badge/-Security%20Event%20Analysis-4B0082?style=flat-square"/> <img src="https://img.shields.io/badge/-Incident%20Investigation-8B0000?style=flat-square"/> <img src="https://img.shields.io/badge/-Basic%20Threat%20Detection-2E8B57?style=flat-square"/>
</p>

---

## ⚔️ Future Attack Simulation Plan

The lab will be expanded with a **Kali Linux** virtual machine, used only inside the authorized and isolated virtual lab environment.

```mermaid
flowchart TD
    A["1️⃣ Generate authorized testing activity — Kali Linux"] --> B["2️⃣ Target isolated Windows test endpoint"]
    B --> C["3️⃣ Generate Windows security events"]
    C --> D["4️⃣ Collect events via Wazuh Agent"]
    D --> E["5️⃣ Forward events to Wazuh SOC Server"]
    E --> F["6️⃣ Detect & analyze activity"]
    F --> G["7️⃣ Investigate alerts"]
    G --> H["8️⃣ Document findings"]
```

**Planned scenarios:**

| Category | Scenarios |
|---|---|
| Reconnaissance | Network discovery · Port scanning |
| Authentication Attacks | Auth attack simulation · Brute-force detection scenarios |
| Endpoint Activity | Suspicious process activity · File modification monitoring · File Integrity Monitoring |
| Advanced | Malware simulation (safe techniques) · Privilege escalation detection |
| Detection Engineering | Custom Wazuh rules · Alert correlation · Threat hunting exercises |

> ⚠️ All testing remains inside the authorized home-lab environment.

---

## 🚦 Future SOC Development

<table>
<tr><td width="25%" valign="top">

**🛠️ Detection Engineering**
- Create custom Wazuh rules
- Improve alert accuracy
- Reduce false positives
- Create detection logic

</td><td width="25%" valign="top">

**🕵️ Threat Hunting**
- Search for suspicious patterns
- Investigate unusual auth behavior
- Analyze endpoint activity
- Correlate multiple events

</td><td width="25%" valign="top">

**🚨 Incident Response**
- Create investigation reports
- Document timelines
- Identify indicators of compromise
- Record containment recommendations

</td><td width="25%" valign="top">

**🗺️ MITRE ATT&CK**
- Map future simulations
- Map detections to techniques
- Align with industry framework

</td></tr>
</table>

---

## 🔄 Learning Methodology

This project follows a practical, hands-on, and cyclical learning approach:

```mermaid
flowchart LR
    A["Generate Activity"] --> B["Collect Security Logs"]
    B --> C["Detect Events"]
    C --> D["Investigate Alerts"]
    D --> E["Analyze Evidence"]
    E --> F["Document Findings"]
    F --> G["Improve Detection"]
    G -. feeds back into .-> A
```

> The objective is not only to understand cybersecurity concepts theoretically, but to develop practical investigation skills.

---

## 🗺️ Project Roadmap

<p align="left">
<img src="https://img.shields.io/badge/Overall%20Progress-2%2F4%20Phases%20Complete-yellow?style=for-the-badge"/>
</p>

<details open>
<summary><b>✅ Phase 1 — SOC Lab Setup</b> &nbsp;<img src="https://img.shields.io/badge/-Complete-brightgreen?style=flat-square"/></summary>
<br/>

- [x] Install VMware
- [x] Deploy Ubuntu Server
- [x] Install Wazuh
- [x] Access Wazuh Dashboard
- [x] Deploy Windows 10 endpoint
- [x] Install Wazuh Agent
- [x] Connect Windows endpoint to Wazuh

</details>

<details open>
<summary><b>✅ Phase 2 — Log Analysis</b> &nbsp;<img src="https://img.shields.io/badge/-Complete-brightgreen?style=flat-square"/></summary>
<br/>

- [x] Collect Windows Event Logs
- [x] Investigate Event ID 4624
- [x] Investigate Event ID 4625
- [x] Filter events by Agent ID
- [x] Investigate specific username
- [x] Compare successful and failed authentication events

</details>

<details>
<summary><b>🔜 Phase 3 — Attack Simulation</b> &nbsp;<img src="https://img.shields.io/badge/-Planned-lightgrey?style=flat-square"/></summary>
<br/>

- [ ] Deploy Kali Linux
- [ ] Configure isolated lab networking
- [ ] Perform authorized security testing
- [ ] Generate detectable events
- [ ] Monitor events in Wazuh
- [ ] Investigate generated alerts

</details>

<details>
<summary><b>🔜 Phase 4 — Advanced Detection</b> &nbsp;<img src="https://img.shields.io/badge/-Planned-lightgrey?style=flat-square"/></summary>
<br/>

- [ ] Create custom Wazuh rules
- [ ] Configure custom alerts
- [ ] Perform threat hunting
- [ ] Map events to MITRE ATT&CK
- [ ] Create incident response reports

</details>

**Also upcoming:** adding screenshots to the repository and writing detailed investigation reports for the completed phases.

---

## 📁 Repository Structure

<details>
<summary><b>Click to view planned repository structure</b></summary>
<br/>

```
wazuh-soc-home-lab/
│
├── README.md
│
├── screenshots/
│   ├── wazuh-dashboard/
│   ├── agent-status/
│   └── investigations/
│
├── investigations/
│   ├── successful-logon-analysis.md
│   └── failed-logon-analysis.md
│
├── attack-simulations/
│   └── future-lab-scenarios/
│
└── reports/
    └── incident-reports/
```

</details>

---

## 🎓 Learning Goals

<table>
<tr><td width="50%">

- Security Operations Center operations
- Blue Team security
- SIEM technologies
- Wazuh
- Log analysis
- Threat detection

</td><td width="50%">

- Endpoint monitoring
- Windows security events
- Incident investigation
- Threat hunting
- Detection engineering

</td></tr>
</table>

---

## ⚠️ Disclaimer

This project is strictly for **educational purposes** and **authorized cybersecurity testing**.

All security testing, simulations, and experiments are performed only inside a **controlled and isolated virtual lab environment**. No unauthorized systems, networks, accounts, or devices are targeted.

---

## 👤 Author

<p align="center">
<b>Daniyal Janjua</b><br/>
Cybersecurity Student · SOC Analyst Aspirant
</p>

<p align="center">
Building practical hands-on skills in Cybersecurity · SOC Operations · Wazuh · SIEM · Blue Team Security · Threat Detection · Log Analysis · Incident Investigation · Threat Hunting · Detection Engineering
</p>

<p align="center">
  <a href="https://github.com/daniyal-sec">
    <img src="https://img.shields.io/badge/GitHub-daniyal--sec-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub"/>
  </a>
  <a href="https://github.com/daniyal-sec">
    <img src="https://img.shields.io/github/followers/daniyal-sec?style=for-the-badge&label=Follow&color=2C5364" alt="Follow"/>
  </a>
</p>

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1e3c72,50:2C5364,100:0F2027&height=120&section=footer" alt="footer"/>
</p>
