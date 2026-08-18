# Incident Documentation — RB-100011 Possible DoS Activity

## Incident Metadata

* **Incident ID: 1787015877.248316**
* **Date / Time: Aug 18, 2026 @ 06:17:57**
* **Analyst: Muhammad Arslan**
* **Status: Resolved**
* **Severity: Medium**
* **Wazuh Rule: 100011**
* **Runbook: RB-100011-Possible-DoS-Attack**
  
## Alert

* **Alert Timestamp: 06:17:57.132**
* **Source IP: 10.0.2.15**
* **Destination IP: 23.235.36.32**
* **Source Port: 44152**
* **Destination Port: 53**
* **Protocol: UDP**
* **pfSense Action: Pass**
* **Agent / Manager: 000**
* **Alert Level: 10**
* **MITRE Technique: T1498 — Network Denial of Service**
* **Full Log: "Aug 18 01:17:58 filterlog[46635]: 89,,,1000004761,em0,match,pass,out,4,0x0,,64,0,0,DF,17,udp,71,10.0.2.15,23.235.36.32,44152,53,51"**

## Information Collected

* **Detected Events: 21**
* **Detection Timeframe: under 30 seconds**
* **First Event: 06:17:40.081**
* **Last Event: 06:18:08.181**

## Investigation

**Findings:**

* Upon viewin source IP and Timestamps, It was assesed that this was an ethical and scheduled activity from Security Department. Therefor alert is being closed.


## Classification

* **Result: Authorized Activity**
* **Reason: Scheduled task by own security team.**

## Containment

* **Action Taken: none - alert closed**

## Escalation

* **Escalated: No**
* **Reason: No sign of any threat**

## Closure

* **Final Status: Resolved**
