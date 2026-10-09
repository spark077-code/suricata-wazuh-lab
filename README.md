# Suricata + Wazuh Lab

Blue team home lab: a Suricata IDS VM connected to a Wazuh SIEM as an agent,
with Suricata alerts visible in the Wazuh dashboard. Custom detection rules
are added in this repo.

This lab builds on my Wazuh server setup:
[wazuh-siem-home-lab](https://github.com/spark077-code/wazuh-siem-home-lab)

## What's Covered
- Deploying a Wazuh agent on a Suricata (Linux) VM
- Forwarding Suricata `eve.json` logs to Wazuh
- Verifying events in the Wazuh dashboard
- Custom Suricata rules/signatures (coming in this repo)

## Lab Setup
| Component | Role |
|-----------|------|
| Wazuh server | Manager, indexer, dashboard |
| Suricata VM (Linux) | Network IDS + Wazuh agent |

## Guides
1. [Connect the Suricata agent](docs/01-connect-suricata-agent.md)
2. Custom rules (coming soon)

## Screenshots
![Agent deployed](screenshots/agents-deployed.png)
![Suricata events](screenshots/suricata-events.png)
![Suricata events timeline](screenshots/suricata-events2.png)

## Roadmap
- [x] Deploy Wazuh agent on the Suricata VM
- [x] Forward Suricata logs to Wazuh
- [ ] Write custom Suricata rules
- [ ] Test rules and view alerts in Wazuh
- [ ] Connect Windows 10 agents

## Connect
[LinkedIn](PASTE_YOUR_LINKEDIN_URL_HERE)
