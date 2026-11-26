# Oil & Gas SOC — Cyber Attack Detection & Analysis

A Splunk-based Security Operations Center (SOC) detection-engineering project focused on cyber threats across **IT, OT and IT/OT DMZ environments** in oil and gas facilities.

**Author:** Akram Al-Bayati  
**Date:** November 2026  
**Platform:** Splunk Enterprise  
**Primary frameworks:** MITRE ATT&CK Enterprise and MITRE ATT&CK for ICS  
**Splunk index:** `oil_gas_soc`

---

## Project Overview

This project demonstrates how security telemetry from industrial environments can be investigated and correlated to identify attacks that may affect both enterprise systems and physical operations.

The lab contains **27,048 security events** covering four facilities. Fourteen SPL detections were engineered across eight planted incident scenarios, mapped to MITRE ATT&CK, and presented through an **Oil & Gas Cyber Defense Command Center** dashboard.

The analysis combines traditional IT security events with OT process telemetry, including pressure, temperature, flow and valve-position values. This makes it possible to connect suspicious cyber activity with potential operational consequences.

## Project at a Glance

| Item | Details |
|---|---|
| Security events | 27,048 |
| SPL detections | 14 |
| Attack scenarios | 8 (`OIL-IR-001` to `OIL-IR-008`) |
| Facilities | 4 |
| Monitored assets | 14 |
| Date range | 1–30 October 2026 |
| Network zones | `IT`, `OT`, `IT_OT_DMZ` |
| Splunk index | `oil_gas_soc` |

### Facilities

- ZUBAIR-REFINERY
- RUMAILA-OPS
- BASRA-PROD
- FAO-PIPELINE

### Telemetry and Assets

The dataset represents activity from systems such as:

- Active Directory / domain controller
- VPN gateway and OT jump server
- Engineering workstation
- PLCs and HMIs
- Historian
- Firewall and DNS
- File and camera servers

Event categories include authentication, VPN, RDP, process execution, DNS, network connections, USB and file activity, alongside OT process measurements.

## Detection Coverage

The project contains 14 detections grouped into eight incident scenarios.

| ID | Detection | Scenario |
|---|---|---|
| D01 | Brute-Force Authentication Attempts | `OIL-IR-001` |
| D02 | Successful Logon After Brute Force | `OIL-IR-001` |
| D03 | Vendor VPN Login Outside Maintenance Window | `OIL-IR-002` |
| D04 | Remote Desktop Session to the OT Jump Server | `OIL-IR-002` |
| D05 | Encoded PowerShell on an Engineering Workstation | `OIL-IR-003` |
| D06 | OT Network Scan from the Engineering Workstation | `OIL-IR-003` |
| D07 | DNS Query to a Suspicious External Domain | `OIL-IR-003` |
| D08 | Unauthorised Modbus Write to a PLC | `OIL-IR-004` |
| D09 | Critical High-Pressure Alarm | `OIL-IR-004` |
| D10 | Large Outbound Transfer from the Historian | `OIL-IR-005` |
| D11 | Periodic DNS Beaconing | `OIL-IR-006` |
| D12 | USB Device on an OT Engineering Workstation | `OIL-IR-007` |
| D13 | Configuration Files Copied to Removable Media | `OIL-IR-007` |
| D14 | Blocked IT-to-OT Connection Attempt | `OIL-IR-008` |

Detections are mapped to relevant MITRE ATT&CK Enterprise and ICS techniques. The report includes the SPL logic, observed evidence, analyst assessment and recommended response for each detection.

## SOC Dashboard

The **Oil & Gas Cyber Defense Command Center** brings the analysis into a single operational view.

Dashboard coverage includes:

- Overall security KPIs and event timeline
- Severity and event-category breakdowns
- Facility and network-zone visibility
- OT process monitoring and critical commands
- Monitored asset inventory
- Protocol and authentication activity
- MITRE ATT&CK coverage
- Incident-scenario validation

## Investigation and Correlation

The project does not treat every alert as an isolated event. Related detections are correlated into attack chains to help explain how activity can progress across IT and OT.

A key example in the report links an unauthorised Modbus write to a PLC with a critical high-pressure alarm. This demonstrates why OT security monitoring should consider both cyber events and the state of the industrial process.

## Methodology

The workflow followed these stages:

1. Define the attack scenario and the expected observable behaviour.
2. Identify the relevant telemetry and fields.
3. Develop the SPL detection logic.
4. Execute and inspect the search results in Splunk.
5. Map the detection to MITRE ATT&CK and assign severity.
6. Review related events and correlate the scenario.
7. Present the results and supporting evidence in the dashboard.

Claude and ChatGPT were used as analytical assistants for query drafting, refinement, interpretation, MITRE mapping and documentation. The searches were executed and checked by the analyst in Splunk.

## Running the Project

This repository's accompanying project files should be used with a Splunk Enterprise environment.

1. Prepare the project dataset and ensure its event fields are preserved.
2. Ingest the events into the Splunk index named `oil_gas_soc`.
3. Open **Search & Reporting** and select an appropriate time range covering October 2026 (or use All time for the complete lab dataset).
4. Run the SPL detections against `index=oil_gas_soc`.
5. Import or recreate the dashboard in Splunk, ensuring its searches use the same index and field names.
6. Compare the returned events with the evidence and scenario analysis in the project report.

> **Important:** The README documents the environment and analysis described in the report. It does not imply that dataset files, dashboard XML, or saved-search exports are included in this repository unless they are added separately.

## Key Outcomes

- Fourteen SPL detections were used to identify all eight planted scenarios in the controlled dataset.
- IT and OT telemetry were analysed together rather than as separate security domains.
- MITRE ATT&CK Enterprise and ICS mappings provide a structured view of detection coverage.
- Dashboard visualisations and cross-scenario correlation help analysts move from high-level indicators to supporting evidence.

## Limitations and Future Work

The dataset is controlled and simulated, with labelled scenarios. Detection thresholds and results must therefore be re-baselined before use in a production environment.

Potential next steps identified in the report:

- Convert searches into scheduled Splunk alerts with risk-based scoring.
- Add protocol-aware monitoring for Modbus and OPC UA.
- Integrate SOAR playbooks for response automation.
- Add UEBA-style baselines for service accounts.
- Extend correlation into a MITRE ATT&CK for ICS coverage heatmap.

## Disclaimer

This is a defensive cybersecurity lab and portfolio project. The dataset represents a controlled simulation and should not be interpreted as telemetry from real oil and gas facilities. Detection logic must be tested, tuned and approved before operational deployment.

---

**Author:** Akram Al-Bayati  
**Focus:** SOC Analysis · Detection Engineering · Splunk SPL · MITRE ATT&CK · ICS/OT Security
