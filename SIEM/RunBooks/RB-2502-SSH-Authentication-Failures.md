# Runbook — SSH Authentication Failures

## 1. Metadata & Overview

**Purpose:** Investigate repeated SSH authentication failures detected on a monitored host.

**Scenario:** Multiple failed SSH authentication attempts against an account.

**Environment:** SOC Lab / Wazuh / Ubuntu

---

## 2. Trigger & Alert Information

**Wazuh Rule:** `2502`

**Level:** `10`

**Description:** User missed the password more than one time

**MITRE ATT&CK:** `T1110 — Brute Force`

**Tactic:** `Credential Access`

**Groups:** `authentication_failed`, `access_control`

**Relevant mappings:**

* PCI DSS: `10.2.4, 10.2.5`
* NIST 800-53: `AU.14, AC.7`
* HIPAA: `164.312.b`
* GDPR: `IV_35.7.d, IV_32.2`

---

## 3. Collect Information

Record the following from the Wazuh alert:

* Alert timestamp
* Source IP (`srcip`)
* Destination/target host
* Target username (`dstuser`)
* Agent name and IP
* Rule ID
* Alert level
* Full log
* Related alerts from the same source IP

---

## 4. Investigate

Check:

1. Number and frequency of failed authentication attempts.
2. Source IP associated with the attempts.
3. Target account.
4. Authentication timestamps.
5. Related SSH events.
6. Other Wazuh alerts from the same source IP.
7. Whether authentication eventually succeeded.
8. Activity following any successful authentication.
9. Whether the source is authorized or expected.

Record all relevant findings and evidence.

---

## 5. Decide

### False Positive / Benign

* Document the reason.
* Close the alert.

### Confirmed / Suspicious Activity

* Proceed to containment.
* Escalate according to the applicable incident procedure.

---

## 6. Containment

For confirmed unauthorized SSH activity in the lab:

* Block the identified source IP from SSH access.
* Verify the block is active.
* Record the containment action and timestamp.

For environments where the analyst does not have authorization to perform containment:

* Escalate to the authorized team.

---

## 7. Documentation

Record:

* Alert details
* Investigation timeline
* Evidence collected
* Findings
* Final classification
* Containment actions
* Escalation details, if applicable

### Future Prevention / Improvements

Record any prevention or detection improvements identified during the investigation, such as:

* Additional Wazuh rules
* Improved alert thresholds
* Dashboard improvements
* SSH hardening
* Additional monitoring requirements
