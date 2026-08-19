# Runbook — Multiple pfSense Firewall Blocks from Same Source

## 1. Metadata & Overview

**Purpose:** Investigate repeated connection attempts blocked by pfSense firewall rules from a single source IP.

**Scenario:** High-frequency port scan, sweep, or unauthorized connection attempts blocked at the perimeter firewall within a short timeframe.

**Environment:** SOC Lab / pfSense / Wazuh

---

## 2. Trigger & Alert Information

**Wazuh Rule:** `87702`

**Level:** `10`

**Description:** Multiple pfSense firewall blocks events from same source.

**Detection Pattern:** 18 or more dropped/blocked packets from the same source IP within 45 seconds.

**MITRE ATT&CK:** `T1110 — Brute Force` (and `T1046 — Network Service Discovery`)

**Tactic:** `Reconnaissance` / `Credential Access`

**Groups:** `multiple_blocks`, `pfsense`, `firewall_block`

---

## 3. Collect Information

Record the following from the Wazuh alert and raw logs:

* Alert timestamp & Incident ID
* Source IP (`srcip`)
* Destination IP (`dstip`)
* Targeted destination ports & protocol (TCP/UDP/ICMP)
* pfSense interface (`em0`, `em1`, `em2`, etc.)
* Total block events recorded in the window
* Suricata IDS alerts triggered concurrently from the same source IP

---

## 4. Investigate

Check:

1. Was the blocked traffic targeting specific sequential ports (port scan/discovery) or a single port (brute force)?
2. Did any packets from the same source IP bypass the firewall and receive a `pass` action?
3. Did Suricata trigger concurrent alerts (e.g., protocol anomalies, Nmap signatures)?
4. Is the source IP an internal lab component (authorized security testing) or external/unauthorized?
5. Did the target endpoint experience any disruption or compromise?

---

## 5. Decide

### Authorized Security Testing / False Positive
* Confirm the scan was scheduled/conducted by the internal lab analyst.
* Validate that firewall enforcement blocked the traffic as intended.
* Document and close as **Authorized Activity**.

### Confirmed Malicious / Suspicious Activity
* Identify the scan scope and verify firewall rules are holding.
* Add source IP to dynamic block table or blackhole routing if necessary.
* Escalate to Tier 2 if perimeter probes coincide with successful host logins.

---

## 6. Containment

* Ensure pfSense default drop/block rules remain active.
* If persistent, add temporary/permanent pfSense firewall alias rule to drop all traffic from the offending source IP at the external interface.
* Verify no state table entries exist for the attacker IP.

---

## 7. Documentation & Improvements

* Record full alert payload, timeline, and affected endpoints.
* Evaluate if threshold tuning (`frequency`/`timeframe`) is required.
* Check if Suricata inline IPS rules should be synchronized with firewall aliases.
