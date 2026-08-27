# Splunk Firewall Monitoring & Traffic Analysis

## Project Overview

This project demonstrates a **Splunk-based Firewall Monitoring and
Traffic Analysis dashboard** using the **Splunk BOTS v2 dataset** and
Palo Alto firewall (`pan:traffic`) logs.

The dashboard provides visibility into firewall activity, including
allowed and blocked traffic, external source and destination IPs,
traffic trends, network protocols, and blocked/non-allowed destination
activity.

## Objectives

-   Monitor firewall traffic using Splunk.
-   Analyze allowed and blocked firewall actions.
-   Identify external source and destination IP addresses.
-   Visualize firewall activity over time.
-   Analyze traffic by network protocol.
-   Investigate non-allowed traffic and destination locations.
-   Practice SPL-based security monitoring and investigation.

## Tools & Technologies

-   **Splunk Enterprise**
-   **Splunk Search Processing Language (SPL)**
-   **BOTS v2 Dataset**
-   **Palo Alto Firewall Logs (`pan:traffic`)**
-   **Security Operations / SOC Monitoring Concepts**

## Dashboard

### Firewall Monitoring Dashboard

The dashboard contains the following panels:

1.  Firewall Blocked Traffic
2.  Firewall Allowed Traffic
3.  External Source IPs
4.  External Destination IPs
5.  Traffic Actions Over Time
6.  Traffic by Protocol
7.  Blocked Traffic Destination Location

## SPL Queries

### 1. Firewall Blocked Traffic

``` spl
index="botsv2" sourcetype="pan:traffic" action=blocked
| stats count(action)
```

Counts firewall events where the action is `blocked`.

### 2. Firewall Allowed Traffic

``` spl
index="botsv2" sourcetype="pan:traffic" action=allowed
| stats count(action)
```

Counts firewall events where the action is `allowed`.

### 3. External Source IPs

``` spl
index=botsv2 sourcetype="pan:traffic"
NOT(src_ip=10.0.0.0/18 OR src_ip=192.168.0.0/16 OR src_ip=172.16.0.0/12)
| stats dc(src_ip)
```

Counts distinct source IP addresses after excluding the specified
private IP ranges.

### 4. External Destination IPs

``` spl
index=botsv2 sourcetype="pan:traffic"
NOT(dest_ip=10.0.0.0/18 OR dest_ip=192.168.0.0/16 OR dest_ip=172.16.0.0/12)
| stats dc(dest_ip)
```

Counts distinct destination IP addresses after excluding the specified
private IP ranges.

### 5. Traffic Actions Over Time

``` spl
index=botsv2 sourcetype="pan:traffic"
| fields action
| timechart count by action
```

Visualizes firewall actions over time and helps identify changes or
spikes in traffic activity.

### 6. Traffic by Protocol

``` spl
index=botsv2 sourcetype="pan:traffic"
| fields transport
| timechart span=600s count by transport
```

Visualizes network traffic by transport protocol over time.

### 7. Blocked / Non-Allowed Traffic Destination Analysis

``` spl
index=botsv2 sourcetype="pan:traffic" dest_ip!="" dest_location!="" action!="allowed"
| stats count as connections by dest_location dest_ip action
| sort - connections
```

Identifies non-allowed traffic and provides the destination location,
destination IP, firewall action, and connection count for investigation.

## Key SOC Skills Demonstrated

-   SIEM monitoring with Splunk
-   SPL query development
-   Firewall log analysis
-   Source and destination IP analysis
-   Network traffic analysis
-   Protocol monitoring
-   Security event visualization
-   Identification of blocked/non-allowed traffic
-   Basic security investigation and triage

## Project Workflow

``` text
Palo Alto Firewall Logs
        ↓
     Splunk SIEM
        ↓
      SPL Queries
        ↓
Traffic Analysis & Filtering
        ↓
Dashboard Visualization
        ↓
Security Monitoring & Investigation
```

## Screenshots

Dashboard screenshots are included in this repository to demonstrate the
implemented Splunk panels and analysis results.

## Dataset

This project uses the **Splunk BOTS v2 (Boss of the SOC v2)** dataset
for hands-on security monitoring and analysis.

## Disclaimer

This is an educational/lab project created for practicing SOC analyst
and SIEM monitoring skills. The analysis is based on the provided BOTS
v2 dataset and does not represent a production security environment.

## Author

**Rajendra Prasad D **

Cybersecurity / SOC Analyst Portfolio Project
