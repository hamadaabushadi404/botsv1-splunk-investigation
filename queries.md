# Splunk Queries Used in Investigation

---

## 1. Identify Available Data Sources

index=botsv1
| stats count by sourcetype

---

## 2. Identify Top Suricata Alerts

index=botsv1 sourcetype=suricata event_type=alert
| stats count by alert.signature
| sort -count

---

## 3. Identify Source of DNS Alerts

index=botsv1 sourcetype=suricata event_type=alert alert.signature="SURICATA DNS malformed request data"
| stats count by src_ip dest_ip
| sort -count

---

## 4. Identify Attacker Behavior

index=botsv1 src_ip=192.168.250.20
| stats count by dest_ip
| sort -count

---

## 5. Analyze Attacker Activity by Sourcetype

index=botsv1 src_ip=192.168.250.20
| stats count by sourcetype
| sort -count

---

## 6. Discover DNS Fields

index=botsv1 src_ip=192.168.250.20 sourcetype=stream:dns
| head 20
| fieldsummary

---

## 7. Extract DNS Queries (Domains)

index=botsv1 src_ip=192.168.250.20 sourcetype=stream:dns
| stats count by hostname{}
| sort -count

---

## 8. Identify Victim from Alerts

index=botsv1 src_ip=192.168.250.20 sourcetype=suricata event_type=alert
| stats count by dest_ip
| sort -count

---

## 9. Analyze Alerts Between Attacker and Victim

index=botsv1 src_ip=192.168.250.20 dest_ip=192.168.250.100 sourcetype=suricata event_type=alert
| stats count by alert.signature
| sort -count