# Runbook — Multiple Suricata Stream Established SYN-ACK Resends from Same Source

## 1. Metadata & Overview

**Purpose:** Investigate high-frequency TCP stream anomalies where repeated SYN-ACK packets target active or closing connections from a single source IP.

**Scenario:** Stateless TCP flood, crafted packet injection, or state table exhaustion attempt targeting endpoint listening services.

**Environment:** SOC Lab / Ubuntu Endpoint / Suricata NIDS / Wazuh SIEM

---

## 2. Trigger & Alert Information

**Wazuh Rule:** `100015`

**Level:** `8`

**Description:** Multiple SURICATA STREAM ESTABLISHED SYNACK resends from same IP.

**Parent Rule:** `100013` (Base Level 1 alert for Suricata SID `2210022`)

**Detection Pattern:** 10 or more `2210022` events from the same `src_ip` within 10 seconds (`ignore="30"` active).

**MITRE ATT&CK:** `T1498.001 — Direct Network Flood` (and `T1498 — Network Denial of Service`)

**Tactic:** `Impact`

**Groups:** `suricata`, `soc_lab_scan`, `dos`

---

## 3. Collect Information

Record the following from the Wazuh alert and raw telemetry:

* Alert Timestamp & Incident ID
* Attacker Source IP (`data.src_ip`)
* Attacker Source Port (`data.src_port`)
* Target Destination IP (`data.dest_ip`)
* Target Destination Port (`data.dest_port`)
* Protocol (`TCP`) & Flags (`SYN-ACK`)
* Agent Name / ID (`agent.name`, `agent.id`)
* Active Response execution logs (`firewall-drop` execution on endpoint)
* Target host system health (CPU, Memory, Packet drop counters)

---

## 4. Investigate

Check:

1. **Traffic Velocity & Pattern:** Did the source generate high-velocity bursts targeting a single active service port or sweep across multiple endpoints?
2. **Protocol Legitimacy:** Was the session genuinely established prior to the resends, or are raw-crafted packets forcing out-of-order state transitions?
3. **Target Impact:** Did the targeted service (e.g., Web, SSH, DB) experience connection drops, socket saturation (`SYN_RECV` backlog), or process crashes?
4. **Correlated Security Events:**
* Did the source IP trigger concurrent UFW block rules (`100010`, `100011`)?
* Did Suricata trigger related stream rules (e.g., `2210023`, `2210008`) or custom DoS rules (`1000002` / `86601`)?


5. **Source Classification:** Is the source an authorized internal testing node (e.g., Kali Linux lab VM) conducting flood simulations, or an unknown/unauthorized address?
6. **Automated Containment Validation:** Verify if the Wazuh Active Response engine successfully executed `firewall-drop` on the agent for the offending source IP.

---

## 5. Decide

### Authorized Testing / Simulation

* Confirm the scan/flood was initiated by an authorized analyst or scheduled lab simulation.
* Verify detection rules and automated Active Response behaved as expected.
* Document findings and close as **Authorized Activity**.

### Confirmed Malicious / Hostile Flood

* Confirm sustained abnormal stream manipulation targeting production services.
* Validate that automated Active Response dropped the IP, or escalate if traffic bypasses controls.
* Close as **True Positive — Denial of Service Attempt**.

### False Positive / Asymmetric Routing

* Check for network asymmetry, MTU misconfigurations, or aggressive proxy load balancing causing legitimate session retries.
* Adjust threshold parameters if legitimate high-concurrency traffic routinely breaches the 10-packet window.

---

## 6. Automated Containment Verification

* Check Wazuh Manager active response logs:
* Look for `active-response/bin/firewall-drop` execution against `<SRC_IP>`.


* Verify endpoint firewall state:
* Run `sudo ufw status numbered` or `sudo iptables -L -n -v` to ensure the drop rule is actively matching.


* Confirm TCP state table clearance:
* Verify stale sockets have dropped and listener backlog is healthy (`ss -tan state syn-recv`).



---

## 7. Documentation & Review

* Log incident details, attack timeline, total suppressed volume, and impact metrics.
* Review if the 30-second cooldown (`ignore="30"`) adequately shielded the SIEM from queue congestion during the peak attack window.

---
