# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/0UBgH3M.png)

## Introduction

In this project, I ddeveloped a mini honeynet in Azure to ingest log sources from various resources into a Log Analytics workspace, leveraging Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I collected security metrics in an insecure environment for 24 hours, implemented security controls to harden the environment, and measured metrics for an additional 24 hours to compare results.

The measured metrics are as follows:
- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/8IRETy5.png)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/3ffj8H9.png)

"BEFORE" Metrics: All resources were deployed with public exposure to the internet. Virtual Machines had unrestricted Network Security Groups and built-in firewalls, while other resources utilized public endpoints without Private Endpoint configurations.

"AFTER" Metrics: Network Security Groups were secured by blocking all traffic except from the admin workstation. Additionally, all resources were protected using built-in firewalls and Private Endpoints for enhanced security.

## Attack Maps Before Hardening / Security Controls
Network Security Group Allowed Inbound Malicious Flows
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/TYWQR39.png)<br>
Linux Syslog Authentication Failures
![Linux Syslog Auth Failures](https://i.imgur.com/Bq3FCjo.png)<br>
Windows RDP/SMB Authentication Failures
![Windows RDP/SMB Auth Failures](https://i.imgur.com/Nk27hoS.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics measured the insecure environment for 24 hours:
Start Time: 2024-11-09 16:37:01
Stop Time: 2024-11-10 16:37:01

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8967
| Syslog                   | 6130
| SecurityAlert            | 0
| SecurityIncident         | 147
| AzureNetworkAnalytics_CL | 3969

## Attack Maps After Hardening / Security Controls

```All map queries returned no results, indicating no instances of malicious activity during the 24-hour period following the implementation of hardening measures.```

## Metrics After Hardening / Security Controls

The following table shows the metrics measured in the environment for another 24 hours, after applied security controls:
Start Time: 2024-11-17 16:16:39
Stop Time: 2024-11-18 16:16:39

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 6651
| Syslog                   | 4
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

This project involved constructing a mini honeynet in Microsoft Azure, integrating log sources into a Log Analytics workspace, and utilizing Microsoft Sentinel to trigger alerts and create incidents from the ingested logs. Metrics were collected in the insecure environment before implementing security controls and then re-evaluated afterward. The results demonstrated a significant reduction in security events and incidents, highlighting the effectiveness of the applied measures.

It is important to consider that if the network resources had been heavily utilized by regular users, additional security events and alerts might have been generated during the 24-hour period following the implementation of the controls.
