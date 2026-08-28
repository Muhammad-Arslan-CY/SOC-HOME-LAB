# Runbook — Possible DoS / High-Volume Network Activity

## 1. Metadata & Overview

**Purpose:** Investigate high-volume network traffic detected by pfSense and Wazuh.

**Scenario:** A large number of network packets/requests are generated from the same source and trigger a Wazuh DoS detection rule.

**Environment:** SOC Lab / pfSense / Wazuh

---

## 2. Trigger & Alert Information

**Wazuh Rule:** `100011`

**Level:** `10`

**Description:** Too many requests from same source. Possible DoS attack.

**Detection Pattern:** `Many events within few seconds`

**MITRE ATT&CK:** `T1498 — Network Denial of Service`

**Tactic:** `Impact`

**Groups:**

* `firewall`
* `pfsense`
* `network_security`
* `DoS`

---

## 3. Collect Information

Record the following from the Wazuh alert:

* Alert timestamp
* Source IP (`srcip`)
* Destination IP (`dstip`)
* Source port (`srcport`)
* Destination port (`dstport`)
* Protocol
* pfSense action — `pass` or `block`
* Agent/manager name
* Rule ID
* Alert level
* Full pfSense log
* Number of related alerts
* Related events from the same source IP

---

## 4. Investigate

Check:

1. Number of events detected by Wazuh.
2. Frequency of events over the detection timeframe.
3. Source IP generating the traffic.
4. Destination IP being targeted.
5. Destination port/service being targeted.
6. Protocol being used.
7. Whether pfSense is allowing or blocking the traffic.
8. Whether the traffic is coming from an authorized test system.
9. Whether other hosts/services are receiving similar traffic.
10. Whether there is any evidence of actual service degradation.

Record all relevant findings and evidence.

---

## 5. Decide

### False Positive / Authorized Testing

* Confirm the traffic was intentionally generated.
* Document the testing activity.
* Record the source and destination.
* Close the alert as authorized activity.

### Confirmed / Suspicious Activity

* Determine the scope and potential impact.
* Identify the affected service/host.
* Proceed to containment if authorized.
* Escalate according to the applicable incident procedure.

---

## 6. Containment

For confirmed unauthorized high-volume traffic in the lab:

* Block the identified source IP at pfSense.
* Verify that the block is active.
* Monitor whether the traffic decreases.
* Check whether the targeted service remains available.
* Record the containment action and timestamp.

For environments where the analyst does not have authorization to perform containment:

* Escalate to the authorized team.

---

## 7. Documentation

Record:

* Alert details
* Detection timestamp
* Source and destination
* Protocol and ports
* Traffic volume/frequency observed
* pfSense action
* Investigation timeline
* Evidence collected
* Findings
* Final classification
* Containment actions
* Escalation details, if applicable

### Future Prevention / Improvements

Record any prevention or detection improvements identified during the investigation, such as:

* Improved Wazuh frequency/timeframe thresholds
* More specific DoS detection rules
* Source/destination correlation
* pfSense firewall rules
* Rate limiting
* Dashboard improvements
* Additional network monitoring
* Baseline traffic measurements
