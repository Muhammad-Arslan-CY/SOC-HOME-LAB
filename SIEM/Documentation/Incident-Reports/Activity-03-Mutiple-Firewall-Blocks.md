# Incident Documentation — RB-87702 Multiple pfSense Firewall Blocks

## Incident Metadata

* **Incident ID: 1787101253.39577**
* **Date / Time: Aug 19, 2026 @ 06:00:53.634**
* **Analyst: M. Arslan**
* **Status: Escalated**
* **Severity: High** 
* **Wazuh Rule:87702** 
* **Runbook:RB-87702-pfSense-Multiple-Firewall-Blocks** 

## Alert

* **Alert Timestamp: Aug 19, 2026 @ 06:00:53.634**
* **Source IP: 192.168.20.10**
* **Destination IP: 192.168.10.10**
* **Source Port: 61010**
* **Destination Port: 22**
* **Protocol: TCP**
* **pfSense Action: Block** 
* **Agent / Host: 002**
* **Alert Level: 10** 
* **MITRE Technique: T1110 / T1046**
* **Full Log: 2026-08-19T06:00:53+00:00 192.168.56.100 filterlog[51409]: 4,,,1000000103,em2,match,block,in,4,0x0,,38,58519,0,DF,6,tcp,60,192.168.20.10,192.168.10.10,61010,22,0,A,,3583945624,1024,,wscale;nop;mss;TS;sackOK**

## Investigation

**Findings:**

* There was no scheduled activity by anyone in security department at this time or these IPs
* The activity appears suspicious and unauthorized scans or data packets flooded on destination ip 192.168.10.10.
* It may belong to a serious incident like possible DoS attempt or Brute-Force.

**Timeline:**

* Aug 19, 2026 @ 06:00:53.634 

## Classification

* **Result: Suspicious Activity** 
* **Reason: No Scheduled**

## Containment

* **Action Taken: Escalated**
* **Source IP / Target: 192.168.20.10 > 192.168.10.10**
* **Result: In progress**

## Escalation

* **Escalated: Yes**
* **Reason: Suspicious Activity. Possibilities of DoS or Brute-force**
* **Escalated To: Tier 2 Analyst, Mr. Arslan Jr.**
* **Time: 8/19/2026 6:33 AM**

## Closure

* **Final Status: under investigation**
* **Summary: There was so scheduled or authorized activity from given source IP. Suspicious Activity may belong to a serious event like DoS attempt or Brute-Force**
