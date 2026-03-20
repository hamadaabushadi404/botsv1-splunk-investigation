# Attack Timeline

---

1. Initial data exploration revealed multiple sourcetypes including Suricata and network stream logs.

2. Analysis of Suricata alerts showed a high number of DNS-related alerts.

3. Investigation identified attacker IP:
   192.168.250.20

4. Victim identification based on alert frequency:
   192.168.250.100

5. Additional host observed with high traffic:
   192.168.250.40 (not primary alert target)

6. Alert analysis revealed:
   - DNS malformed request data (739 events)
   - DNS unsolicited response (1 event)

7. DNS traffic analysis showed repeated queries to suspicious domains.

8. Identified suspicious domains:
   - hostby.guardomicro.com
   - ns3.isp4p.net
   - ns.kirov.ru
   - xantrox-server.de

9. Final conclusion:
   DNS protocol was used as a covert communication channel.