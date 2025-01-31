# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](![azure plot 12 (3)](https://github.com/user-attachments/assets/7481cd24-4291-429e-9f60-05ccbe4a0699)
)
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)
(![anime 2](https://github.com/user-attachments/assets/a25cf51b-2954-4047-92e3-41ef751e7f78)
)

## Architecture After Hardening / Security Controls

![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)
![DALL·E 2024-08-01 18 38 04 - A Power Rangers-style version of a cloud diagram depicting Public Internet connected to various components like SQL database, key vault, virtual machi](https://github.com/user-attachments/assets/f8482eb3-22f9-4a87-8b29-aee3241324df)


The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources were deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint.

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/1qvswSX.png)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/G1YgZt6.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/ESr9Dlv.png)<br>

## Additional Attack Maps
![Additional Attack Maps 1](https://i.imgur.com/mvfYTIq.png)<br>
![Additional Attack Maps 2](https://i.imgur.com/gJYsH5T.png)<br>
![Additional Attack Maps 3](https://i.imgur.com/acSrt3J.png)<br>
![Additional Attack Maps 4](https://i.imgur.com/KdaW0tV.png)

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 168 hours:
Start Time 2024-07-13:30:11.7980884Z

Stop Time 2024-07-25T21:30:11.7980884Z

| Metric                   | Count |
| ------------------------ | ----- |
| SecurityEvent            | 25,063|
| Syslog                   | 15,321|
| SecurityAlert            | 1,075 |
| SecurityIncident         | 12,959|
| AzureNetworkAnalytics_CL | 9,784 |

## Attack Maps After Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-07-30T21:24:54.9284657Z

Stop Time	2024-07-31T21:24:54.9284657Z

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            |1200
| Syslog                   | 40
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.


