# Splunk Intrusion Detection & Alert Analysis

## Project Overview

This project demonstrates the use of **Splunk SIEM** to monitor and analyze **Suricata IDS alerts** using the Splunk BOTS v2 dataset.

The analysis focuses on intrusion alerts, alert severity, intrusion signatures, and whether suspicious traffic was allowed or blocked.

## Tools & Technologies

- Splunk Enterprise
- Splunk Search Processing Language (SPL)
- Suricata IDS
- BOTS v2 Dataset
- SIEM & SOC Monitoring

## Objectives

- Analyze Suricata intrusion detection alerts.
- Monitor allowed and blocked intrusion traffic.
- Identify medium-severity intrusion activity.
- Analyze frequently triggered intrusion signatures.
- Examine intrusion alerts based on severity.
- Practice SOC alert monitoring and investigation using Splunk.

## SPL Queries

### 1. Allowed Intrusion Traffic

```spl
index=botsv2 sourcetype=suricata alert.action=allowed alert.signature=*
| stats count(alert.signature)
```

### 2. Medium-Severity Intrusion Traffic

```spl
index=botsv2 sourcetype=suricata alert.severity=2 alert.signature=*
| stats count(alert.severity)
```

### 3. Blocked Intrusion Traffic

```spl
index=botsv2 sourcetype=suricata alert.action=blocked alert.signature=*
| stats count(alert.signature)
```

### 4. Intrusion Signatures

```spl
index=botsv2 sourcetype=suricata alert.signature=*
| stats count by alert.signature
```

### 5. Intrusion Alerts by Severity

```spl
index=botsv2 sourcetype=suricata alert.signature=* alert.severity=*
| stats count by alert.signature alert.severity
```

## SOC Skills Demonstrated

- SIEM monitoring with Splunk
- SPL query development
- IDS alert analysis
- Suricata log analysis
- Intrusion signature analysis
- Security alert triage
- Severity-based investigation
- Allowed vs blocked traffic analysis
- Security event monitoring

## Investigation Workflow

```text
Suricata IDS Alerts
        ↓
    Splunk SIEM
        ↓
     SPL Queries
        ↓
Alert Filtering & Analysis
        ↓
Signature & Severity Analysis
        ↓
SOC Investigation
```

## Key Analysis Areas

| Analysis | Purpose |
|---|---|
| Allowed Intrusion Traffic | Identify alerts where suspicious traffic was allowed |
| Medium-Severity Traffic | Monitor moderate-severity intrusion activity |
| Blocked Intrusion Traffic | Identify prevented intrusion attempts |
| Intrusion Signatures | Determine frequently triggered signatures |
| Alerts by Severity | Prioritize and analyze security alerts |

## Dataset

This project uses the **Splunk BOTS v2 (Boss of the SOC v2)** dataset and Suricata IDS logs for educational security monitoring and analysis.

## Disclaimer

This is an educational cybersecurity project created to demonstrate practical SOC analyst and SIEM monitoring skills using a controlled dataset.

## Author

**Rajendra Parasad D**

Cybersecurity / SOC Analyst Portfolio Project
