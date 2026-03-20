# BOTSv1 Splunk Investigation

This project documents a security investigation using the BOTSv1 dataset in Splunk to identify suspicious activity, track attacker behavior, and extract indicators of compromise (IOCs).

## Tools Used
- Splunk
- BOTSv1 Dataset
- Wireshark

# BOTSv1 Splunk Investigation

## Overview
This project documents a SOC investigation using the BOTSv1 dataset in Splunk.  
The goal was to identify suspicious activity, determine the attacker and victim, and analyze the attack behavior.

---

## Identified Entities

Attacker:
192.168.250.20

Primary Victim:
192.168.250.100

Other Observed Host:
192.168.250.40 (high traffic but not primary alert target)

---

## Investigation Steps

1. Identified active sourcetypes and focused on Suricata alerts.
2. Detected abnormal alert patterns involving DNS activity.
3. Confirmed attacker IP generating large number of events.
4. Determined the primary victim based on alert distribution.
5. Analyzed alert types and identified DNS malformed requests.
6. Investigated DNS traffic to extract queried domains.

---

## Key Findings

- High volume of DNS-related alerts detected:
  - SURICATA DNS malformed request data (739 events)
  - SURICATA DNS unsolicited response (1 event)

- Attacker generated repeated DNS requests to suspicious domains:
  - hostby.guardomicro.com
  - ns3.isp4p.net
  - ns.kirov.ru
  - xantrox-server.de

- DNS activity frequency was abnormally high and not consistent with normal user behavior.

---

## Analysis

The attacker (192.168.250.20) appears to be abusing the DNS protocol as a communication channel.

The high frequency of DNS queries, combined with unusual domain names, suggests:

- Possible DNS tunneling
- Potential command-and-control (C2) communication
- Possible data exfiltration over DNS

This behavior is commonly used by malware to evade detection, as DNS traffic is often allowed in most networks.

---

## Conclusion

The investigation indicates that the attacker leveraged DNS-based communication to interact with external infrastructure.

This activity strongly suggests malicious behavior involving covert communication channels, likely for data exfiltration or remote control.

---

## Tools Used

- Splunk (Log Analysis)
- Suricata (IDS Alerts)
- BOTSv1 Dataset

---

## Skills Demonstrated

- Log analysis and threat detection
- Splunk SPL querying
- Network traffic analysis
- Identifying attacker and victim
- IOC extraction
- Understanding DNS-based attacks

---