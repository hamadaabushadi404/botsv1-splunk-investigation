# Attack Timeline

This file will be updated during the investigation to track the sequence of attacker activity.
Initial investigation started.
Searching for suspicious activity in BOTSv1 dataset.

### DNS Malformed Request Activity



An internal host (192.168.250.20) generated a high volume of malformed DNS requests targeting 192.168.250.100.



Total requests: 739



This behavior is suspicious and may indicate scanning activity or malware communication.


### Attacker Target Analysis

The attacker (192.168.250.20) communicated with multiple internal and external hosts.

Top targets include:
- 8.8.8.8 (external DNS) – 6444 requests
- 192.168.250.100 – 2362 requests
- 192.168.250.40 – 1472 requests

This behavior indicates possible DNS activity, internal scanning, and external communication.
