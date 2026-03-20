# BOTSv1 Splunk Investigation

## Overview
This project documents a SOC investigation using the BOTSv1 dataset in Splunk.  
The objective was to detect suspicious activity, identify attacker and victim systems, and analyze the attack behavior.

---

## Tools Used
- Splunk (Log Analysis)
- Suricata (IDS Alerts)
- Wireshark (Network Analysis)
- BOTSv1 Dataset

---

## Identified Entities

**Attacker:**  
192.168.250.20

**Primary Victim:**  
192.168.250.100

**Observed Host (High Traffic):**  
192.168.250.40  
*(Generated high traffic but was not the primary alert target)*

---

## Investigation Steps

1. Explored available data sources and identified key sourcetypes.
2. Focused on Suricata alerts to detect abnormal behavior.
3. Identified high volume of DNS-related alerts.
4. Determined attacker and victim based on source and destination analysis.
5. Investigated communication patterns between systems.
6. Extracted DNS queries used by the attacker.
7. Identified suspicious domains involved in the activity.

---

## Key Findings

- High volume of DNS alerts:
  - SURICATA DNS malformed request data (739 events)
  - SURICATA DNS unsolicited response (1 event)

- Repeated DNS queries to suspicious domains:
  - hostby.guardomicro.com
  - ns3.isp4p.net
  - ns.kirov.ru
  - xantrox-server.de

- DNS activity frequency was abnormally high and not consistent with normal user behavior.

---

## Analysis

The attacker (192.168.250.20) abused the DNS protocol as a communication channel.

The high frequency of DNS queries, combined with unusual domain names, strongly suggests:

- DNS tunneling
- Command-and-Control (C2) communication
- Possible data exfiltration over DNS

This technique is commonly used by malware to evade detection, as DNS traffic is typically allowed in most networks.

---

## Conclusion

The investigation indicates that the attacker leveraged DNS-based communication to interact with external infrastructure.

This behavior strongly suggests malicious activity using covert communication channels, likely for data exfiltration or remote control.

---

## Skills Demonstrated

- Log Analysis using Splunk
- Threat Detection & Investigation
- Network Traffic Analysis
- Identifying Attacker & Victim
- IOC Extraction
- Understanding DNS-based Attacks