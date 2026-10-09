# Custom Suricata Rules

## Overview
Custom Suricata signatures for common lab attack patterns. Alerts are
collected by the Wazuh agent and shown in the Wazuh dashboard.

## Rules
| SID | Detects | Logic |
|-----|---------|-------|
| 1000005 | ICMP ping sweep | 10 ICMP packets from one source in 5 s |
| 1000002 | Port scan / rapid connections | 30 SYN packets from one source in 3 s |
| 1000003 | Possible SSH brute force | 5 packets to port 22 from one source in 60 s |
| 1000004 | Slowloris-style connection rate | 20 SYN packets to port 80 from one source in 10 s |
| 1000020 | hping3 ICMP flood | 10 ICMP echo requests with a marker string in 3 s |
| 1000021 | nping ICMP flood | 10 ICMP echo requests with a marker string in 3 s |

Full rule file: [rules/local.rules](../rules/local.rules)

## Loading the rules
1. Save the rules to `/etc/suricata/rules/local.rules`.
2. Make sure the file is listed under `rule-files:` in `/etc/suricata/suricata.yaml`:
```yaml
   rule-files:
     - local.rules
```
3. Validate the configuration and restart Suricata:
```bash
   sudo suricata -T -c /etc/suricata/suricata.yaml
   sudo systemctl restart suricata
```

## Testing
| Rule | Test tool | Command |
|------|-----------|---------|
| Port scan | <tool> | `<command>` |
| Slowloris-style | <tool> | `<command>` |
| hping3 ICMP flood | hping3 | `<command>` |
| nping ICMP flood | nping | `<command>` |

Replace the placeholders with the commands you used. Use `<TARGET_IP>`
instead of real addresses.

## Results in Wazuh
Alerts appear under **Threat Hunting > Events** for the Suricata agent.
All Suricata alerts arrive as Wazuh rule ID `86601` (level 3) and the
Suricata signature name is shown in the rule description.

## Observations
- Thresholds need tuning: too low causes noise, too high misses attacks.
- The ICMP flood rules match a marker string in the payload, so they fire
  on tagged lab traffic and not on every flood.
- All Suricata alerts share one Wazuh rule ID and severity. Custom Wazuh
  rules can set different severity levels per signature (next step).

## Screenshots
![Custom rules file](../screenshots/custom-rules-file.png)
![Port scan and Slowloris alerts](../screenshots/alerts-portscan-slowloris.png)
![hping3 ICMP flood alerts](../screenshots/alerts-hping3.png)
![nping ICMP flood alerts](../screenshots/alerts-nping3.png)
