# Incident Documentation — RB-2502 SSH Authentication Failures

## Incident Metadata

* **Incident ID: 1786229309.20684**
* **Date / Time: Aug 9, 2026 @ 03:48:29.433**
* **Analyst: M ARSLAN**
* **Status: Escalated**
* **Severity: High**
* **Wazuh Rule: 2502**
* **Runbook: RB-2502-SSH-Authentication-Failures** 

## Alert

* **Alert Timestamp: Aug 9, 2026 @ 03:48:29.433**
* **Source IP: 	192.168.100.10**
* **Destination / Host: ubuntu**
* **Target Username: ubuntu**
* **Agent: 	192.168.56.101**
* **Alert Level: 10**
* **MITRE Technique: 	T1110**
* **Full Log: 	Aug 08 22:48:28 Ubuntu sshd-session[2788]: PAM 2 more authentication failures; logname= uid=0 euid=0 tty=ssh ruser= rhost=192.168.100.10  user=ubuntu**

## Information Collected

* **Authentication Attempts: multiple**

## Investigation

**Findings:**

**Multiple failed SSH authentication attempts against the Ubuntu account were detected. The activity is consistent with possible brute-force/password-guessing behavior. The user confirmed they did not initiate the attempts, so the activity was treated as suspicious and escalated to Tier 2.**
**Timeline:**

* Event occured: 03:48:29 —
* Triage Time:   03:50:11 —
* Escalation Time: 03:56:21 —

## Classification

* **Result: Suspecious Activity**
* **Reason: User confirmed NO ATTEMPT was made by him.**

## Containment

* **Action Taken: All Data related to event recorded and sent to Tier 2 for furthure investigation**

## Escalation

* **Escalated: Yes**
* **Reason: Unexpected/Unverified login attempts**
* **Escalated To: MR. ALI @ Tier 2**
* **Time: 03:56:21**

## Closure

* **Final Status: Under Investigation**
* **Summary: Unverified and Unknown failed login attempts on user UBUNTU account.**

