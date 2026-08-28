# Incident Documentation — RB-100033 Established Invalid ACK

## Incident Metadata

* **Incident ID:**
* **Date / Time:**
* **Analyst:**
* **Status:** Open / In Progress / Closed
* **Severity:** High (Level 8)
* **Wazuh Rule:** 100033
* **Runbook:** RB-100033-Suricata-Stream-Established-Invalid-ACK

## Alert

* **Alert Timestamp:**
* **Source IP:**
* **Source Port:**
* **Destination IP:**
* **Destination Port:**
* **Protocol:** TCP
* **Suricata SID:** 2210029
* **Agent / Host:**
* **Alert Level:** 8
* **MITRE Technique:** T1498.001
* **Full Log:**

## Information Collected

* **Detected Events in Window:**
* **Detection Timeframe:**
* **First Event Timestamp:**
* **Last Event Timestamp:**
* **Related Suricata Stream SIDs:**
* **Correlated Firewall Logs (`[UFW BLOCK]`):**
* **Target Endpoint Impact:** None / Resource Pressure / Service Interruption

## Investigation

**Findings:**

**Timeline:**

* `[TIME]` —
* `[TIME]` —
* `[TIME]` —

## Classification

* **Result:** Authorized Activity / True Positive / False Positive
* **Reason:**

## Automated Containment Check

* **Active Response Triggered:** Yes / No
* **Action Executed:** `firewall-drop` (UFW / iptables)
* **Source IP Block Verified:** Yes / No
* **Socket State Cleared:** Yes / No

## Escalation

* **Escalated:** Yes / No
* **Reason:**
* **Escalated To:**
* **Time:**

## Closure

* **Final Status:** Resolved / Closed
* **Summary:**

## Evidence

* Wazuh Level 8 Alert JSON:
* Suricata `eve.json` Stream Events:
* Active Response Execution Log:
* Endpoint `iptables` / `ufw` Block Verification:
