# Splunk Queries Used During Investigation

This file will contain the Splunk queries used during the investigation.



### Top Attacks



index=botsv1 sourcetype=suricata event\_type=alert

| stats count by alert.signature

| sort -count



Used to identify the most frequent attack types in the dataset.





### DNS Attack Source Identification



index=botsv1 sourcetype=suricata event\_type=alert alert.signature="SURICATA DNS malformed request data"

| stats count by src\_ip dest\_ip

| sort -count

Used to identify attacker and victim IPs.


index=botsv1 src_ip=192.168.250.20

