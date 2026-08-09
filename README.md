# Home-SOC-Lab
A hands-on Security Operations Center (SOC) lab featuring Windows logging, SIEM deployment, attack simulation, threat detection, and incident response.
# SIEM Incident Response Lab

## Overview

This project is a hands-on Security Information and Event Management (SIEM) lab designed to demonstrate practical SOC analyst and incident response workflows.

The lab uses Windows security telemetry collected from a controlled endpoint and analyzed using Splunk. Investigations focus on identifying notable security events, analyzing their context, correlating related activity, and determining whether observed behavior is benign, suspicious, or malicious.

The project follows an evidence-based investigation methodology rather than treating individual security events as automatically malicious.

### Investigation Workflow

```text
Detection
    ↓
Triage
    ↓
Investigation
    ↓
Correlation
    ↓
Analysis
    ↓
Classification
    ↓
Documentation
```

---

## Objectives

- Build and operate a functional SIEM environment.
- Collect and analyze Windows Security Event Logs.
- Use Splunk to search and investigate security telemetry.
- Identify notable authentication and account-related events.
- Investigate processes associated with security events.
- Correlate accounts, processes, timestamps, hosts, and event IDs.
- Distinguish legitimate system/software activity from potentially suspicious activity.
- Collect and preserve investigation evidence.
- Produce professional SOC-style investigation reports.

---

## Lab Environment

| Component | Purpose |
|---|---|
| Windows 10 | Endpoint generating security telemetry |
| Splunk | SIEM and log analysis platform |
| Windows Security Event Log | Primary security telemetry |
| Sysmon | Additional endpoint telemetry |
| Kali Linux | SIEM analysis environment |
| VirtualBox | Virtualization platform |

---

## Data Flow

```text
Windows Endpoint
       |
       | Windows Security Events
       v
   Log Collection
       |
       v
     Splunk
       |
       | SPL Queries
       v
Detection & Investigation
       |
       v
Evidence Collection
       |
       v
Investigation Reports
```

---

## Splunk Data Source

Windows event data is indexed in Splunk using:

```text
index=wineventlog
```

The project uses Windows Security Event IDs and associated fields to identify and investigate notable activity.

---

## Investigation Methodology

Each investigation follows a consistent SOC investigation process.

### 1. Detection

Identify an event or activity that warrants further investigation.

### 2. Triage

Determine whether the event is worth investigating by reviewing its frequency, context, affected account, host, process, and related activity.

### 3. Investigation

Review the available event fields, including:

- Event ID
- Timestamp
- Account name
- Computer name
- Logon type
- Process name
- Process ID
- Source address
- Event status
- Event message
- Security ID

### 4. Correlation

Compare related events using:

- Account
- Host
- Process
- Timestamp
- Event ID
- Source information

### 5. Analysis

Determine whether the observed activity is consistent with:

- Normal system activity
- Legitimate software activity
- Administrative activity
- Suspicious activity
- Potential malicious activity

### 6. Classification

The investigation is assigned a final classification based on the available evidence.

### 7. Documentation

Relevant evidence and analyst conclusions are documented in an individual investigation directory.

---

## Investigations

| Investigation | Event ID | Classification | Status |
|---|---:|---|---|
| Local Group Membership Enumeration | 4798 | Likely Benign | Completed |
| Failed Logon Investigation | 4625 | Under Investigation | Pending |
| Additional Security Event Investigations | — | — | Pending |

---

## Current Findings

### Event ID 4798 — Local Group Membership Enumeration

Event ID 4798 was observed repeatedly on the Windows endpoint.

Investigation identified the process responsible for the activity as:

```text
C:\Program Files (x86)\IObit\Advanced SystemCare\smBootTime.exe
```

The event indicated that local group membership was enumerated and was associated with the installed IObit Advanced SystemCare software.

The activity was assessed as **likely benign** based on the available process and event context.

Full investigation details and supporting evidence are available in:

```text
investigations/event-4798-group-membership-enumeration/
```

---

## Skills Demonstrated

- SIEM administration
- Splunk
- Splunk Search Processing Language (SPL)
- Windows Event Log analysis
- Windows Security Event ID analysis
- Security event triage
- Authentication analysis
- Account activity investigation
- Process correlation
- Timeline analysis
- False-positive identification
- Evidence collection
- SOC investigation methodology
- Incident documentation

---

## Key Lessons

Security events must be evaluated in context.

An event associated with account enumeration may initially appear suspicious because similar behavior can occur during reconnaissance. However, examining the responsible process, executable path, account, host, timestamp, and surrounding activity can provide important context.

This project demonstrates the importance of:

> **Investigating the evidence before assigning a verdict.**

---

## Repository Structure

```text
SIEM-Incident-Response-Lab/
│
├── README.md
│
└── investigations/
    │
    ├── event-4798-group-membership-enumeration/
    │   ├── README.md
    │   └── evidence/
    │       └── event-4798-expanded.png
    │
    └── event-4625-failed-logon/
        ├── README.md
        └── evidence/
```

Additional investigations will be added as they are completed.

---

## Evidence

Screenshots and other supporting evidence are stored within the corresponding investigation directory.

Evidence is collected directly from the lab's Splunk environment and is used to support the conclusions documented in each investigation.

---

## Disclaimer

This project was conducted in a controlled laboratory environment for educational and portfolio purposes.

The systems, accounts, events, and telemetry analyzed in this repository belong to the controlled lab environment used for the project.
