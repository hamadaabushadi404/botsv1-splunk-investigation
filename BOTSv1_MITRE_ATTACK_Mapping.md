# BOTSv1 Splunk Investigation – MITRE ATT&CK Mapping

> Note: This mapping is based on the evidence currently documented in this repository.
> It separates what is directly supported by observed evidence from what remains an analytical assessment.

---

## Scope of This Mapping
This project identified repeated suspicious DNS activity originating from **192.168.250.20** and targeting suspicious external domains, with **192.168.250.100** documented as the primary victim.

Observed highlights from the investigation:
- High volume of `SURICATA DNS malformed request data` alerts
- Repeated DNS queries to suspicious domains
- Analysis suggesting possible covert DNS-based communication

Because the current repository mainly documents **network/alert evidence**, the strongest ATT&CK mapping is under **Command and Control**. Exfiltration-related mapping is included as **assessed / suspected**, not confirmed.

---

## Confirmed / Strongly Supported Mapping

### 1) Command and Control
#### T1071.004 – Application Layer Protocol: DNS
**Why it fits:**
The investigation documented repeated DNS requests to suspicious external domains and concluded that the attacker appears to be abusing DNS as a communication channel.

**Evidence from this project:**
- Repeated DNS-related Suricata alerts
- Suspicious queried domains:
  - `hostby.guardomicro.com`
  - `ns3.isp4p.net`
  - `ns.kirov.ru`
  - `xantrox-server.de`
- Analysis describing likely DNS-based malicious communication

**Analyst note:**
This is the strongest ATT&CK mapping in the project and should be presented as the primary technique.

**Suggested wording for README:**
> The observed behavior is most strongly aligned with **MITRE ATT&CK T1071.004 (Application Layer Protocol: DNS)** because the attacker appears to have used DNS traffic as a covert communication mechanism.

---

## Assessed / Suspected Mapping

### 2) Exfiltration
#### T1041 – Exfiltration Over C2 Channel
**Why it may fit:**
If the DNS traffic was used not only for command-and-control but also to move data out of the environment through the same covert channel, T1041 may apply.

**Why this is not fully confirmed yet:**
The current project shows suspicious DNS communication, but it does not conclusively prove that actual stolen data was encoded and exfiltrated through that channel.

**How to present it safely:**
> The DNS activity may also indicate **possible T1041 (Exfiltration Over C2 Channel)** if the same covert DNS channel was used to transfer collected data outward. This remains an analytical assessment rather than a confirmed finding.

---

### 3) Exfiltration
#### T1048.003 – Exfiltration Over Unencrypted Non-C2 Protocol
**Why it may fit:**
If DNS was used as an alternate protocol specifically for data exfiltration outside the primary command-and-control channel, this technique can be relevant.

**Why this is lower confidence than T1071.004:**
The current evidence more clearly supports DNS-based communication than a distinct, proven exfiltration workflow over a separate non-C2 protocol.

**How to present it safely:**
> A lower-confidence mapping is **T1048.003 (Exfiltration Over Unencrypted Non-C2 Protocol)** if the attacker used DNS specifically as an alternate exfiltration path. Additional evidence would be needed to confirm this.

---

## Recommended Final ATT&CK Section for the Repository

## MITRE ATT&CK Mapping

### Confirmed / Strongly Supported
- **T1071.004 – Application Layer Protocol: DNS**  
  The attacker appears to have used DNS traffic as a covert communication channel, supported by repeated suspicious DNS queries and high-volume Suricata DNS alerts.

### Assessed / Suspected
- **T1041 – Exfiltration Over C2 Channel**  
  Possible if the same DNS channel was used to transfer stolen data outward.

- **T1048.003 – Exfiltration Over Unencrypted Non-C2 Protocol**  
  Possible if DNS was used as an alternate protocol for data exfiltration. This remains lower confidence based on the current evidence.

---

## Confidence Statement
- **High confidence:** T1071.004
- **Medium / low confidence:** T1041
- **Low confidence:** T1048.003

---

## Recommended Analyst Conclusion
The strongest ATT&CK-aligned conclusion from this investigation is that the attacker likely used **DNS-based communication** consistent with **T1071.004**. The evidence also raises the possibility of DNS-facilitated exfiltration, but that portion should be framed as a **suspected scenario**, not a fully confirmed fact.

---

## Optional Detection / Defensive Recommendations
- Baseline normal DNS behavior per host and detect high-frequency query anomalies
- Flag repeated DNS requests to rare, newly observed, or suspicious domains
- Correlate DNS alerts with endpoint telemetry and process execution
- Investigate hosts generating malformed or unusual DNS traffic patterns
- Monitor for unusually long queries, encoded subdomains, or beacon-like periodic behavior

---

## Short Version for Quick Copy/Paste
**MITRE ATT&CK Mapping:**
- **T1071.004 – Application Layer Protocol: DNS** *(strongly supported)*
- **T1041 – Exfiltration Over C2 Channel** *(possible / assessed)*
- **T1048.003 – Exfiltration Over Unencrypted Non-C2 Protocol** *(possible / lower confidence)*
