---
layout: project
type: project
image: img/wazuh-splunk-landing.png
title: "Wazuh → Splunk Integration"
date: 2026
published: true
labels:
Wazuh
Splunk
SIEM
Ubuntu
SPL
summary: "Built an end-to-end Wazuh to Splunk log-forwarding pipeline in a home-lab SOC environment, forwarding JSON security alerts into Splunk and validating them with SPL searches."
---
<br />


# Project A — Wazuh → Splunk Integration

A home-lab SOC project that forwards Wazuh security alerts into Splunk Enterprise, then validates the data with SPL searches.

![SIEM](https://img.shields.io/badge/SIEM-Wazuh-blue) ![Splunk](https://img.shields.io/badge/Log_Analytics-Splunk-green) ![Status](https://img.shields.io/badge/Status-Completed-success)

---

## Summary

I built an end-to-end log-forwarding pipeline between Wazuh and Splunk in a VirtualBox home lab. Wazuh Manager runs on an Ubuntu Server VM and writes security alerts to `alerts.json`. The Splunk Universal Forwarder monitors that file and ships the JSON alerts to Splunk Enterprise running on the Windows host. I then validated the data in Splunk using SPL searches for raw events, alert severity levels, and rule descriptions.

The goal was to prove that security events can be generated, forwarded, indexed, searched, and summarized — the core of a real SOC data workflow.

---

## Tools used

| Tool | Role in the project |
| --- | --- |
| Wazuh Manager | Generates security alerts and writes `alerts.json` |
| Splunk Enterprise | Receives, indexes, and searches the security logs |
| Splunk Universal Forwarder | Forwards Wazuh log files from Ubuntu to Splunk |
| Ubuntu Server 22.04 (VM) | Wazuh lab server |
| Windows host | Runs Splunk Enterprise (the receiving endpoint) |
| VirtualBox NAT networking | Ubuntu reaches the Windows host at `10.0.2.2` |
| PowerShell / Linux terminal | Firewall, service, and forwarding configuration |

---

## Architecture

```
┌─────────────────────────────────────────┐
│  Ubuntu Server VM                        │
│  ┌────────────────────────────────────┐  │
│  │  Wazuh Manager                     │  │
│  │  /var/ossec/logs/alerts/alerts.json│  │
│  └────────────────┬───────────────────┘  │
│                   │                       │
│  ┌────────────────▼───────────────────┐  │
│  │  Splunk Universal Forwarder        │  │
│  │  monitors alerts.json              │  │
│  │  index=wazuh                       │  │
│  │  sourcetype=wazuh-alerts-json      │  │
│  └────────────────┬───────────────────┘  │
└───────────────────┼──────────────────────┘
                    │  forwards over NAT
                    │  10.0.2.2 : 9997
                    ▼
┌─────────────────────────────────────────┐
│  Windows Host                            │
│  ┌────────────────────────────────────┐  │
│  │  Splunk Enterprise                 │  │
│  │  Receiving port: 9997              │  │
│  └────────────────────────────────────┘  │
└─────────────────────────────────────────┘
```

---

## Implementation steps

1. Mapped the VM network path and confirmed `10.0.2.2` is the Windows host as seen from inside the VM.
2. Installed the Splunk Universal Forwarder on Ubuntu and started `splunkd`.
3. Created a dedicated Splunk index named `wazuh` in Splunk Enterprise.
4. Enabled Splunk receiving on TCP port `9997` and allowed the port through Windows Firewall.
5. Pointed the forwarder at Splunk (`10.0.2.2:9997`).
6. Found that an agent-only install did **not** create `alerts.json`, then installed Wazuh **Manager**.
7. Verified Wazuh Manager was active and that `/var/ossec/logs/alerts/alerts.json` existed.
8. Added a Splunk monitor for `alerts.json` with `sourcetype=wazuh-alerts-json` and `index=wazuh`.
9. Validated ingestion in Splunk with SPL searches for raw events, rule levels, and rule descriptions.

---

## Key commands

**Find the Windows host from the Ubuntu VM**
```bash
ip route | grep default
```

**Point the Universal Forwarder at Splunk**
```bash
sudo /opt/splunkforwarder/bin/splunk add forward-server 10.0.2.2:9997 -auth admin:<password>
```

**Verify Wazuh Manager is running**
```bash
sudo systemctl status wazuh-manager --no-pager
```

**Verify alerts.json exists**
```bash
sudo ls -lh /var/ossec/logs/alerts/alerts.json
```

**Monitor Wazuh alerts.json**
```bash
sudo /opt/splunkforwarder/bin/splunk add monitor /var/ossec/logs/alerts/alerts.json \
  -index wazuh -sourcetype wazuh-alerts-json -auth admin:<password>
```

**Verify forwarding is active**
```bash
sudo /opt/splunkforwarder/bin/splunk list forward-server -auth admin:<password>
```

---

## SPL searches used for validation

**Raw Wazuh JSON alerts**
```spl
index=wazuh sourcetype=wazuh-alerts-json | head 20
```

**Alert count by severity level**
```spl
index=wazuh sourcetype=wazuh-alerts-json
| spath path=rule.level output=rule_level
| stats count by rule_level
| sort - rule_level
```

**Top alert descriptions**
```spl
index=wazuh sourcetype=wazuh-alerts-json
| spath path=rule.description output=rule_description
| stats count by rule_description
| sort - count
```

**Clean event table**
```spl
index=wazuh sourcetype=wazuh-alerts-json
| spath path=rule.level output=rule_level
| spath path=rule.description output=rule_description
| spath path=agent.name output=agent_name
| table _time agent_name rule_level rule_description location
```

---

## Screenshots / evidence

**1. Wazuh Manager service active** — `wazuh-manager.service` is loaded, enabled, and `active (running)`.
![Wazuh Manager active](screenshots/01-wazuh-manager-active.png)

**2. Splunk returns Wazuh alerts.json events** — `index=wazuh sourcetype=wazuh-alerts-json` returns Wazuh JSON security alerts in Splunk.
![Splunk events](screenshots/02-splunk-events.png)

**3. alerts.json exists** — the alert file is present on the Wazuh Manager with a real size and timestamp.
![alerts.json exists](screenshots/03-alerts-json-exists.png)

**4. Alert count by rule level** — severity levels 3, 4, and 7 observed in Splunk.
![Rule level count](screenshots/04-rule-level-count.png)

**5. Top rule descriptions** — PAM login sessions, successful sudo to ROOT, and CIS Ubuntu benchmark findings.
![Top rule descriptions](screenshots/05-top-rule-descriptions.png)

---

## Validation results

| Validation check | Observed result |
| --- | --- |
| Wazuh Manager service | `active (running)` |
| alerts.json path | `/var/ossec/logs/alerts/alerts.json` exists (522 KB) |
| Splunk index | `index=wazuh` returned events |
| Splunk sourcetype | `sourcetype=wazuh-alerts-json` returned Wazuh JSON alerts |
| Rule level summary | Levels 3 (125), 4 (1), and 7 (109) |
| Top alerts | PAM login events, sudo to ROOT, CIS Ubuntu benchmark findings |

---

## Key findings and takeaways

- **Agent vs. Manager matters.** The Wazuh agent collects endpoint activity, but the Wazuh **Manager** is what generates `alerts.json`. An agent-only install left the file missing.
- **Port 9997 is critical.** Splunk receiving must be enabled *and* the port allowed through Windows Firewall, or no data flows.
- **NAT gateway discovery matters.** In this VirtualBox NAT lab, Ubuntu reaches the Windows host through `10.0.2.2`.
- **Index and sourcetype keep searches clean.** Using `index=wazuh` and `sourcetype=wazuh-alerts-json` made the data easy to validate.
- **Troubleshooting is part of the work.** Old download links, a wrong-shell command, a forwarder login failure, and the missing `alerts.json` were each solved step by step.

---

## Troubleshooting notes

| Problem | Cause | Fix |
| --- | --- | --- |
| `New-NetFirewallRule` not found | A Windows PowerShell command was run in Ubuntu by mistake | Run it in Windows PowerShell as Administrator |
| 404 while downloading Splunk UF | Outdated Universal Forwarder download link | Use a current Splunk UF download package |
| Forwarder login failed | Forwarder had an old local admin password | Reset forwarder credentials via `user-seed.conf` |
| alerts.json missing | Only the Wazuh agent was installed | Install Wazuh Manager and verify the alerts path |

---

## What this project demonstrates

SIEM integration, log forwarding, Linux service management, Splunk indexing and SPL search, and hands-on troubleshooting of a real security data pipeline.

---

*Project A of a 4-part SOC home-lab portfolio.*
